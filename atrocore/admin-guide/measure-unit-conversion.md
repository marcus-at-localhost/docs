# Measure Unit Conversion

## Creating Measures and Units

AtroCore enables you to manage different Measures (e.g length or weight) and Measure Units (e.g. cm, mm, dm, m) as well as supports the automatic measure unit conversion. 

To manage this data go to `Administration > Measures`. Here you see the list of Measures, which are currently available in your system.

![measure-list](../_assets/admin-guide/measure-unit-conversion/measure-list.png)

To create a new Measure, click on the button `Create Measure`. Popup windows opens, here you can set the name for your new measure and save the record.

![measure-create](../_assets/admin-guide/measure-unit-conversion/measure-create.png)

> Measure is used for the fields and product attributes of type "unit". You can define multiple Measures with the same nature, if you plan to use different Units for different attributes or fields. Thus, you may create the Measure "Length 1" with "mm" and "cm" as Units and the Measure "Length 2" with "mm", "m" and "km" as Units and assign each Measure to different attributes of fields.

After Measure is created you can create and assign Units to it. These are visible it the "Units" panel.

![measures-units](../_assets/admin-guide/measure-unit-conversion/measures-units.png)

To create a new Unit, click on the "+" icon in the top right corner of this panel. 

![unit-create](../_assets/admin-guide/measure-unit-conversion/unit-create.png)

Here you can 
- define the name for the new Unit e.g. "mm" or "cm", 
- set the "Multiplier", which is used for automatic unit conversion and 
- choose the Unit to which the current Unit should be automatically converted.

If you create very first Unit for some Measure, this Unit is automatically marked as "default", and its "Multiplier" is set to "1".

> If you want to store full unit names e.g. "meter" you need to add the field "description" to the Detail (small) Layout for Units and use this field for it. You can also create new field for that via "Entity Manager".

To edit a data record, use its menu. On the "Edit View" you can set a new Unit as a "default" Unit. In this case its "Multiplier" is set to 1, and all other "Multipliers" will be adjusted accordingly. The Unit marked as "default" cannot be deleted.

![unit-create](../_assets/admin-guide/measure-unit-conversion/unit-edit.png)

> "Default" Unit is a base Unit which the calculation for all other Units for the current Measure is based on. This is the only purpose of this setting.

## Localized Measure Units
In AtroCore you can create and use multiple Locales. For each Locale, you may decide whether you want to enable Measure Unit localization or not. This is done by adding a measure to the Locale and setting which units should be available for this measure. Click on the "Select" button for that.

![locale-measure-select](../_assets/admin-guide/measure-unit-conversion/locale-measure-select.png)

In the popup window select the measures for which you want to enable localized units and click on the button "Select".

![locale-measure-select-popup](../_assets/admin-guide/measure-unit-conversion/locale-measure-select-popup.png)

After a Measure is added it will appear in the "Measures" panel for your Locale. 

![locale-measures-list](../_assets/admin-guide/measure-unit-conversion/locale-measures-list.png)

Per default all Units for the Measure are automatically added. To remove some or them open the appropriate data record for editing.

![locale-measures-list](../_assets/admin-guide/measure-unit-conversion/locale-measures-edit.png)

Here you need to leave only Units, which should be available for the current Locale. You must also choose a default Measure Unit for the Locale.

> Example: In you want that some user should be able only to work with "cm", "dm" and "mm" as Units for the Measure "Length" you need to enable only these units for the Locale of this user.

### Automatic Unit Conversion

"Multiplier" is used to automatically convert the values. It defines how many current Units match 1 default Unit.

> Example: You have "mm" set as "default" Unit and its "Multiplier" is set to "1". You want to add "cm", its "Multiplier" should be set to 0,1 because 1 mm = 0,1 cm.

The values for the fields and attributes of type "Unit" are always stored as shown. 

The user always sees the value as it is stored, if this unit is available for his Locale (if no Locale is set for system, system assumes the user has the same Locale as the system). Otherwise, he sees the value in Unit which is set as "Convert to" Unit for the stored Unit, provided this Unit is available for his Locale. If this Unit is not available than the user sees the value in Unit which is set as "default" unit for this Measure for his Locale.

> Example: User A sees only kilometers (miles are set as "Convert to" for kilometers) and meters (default for his Locale), User B sees only miles (default for his Locale). User A saves the value "10 km". User B sees this value as "6.21371 miles". User B changes the value to 10 miles (value "10 miles" is stored). User A sees this value as "16093,4 m". 

### API

API returns additionally the values for all fields and attributes of type "unit" in all Units of their Measure.


