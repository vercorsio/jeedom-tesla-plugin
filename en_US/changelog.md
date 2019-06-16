<a name="1.7.0"></a>
# 1.7.0 (2019-06-16)

### Features
 * Add currencies for cost displays (possible choices are EUR, USD, CHF and GBP)
 * [**Range Tracking**] Add a sleep mode to reduce frequency of car updates when the car is stopped since 8 minutes. During the day, the frequency changes from 1 call every 5 seconds to 1 call every 60 seconds. During the night (11 PM till 5 AM) the frequency changes to 1 call every 10 monutes. The numbers 8, 5, 60 et 10 above can be modified from the tesla configuration panel.
  * [**Range Tracking**] Next to the addition of sleeping mode, use can freely activate the Automatic Management of daemon.
  * [**Range Tracking**] When the car is offline, the range curve turns to black.

### Improvements

 * Improve rendering performance when loading big trakcing files.

Thanks to `matts` from [Automobile Propre](https://forums.automobile-propre.com/topic/piloter-sa-tesla-avec-jeedom-13412/) forum for his feedback and tests !

<a name="1.6.1"></a>
# 1.6.1 (2019-05-15)

### Features

 * [**Health**] Add a serie of tests to make sure the plugin is doing well (menu Analyze / Health / plugin Tesla ).

### Improvements

 * When the "Automatic Management" is set, the button to start/stop the *Range Tracking* is disabled.

### Fixes
 * Check and repair the tracking files permissions.
 A file with bad permission, may have impact on *Range Tracking* display.

Thanks to `J0kers` from [Automobile Propre](https://forums.automobile-propre.com/topic/piloter-sa-tesla-avec-jeedom-13412/) forum for his feedback and tests !


<a name="1.6.0"></a>
# 1.6.0 (2019-05-07)

### Features

 * [**Range Tracking**] Add a serie in the graph to display power of charge.
 * [**Range Tracking**] Ability to choose which column to display in the table and sort them.
 * [**Widget**] Add a button to start/stop the range tracking in the widget.

### Improvements

 * Improve the way range tracking is managed by Jeedom.
 * Ready for Jeedom V4 !

### Fixes
 * Minor fixes
  
### Update instructions
 * As cron has been changed to 'daemon', it's better to not activate the "Automatic Management" in the plugin configuration panel. 
 As a matter of fact, the "Automatic Management" will tess Jeedom to make sure the daemon is always up, restarting it if stopped. For the range tracking, we prefer to start and stop it manually.

<a name="1.5.2"></a>
# 1.5.2 (2019-04-08)

### Improvements

 * [**Range Tracking**] The tracking files are stored into the tesla plugin directory. They are moved while updating the plugin if old files were found in their previous location.
 * [**Command**] The calculation of the charging start time has been improved.
 * Use UTC time for time display (take in account the time zones and the sunlight saving).
 * When Tesla server does not answer, the plugin makes multiple attempts until it finally fails.
 * Imrpovement in `tesla` logs.
 * [**Command**] Add a new Info command `Info batteryu level` that returns the percentage of the battery.

### Fixes
 * No access to tesla equipements when they are disabled of plugin is disabled.
 * [**Widget**] Display wheels and perofmance pack on Model 3.
 * [**Widget**] Display right colors on Model 3.
 * [**Widget**] Some web browsers display white background for charging limit slider. Fixed
 
### Known Issues
 * [**Scnario**] In the night, a trace in tesla log may indicate that the charging was not possible. However, the Tesla server may trigger it when car is awake. It is recommanded to add an awake command before starting the charge.

<a name="1.5.1"></a>
# 1.5.1 (2019-03-20)

### Improvements
 * [**Range Tracking**] Improve performance for graph rendering (6 times faster)
 * [**Command**] "Info Charging" now returns 'Driving' when car is moving.

### Fixes
 * [**Widget**] Fixed unit issue (kW -> kWh) 
 * [**Range Tracking**] First trip of the day was seen as parked. Fixed
 

<a name="1.5.0"></a>
# 1.5.0 (2019-03-14)

### Features
* [**Range Tracking**] It is now possible to switch from distance to energy. Some settings about battery is required on the vehicle configuration panel.

### Improvements
 * [**Range Tracking**] Live is automatically activated (last 5 min) when car is driving.
 * [**Range Tracking**] "Live" checkbox has been moved to a new option `Live OFF` in the time window selector.
 * [**Range Tracking**] Update curve extremes on the fly for a better rendering.
 * [**Range Tracking**] In Mobile version, for a better readability on large devices (such as Tesla screens), the width of curve lines are now bigger.
 * [**Widget**] Clicking on `trunk`, `frunk` and `lock` buttons now require user to confirm the action (modal window).
 * Added a red Model Y in the fake cars.
 
### Fixes:
 * [**Range Tracking**] Fix background color when HVAC is on.
 * [**Widget**] On Model 3, car image displays now the right color and wheels, and the roof button has been remove.

### Tips:
* [**Range Tracking**] To automagically display the `Tesla` view on Mobile version, you can define `Tesla` as the default `Mobile` view in Jeedom profile configuration : `User menu` -> `Admin Profil` -> `Interface tab`.

### Known Issues
* [**Range Tracking**] When a lot of data has been received on a single day (long trips), the plugin may take a long time to display the graph (or even cannot display it).



I want to thank `Bob Jouy` (https://twitter.com/bobjouy) for his feedback, suggestions and tests he made on his Model 3 !

<a name="1.4.2"></a>
# 1.4.2 (2019-02-14)

### Improvements
* [**Range Tracking**] A new command 'Control the range tracking' allows to programatically start and stop the range tracking thru a scenario.
* [**Widget**] Update title and subtitle when a software update is in progress.

### Fixes
* Fix issue with 'last seen text' in widgets that toggles multiple values.

<a name="1.4.1"></a>
# 1.4.1 (2019-02-08)

### Improvements
* [**Scenario**] The command 'Control the charging' has a new argument 'Estimer' that will start a short charging to calculate the starting time. Note: It simplifies the scenario to start a charging and make it more robust.

<a name="1.4.0"></a>
# 1.4.0 (2019-02-04)

### Features
* [**Scenario**] Added the commands that based on the charging end time and the charging percentage will provide the specific time when the charging needs to start. This can be used in Jeedom scenario (cf doc).

<a name="1.3.1"></a>
# 1.3.1 (2019-01-30)

### Improvements
* [**Range Tracking**] In live mode live, the range curve turns to violet when HVAC is activated.
* [**Range Tracking**] It is now possible to display example graph for a fake Tesla.
* Widget is doubled size in mobile mode, when device width is bigger than 500px.

### Fixes
* Cleanup.

<a name="1.3.0"></a>
# 1.3.0 (2019-01-23)

### Features
* Add the '**Range Tracking**' panel to let user visualize on a graph the range evolution depending on what the car is 'doing': **driving**/**charging**/**parking**.

### Known issues
* The 'Range Tracking' panel is not translated in english yet.
 
<a name="1.2.2"></a>
# 1.2.2 (2019-01-07)

### Improvements
* Add an indication in the widget to tell when last update did occur ("Updated just now", "Updated 2 minutes ago" ...).

### Fixes
* Remove the message "Erreur d'accès au Seveur Tesla", when system tries to wake up the car.

<a name="1.2.1"></a>
# 1.2.1 (2018-12-22)
### Fixes
* Issues raised when Jeedom runs on top of php 5.6 have been fixed.

<a name="1.2.0"></a>
# 1.2.0 (2018-12-19)
### Features
* Add Mobile widget.
* Add Info command to retrieve the inside temparature (ex: useful for a scenario that triggers an HVAC start, ...).
* Add a wakeup command that triggers 3 attempts (with 5 sec between two tries) to wake up the vehicle (3 et 5 can be configured in the plugin panel).
* When plugin is upgrading, it re-synchronizes all configured vehicles.

### Improvements
* Most of the action commands can be used in Jeedom scenarios.
* More english translations.

### Fixes
* Sunroof button is now working properly.

### Known issues
* The wake up function better works when the **Always connected** mode is activated in the car.
 

Thank you to `Kim` for his feedback !


<a name="1.1.0"></a>
# 1.1.0 (2018-12-07)
### Features
* Control driver and passenger temperatures.
* Control trunk, frunk and sunroof openings.
* Control charging limit using dashboard or scenario.
* Display temperatures in `°C` or `°F` following car settings
* Display distances in `km` or `miles` following car settings


### Improvements
* Added hover effects on buttons.
* Optimize and clean code (added a css file shared among templates, ...)

### Known issues
* [Temp settings] Due to a limitation in Tesla API, we cannot toggle from `SYNC` to `Not SYNC`. Thus we only can set passenger temp when `Not SYNC` is already selected in the car.

<a name="1.0.0"></a>
# 1.0.0 (2018-11-29)
### Highlights
* This is the first **stable** version published on Jeedom market !
* Keep posted, next version will have more features (set temperatures, charging limit, ...) !

Many thanks to Jeedom team `Loic` and `Alexandre`, and to beta testers `carfnann` and `philippe` for their tests and inputs !

<a name="0.3.0"></a>
# 0.3.0 (2018-11-23)
### Bug Fixes
* Properly refresh charging button after action on it.
* Display battery percentage in battery graph.
* Add button to remove fake Teslas.
* Add Model 3 and Roadster in the list of fake Teslas.
* Improve authentication and token retrieval.

<a name="0.2.0"></a>
# 0.2.0 (2018-11-18)
### Features
* Update documentation
* Added english as supported language

<a name="0.1.0"></a>
# 0.1.0 (2018-11-10)

### Highlights
* This is the first **beta** version published on Jeedom market


### Features
* Control and display charging
* Control and display HVAC
* Control and display lock

  

