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

  

