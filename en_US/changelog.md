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
 
### Fixes:
 * [**Range Tracking**] Fix background color when HVAC is on.
 * [**Widget**] On Model 3, car image displays now the right color and wheels, and the roof button has been remove.

 ### Tips:
* [**Range Tracking**] To automagically display the `Tesla` view on Mobile version, you can define `Tesla` as the default `Mobile` view in Jeedom profile configuration : `User menu` -> `Admin Profil` -> `Interface tab`.


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

  

