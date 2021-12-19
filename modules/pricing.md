# Pricing 

The "Pricing" module enables to operate with different prices for different customer groups and channels. In addition, you can take usage of scale pricing capabilities and automatic price recalculation for different currencies. The module enables you also to set the price in each currency for any amount of products manually.

You can create multiple price profiles to be able to set different prices. Examples of price profiles may be the following: Regular prices, Wholesale prices, B2B prices, VIP clients prices, Seasonal discounts, etc.

## Administrator Functions  

The "Pricing" module significantly extends the pricing functionality of the AtroPIM PIM System.

After the module installation, a new entity "Price Profile" is added to the system. It is also automatically added to your [Navigation Menu](../atropim/user-guide/user-interface.md#navigation-menu). New "Prices" panel is added to the [Products](../atropim/user-guide/products.md) detail view page.

### Currency Configuration

If you want to enable working with multiple currencies you need to configure these in the administration, go to `Administration > Currency`:

![Currency settings](./_assets/pricing/currencies.png)

The `EUR` currency is set by default, but you can expand the list with as many currencies as needed. To do this, click the `Currency List` field and choose the desired options from the drop-down list that appears. 

Here you can also select the default currency (to be used when creating new records) and currency format via the corresponding drop-down lists. In the `Currency Decimal Places` field, specify the number of decimal places to be used in currency fields and calculations or leave the field empty to have all filled decimal places displayed.

On the "Currency Rates" panel you should also specify the conversion rates for the currencies available in the currency list if you want to use automatic price conversion. For this, select the base currency and enter its rate value according to other currencies.

Click the `Save` button to apply your currency configuration.


### Access Rights

By default, the pricing feature is enabled for all users, however, it can be disabled for certain user roles, if needed, on the `Administration > Roles > 'Role name'` page:

![Access rights](./_assets/pricing/pricing-role-cfg.jpg)

Please, note that access rights for `Channels` and `Products` should also be enabled.

## User Functions

After the "Pricing" module is installed and configured by the administrator, user can work with price profiles in accordance with his role rights that are predefined by the administrator.

## Price Profile

A price profile is a configurable price variation that allows you to define various prices for different groups of customers, both in numbers and currencies. 

![price profiles](./_assets/pricing/price-profiles.png)

### Creating

To create a new price profile record, click `Price Profiles` in the navigation menu to get to the profiles [list view](../atropim/user-guide/views-and-panels.md#list-view), and then click the `Create Price Profile` button. The common creation window will open:

![price-profile-create](./_assets/pricing/price-profiles-create.png)

Here enter the desired name for the price profile record being created and define the currencies to be used in it (in accordance with the ones defined on the [currency configuration](#currency-configuration) step). 

Please, note that the default currency cannot be removed.

Activate the price profile and enter its description, if needed.

Please, note that only activated profiles are added to the products available in the system.

Click the `Save` button to finish the price profile creation and move to its [configuration](#configuring) or `Cancel` to abort the process.

### Assigning Price Profiles to Channels

After the new price profile is saven on the panel "Channels" you can select the channels, for which this price profile should be valid.

![price-profile-example](./_assets/pricing/price-profiles-example.png)

Alternatively, you can link price profiles with channels on the "Price Profiles" panel within the desired channel detail view page:

![Price profiles panel](./_assets/pricing/channels.png)

Thus, one Price Profile can be assigned to multiple Channels, and one Channel may have multiple Price Profiles assigned to it.

## Setting Product Prices

As soon as the active Price Profile is created, it is added to all products available in the system and is displayed on the "Prices" panel:

![prices](./_assets/pricing/prices.png)

Here you can define product prices for all currencies pre-configured for the given price profile. To add a new price entry click on the plus icon in the top right corner of the panel.

![prices](./_assets/pricing/prices-add.png)

A popup window appears, in which you can set the desired minumum amount, select the respective price profile, currency and the price.

![prices](./_assets/pricing/prices-add-popup.png)

If a non-main currency is selected and a price entry for the current amount in the main currency exists, option "Calculate automatically" appears additionally. If set the price for the current currency will be calculated automatically. In the future if the price in the main currency for the current amount is changed the prices in this currency will be automatically recalculated. For such records "Base price" is set and is displayed on the "Prices" panel, so you can easily recognize, which prices will be recalculated automatically.

To edit some price enty select `Edit` from the record menu:

![prices](./_assets/pricing/price-edit.png)

You can select `View` to see in the side popup all the information about a certain price entry.

![prices](./_assets/pricing/price-view.png)

To remove a price entry, click on the option `Remove`.


