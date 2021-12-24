# Measure Unit Conversion


1) Default value for unit fields and attributes should be configurable (issue is opened: https://my.atrocore.com/#Issue/view/618b9c15bf30985da)

1a) Default unit for the field or attribute can be chosen only from units available for the default system locale.

2) New Entity "Locale" is to be added.

3) Locale Settings (for system and each user) will be moved to Locale Entity. Multiple records can be created here. 

4) For the system you must set the locale (one should always be preconfigured and will have the Name "Default Locale"). The locale, which is selected for the system or some user, cannot be removed. For the system locale is a mandatory field.

4a) You can set different locales for different users (=one locale per user, so you need to configure a locale only once, not for each user separately).

4b) Global default unit for some measure is always the same as the default unit for the system locale (= which is assigned to the system) for that measure.

5) For each locale you can (not must) configure, which units should the user be able to use (e.g. for length "miles", but not "kilometers"). If you create a new measure relation for some locale the list of units and default units are mandatory fields. Default unit must only be chosen from the chosen units.

5a) Each measure can be linked with any locale only once.

5b) Locale is an optional field for a user.

5f) If no measure record is linked with some locale, no filter applies and all units should be available for a user with that locale. This is valid also for a default locale.

6) Add the possibility to set the checkbox "Default | Standard" (for setting the global default unit for the measure), "Multiplier | Multiplikator" as float, "Convert to | Konvertieren zu" as a dropdown in the relation to "Unit" entity. 

Only units, selected for the locale of the current user can be chosen via frontend and via API. If nothing is selected for the locale all units are available.

7) In dropdown "Convert to" I can choose via dropdown, which unit corresponds with the current unit.

9) For the default unit the multiplier is always 1 and cannot be changed. Only one unit can be set as the default unit. Each measure always should have the default unit. Thus  the first unit added for some measure should always be automatically marked as default value. 

9a) If I want to set the current unit as the new default unit, its multiplier should be set to 1 and multipliers of all other units should be recalculated respectively.

9b) The Unit marked as default cannot be deleted. It is not possible to delete the last unit for the value (which should be marked as default).

10) If a user creates a new attribute or field of type unit, for the default option all units are available. While creating attributes of field value default value is determined based on recalculation principles.

11) The unit attribute or unit field value is always stored as shown. 

12) The user always sees the value as it is stored, if this unit is available for him. Otherwise he see the value 
in unit which is set as "Convert to", for the stored unit, provided this unit is available for his locale, if not available than
in unit which is set as default unit for this measure for his locale

12a) If the user will open the product for editing and will not change the value of this unit field or attribute the database will keep the value which is stored (he sees the value in one unit and it is still stored in some other unit).

Example: User A sees only kilometers and meters (default for his locale), User B sees only miles (default for his locale, set as "Convert to'' for kilometers). User A saves the value 10 km. User B sees this value as 6.21371 miles. User B changes the value to 10 miles (he sees the value as 10 miles, value is stored as 16,0934 km, if kilometer is set as “Convert to” for miles, if “Convert to” is not set, than 16093,4 m is stored). User A sees this value then as it is stored. 

13) API should always return unit value in the “local unit”, it means value is returned as it is stored, if this unit is available for the locale or the API user. Otherwise the value is returned
in unit which is set as "Convert to", for the stored unit, provided this unit is available for the locale of this user, if not available than
in the unit which is set as the default unit for this measure for the locale of the API user.

ADDITIONALLY the value is also returned in all other units of this measure. The “Convert to” unit of the unit determined in the previous step (“local unit”) is always returned on THE FIRST PLACE of these additional values, if “Convert to” is set for this “local unit”.
