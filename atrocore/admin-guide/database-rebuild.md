# Database Rebuild

AtroCore uses its own ORM system. It means that the database structure is first described as metadata with the help of JSON files. This metadata is synchronized than with the real database structure.
Sometimes, some system errors result in differences between the database structure and these metadata. To solve this kind of problems the feature `Rebuild Database` was implemented.

Indication of the problems with the database structure could be "Bad Server Response" errors while you visit the list or detail page for some entity. In this case go to "Administration > Settings" and click on the link `Rebuild Database` to actualize your database structure. If it does not help, contact the support.