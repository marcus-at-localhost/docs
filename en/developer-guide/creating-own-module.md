# Modules creating

## Overview
In this tutorial you will learn how to create and install your own module for AtroCore software development platform.
Example module we refer to in this guide can be found here: https://github.com/atrocore/test-module

## Module structure
Module consist of backend and frontend parts.

![Module structure](../../_assets/developer-guide/module-creating/module-structure.png)

As you can see module consist of two main folders - `app`, where the backend part is stored, and `client` - where the frontend part is stored. The root module folder should contain composer file with all information about the module as well as all its dependencies and may contain any other files such as markdown files, git files, etc.

### Backend folder

`app` folder has the following structure:

- `Module.php` - main module class where module configuration (module load order, path to files, loading metadata and layouts, etc.) is described
- `Controllers` - contains the controllers of the module
- `Entities` - folder with ORM entity classes
- `Listeners` - event listener classes
- `Repositories` - stores entities repositories where are contain queries logic.
- `Resources` - has several subfolders such as:
  - `i18n` - contain modules translations
  - `layouts` - contain module layouts
  - `metadata` - contain module metadata, which are available in the backend as instance of `Espo\Core\Utils\Metadata` class from container
  > To get data from metadata use such way `$metadata->get(['entityDefs', 'Test', 'fields', 'name', 'type'], 'varchar')`.
  Second argument means default value. In frontend metadata object is accessible from all views object by method `getMatedata`.
  For example `this.getMetadata().get(['entityDefs', 'Test', 'fields', 'name', 'type'])`.
  - Metadata has next sections:
     - `app` - application definitions
     - `clientDefs` - frontend parameters for entity types
     - `entitiyDefs` - entity definitions such as fields, links, indexes
     - `scopes` - general parameters for entity types
     - `fields` - field type definitions
- `Services` - main business logic to work with data 
> A record service handles CRUD operations over entities. They extend base class `Espo\Services\Record`. 
- Main methods of the Record service are:
    - `readEntity` - get an entity record
    - `createEntity` - create new entity record
    - `updateEntity` - update entity record
    - `deleteEntity` - delete entity record
    - `findEntities` - get list of entities by search parameters, used in list view
    - `findLinkedEntities` - get list of related entities, used in relationship panels.

### Module.php

Here is a simple code example for module class.
```
    class Module extends AbstractModule
    {
        public static function getLoadOrder(): int
        {
            return 9999;
        }
    }
```

It has only one required method that must be realized - `getLoadOrder`. It must return integer value that point in module load order. A higher value indicates that the module will be loaded later.

### Frontend folder

All client files save in two main folders - `templates`, where are all module templates files, and `src`, that contain logic that will be work on client side.

For frontend used Backbone.js library. You can explore it in detail by following the next link to the documentation: https://backbonejs.org.

Basically, the frontend uses the view. Every page is rendered by multiple view objects. Every views can have their child views as child can have their own views. When view is rendered it has all HTML of his child views.

There is example of view `client/modules/test-module/src/views/test/record/detail.js`:

    Espo.define('test-module:views/test/record/detail', 'views/record/detail',
        Dep => Dep.extend({
    
            // template file
            template: 'test-module:test/record/detail',
    
            // handlers of DOM events
            events: {
                'click a[data-action="save"]': function (e) {
                    console.log(e.currentTarget);
                }
            },
            
            // logic initialization
            setup() {
                // call parent setup method
                Dep.prototype.setup.call(this);
    
                // create child view with options parameters
                // rendering of parent view will be delayed until child view is loaded
                this.createView('someView', 'test-module/test/some-view', {
                    key1: 'value1',
                    key2: 'value2'
                });
    
                // listen model changing event
                this.listenTo(this.model, 'change', () => {
    
                });
    
                // listen model saving or fetching
                this.listenTo(this.model, 'sync', () => {
    
                });
            },
    
            // data that will be returned to template
            data() {
                let data = Dep.prototype.data.call(this);
                
                data.key1 = 'value1';
                
                return data;
            },
    
    
            // called after view is rendered
            afterRender() {
                Dep.prototype.afterRender.call(this);
    
                // get child view
                let child = this.getView('someView');
    
                if (child) {
                    // remove child view from DOM
                    this.clearView('someView');
                }
            }
        })
    );

Template file `client/modules/test-module/res/templates/test/record/detail.tpl`:

    <div class="some-class">{{key1}}</div>
    <a class="action" data-action="save">Save</a>

AtroCore give you an abilities to define custom views for certain entity types. It must be set in `app/Resources/metadata/clientDefs` folder. There is example `app/Resources/metadata/clientDefs/Test.json`:

    {
        "controller": "pim:controllers/product",
        "iconClass": "fas fa-square",
        "views": {
            "list": "test-module:views/test/list",
            "detail": "test-module:views/test/detail"
        },
        "recordViews": {
            "list": "test-module:views/test/record/list",
            "detail": "test-module:views/test/record/detail"
        }
    }

**Detail view** `test-module:views/test/detail` contains all panels, relations, header bar with buttons in the top-right corner.

**Record detail view** `test-module:views/test/record/detail` contains all the above except header bar.

**List view** `test-module:views/test/list` contains Record List view, header and Search row view.

**Record list view** `test-module:views/test/record/list` contains only rows of records.

### Composer file
    
    {
        "name": "atrocore/test-module",
        "require": {
            "atrocore/core": "~1.3.12"
        },
        "autoload": {
            "psr-4": {
                "TestModule\\": "app/"
            }
        },
        "extra": {
            "treoId": "TestModule",
            "name": {
                "default": "TestModule"
            },
            "description": {
                "default": "Test module."
            }
        }
    }

There is nothing unusual here. It is only necessary to note, the `treoId` key - it contains the unique name of the module for its identification in system. `name` and `description` in accordance are name and description of module in Module Manager.

## Module installation

Modules installation is carried out from the Module Manager located at `Administration > System > Update & Modules` page. To make your module to be available for installation in the modules list , you need to perform certain actions, which will be described below.

> Should be noted that modules installation in AtroCore is based on Composer. You can get detailed information about Composer following the link https://getcomposer.org.

In our modules store showed modules that we had registered in our private repository. In future we will create a possibility to add your own modules in the store. At this moment you can install your module only adding requirement in your composer.json file, that was stored in your project root directory.

In your git or other VCS repository add and commit the `composer.json` file. Structure of it described in this paragraph - [Composer file](#composer-file).

Next create your first stable release.

![Release create](../../_assets/developer-guide/module-creating/git-releases.png)

You need to add a repository that contains your module. If your module stored in public GitHub repository, add next block in `repositories` key in `composer.json` file:

    {
        "type": "git",
        "url": "https://github.com/atrocore/test-module"
    }

For private repositories first you must generate access token for your GitHub account.

> Follow the link https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token to know about how create personal access token to GitHub.

When you will have personal access token add next block in `repositories` key:

    {
        "type": "git",
        "url": "https://username:usertoken@github.com/atrocore/test-module"
    }

, where `username` - your GitHub username, `usertoken` - your created in previous step personal access token.

> Instead GitHub you can use any VCS. You can get detailed information following the link: https://getcomposer.org/doc/05-repositories.md#vcs

Now in project `composer.json` file in `require` section add your module package name.

![Adding depandency](../../_assets/developer-guide/module-creating/adding-dependency-on-module.png)

If you open Module Manager you will see that your module prepared for install.

![Prepare for install](../../_assets/developer-guide/module-creating/module-manager-dependency.png)

Click on update button or run `php composer.phar update` command from terminal to initiate updating. In success your module will be displayed as installed. If was error while updating, you can see logs for detailed information. 
