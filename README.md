
# Angular Date Time Picker

**Angular date time picker - Angular reusable UI component**
**This package supports Angular 4**

## Updates
* Added **[minMoment]** and **[maxMoment]** to restrict the range of date or time, closes
   [#41](https://github.com/DanielYKPan/date-time-picker/issues/41), [#77](https://github.com/DanielYKPan/date-time-picker/issues/77)
* Added **(dataTimePickerError)** to emit a message whenever a invalid date or time is being selected.
* Fixed picker hover issue and position issue in IE 11. closes [#48](https://github.com/DanielYKPan/date-time-picker/issues/48), [#64](https://github.com/DanielYKPan/date-time-picker/issues/64), 
   [#70](https://github.com/DanielYKPan/date-time-picker/issues/70).
* Fixed time panel slider not working properly. closes [#74](https://github.com/DanielYKPan/date-time-picker/issues/74).
* Fixed Time picker does not update in 'inline' view, closes [#75](https://github.com/DanielYKPan/date-time-picker/issues/75).
* Fixed German translation error, closes [#76](https://github.com/DanielYKPan/date-time-picker/issues/76).

## Important
* Get locale working in the whole picker. Words not from MomentJS in the picker now are also translated.( 'ca', 'de', 'en', 'es', 'fr', 'lt', 'pl', 'pt', 'ro', 'ru', 'zh_CN', 'zh_HK', 'zh_TW').
   If the locale you are using is not working, please open an issue and help me to build that locale library.
* This npm package now rename to [ng-pick-datetime](https://www.npmjs.com/package/ng-pick-datetime), this is because this package now support angular 4. The previous package was named [ng2-date-time-picker](https://www.npmjs.com/package/ng2-date-time-picker).
* **[minDate]=" 2017-05-05 "** --- Set the picker minDate.
* **[maxDate]=" 2017-05-31 "** --- Set the picker maxDate.

## Other Similar Projects

* [Date Range Picker](https://github.com/DanielYKPan/date-range-picker)

## Description
Simple Angular date time picker. Online demo is [here](https://danielykpan.github.io/date-time-picker/). 
This picker is responsive design, so feel free to try it in your desktops, tablets and mobile devices. 
This picker uses [MomentJS](http://momentjs.com/)

## Installation

To install this component, follow the procedure:

1. __Install with [npm](https://www.npmjs.com):`npm install ng-pick-datetime --save`__
2. Add __DateTimePickerModule__ import to your __@NgModule__ like example below
    ```js
    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';
    import { MyTestApp } from './my-test-app';

    import { DateTimePickerModule } from 'ng-pick-datetime';

    @NgModule({
        imports:      [ BrowserModule, DateTimePickerModule ],
        declarations: [ MyTestApp ],
        bootstrap:    [ MyTestApp ]
    })
    export class MyTestAppModule {}
    ```
3. This picker use MomentJS. Remember to load MomentJS when you load your project from webpack or systemjs.**
4. If you are using __systemjs__ package loader add the following ng-pick-datetime properties to the __System.config__:
    ```js
    (function (global) {
        System.config({
            paths: {
                'npm:': 'node_modules/'
            },
            map: {
                // Other components are here...

                'ng-pick-datetime': 'npm:ng-pick-datetime',
                'moment': 'npm:moment',
            },
            packages: {
                // Other components are here...

				// the picker
                'ng-pick-datetime': {
                    main: 'picker.bundle.js',
                    defaultExtension: 'js'
                },
                // momentJS
                'moment': {
	                main: 'moment.js',
	                defaultExtension: 'js'
	            },
            }
        });
    })(this);
    ```

## Usage

Use the following snippet inside your template. For example:

```html
<input [ngModel]="momentValue | date: 'short'" [(dateTimePicker)]="momentValue" readonly />
```
<p>Or:</p>

```html
<input [ngModel]="momentValue | date: 'short'" [dateTimePicker]="momentValue" (dateTimePickerChange)="setMoment($event)" readonly />
```
```typescript
public setMoment(moment: any): any {
    this.momentValue = moment;
    // Do whatever you want to the return object 'moment'
}
```

 * Create a normal HTML Input and put it anywhere you want (like inside a form you already created). 
 * You may set the HTML Input to **readonly**, so you can only change the date value from the pop-up date-time picker.
 * Use **dateTimePicker** directive from our DateTimePickerModule `[(dateTimePicker)]="momentValue"`. This is the two way binding feature from AngularJS.
    Firstly, the local variable 'momentValue' would be bind to our 'dateTimePicker' directive Input and shows in the popup picker dialog.
    Once you select your new moment value and confirm it, the local variable 'momentValue' would be updated. Or if you want to deal
    with the return new moment value from our directive before update the local variable, your can separate it like this `[dateTimePicker]="momentValue" (dateTimePickerChange)="setMoment($event)"`
 * Use `[ngModel]="momentValue"` from Angular built-in FormsModule to bind the moment value to the input value. 
 * Inside `[ngModel]="momentValue | date: 'short' "`, we use the date pipe from Angular built-in Pipes to transform the Javascript Date Object to more friendly formats.
    We only use this built-in date pipe when we set the 'dateTimePicker' return object as Javascript Date Object.
 * Optional attributes:
    * **[autoClose]=" false "** --- The picker would not close or return the value by selecting a day in the calendar. 
        If setting __`[autoClose] = "true"`__, the picker would close and return the moment value by clicking a day in the calendar or confirming the time value in time slider 
        (The default value is 'false').
    * **[hourTime]=" '24' "** --- Set the hour time format (12-hour format or 24-hour format). 
        Default is '24'(24-hour format). The other choice could be '12'(12-hour format).
    * **[locale]=" 'en' "** --- This date-time-picker has robust support for internationalization. 
        (Default value is 'en'. If you want to change to French for example, just set [locale]=" 'fr' ". You can get more inform about the i18n from [MomentJS-i18n](http://momentjs.com/docs/#/i18n/)).
    * **[mode]=" 'popup' "** --- Set the date-time picker mode. Default is 'popup'. 
        The options choice could be 'popup', 'dropdown', 'inline'. 
        If you set it as 'inline', the date-time-picker would always show on your web page as a html element (In inline mode, you could set width = '250px' to make the the picker smaller or bigger. picker width are set between 250px and 300px ).
    * **[minMoment]= "'2017-09-21 19:30:00''" / [maxMoment]** -- Set minimum date / time and maximum date / time that is selectable. The format is **YYYY-MM-DD HH:mm:ss**(or **YYYY-MM-DD** for only setting date value).
        <br />
        For example, if the ideal min date and time is **September 21st, 2017 19:30**, the format string is **'2017-09-21 19:30:00'**(The default value is 'null'). 
        If you want to know whether a user selected a invalid date or time, you could use **(dateTimePickerError)="DoWhateverFn($event)"** to catch an error message.
    * **[onlyCurrentMonth]=" true "** --- Set to only show current month days in date picker. (The default value is false).
    * **[pickerType]=" 'both' "** --- You can set the default dialogType to 'date' or 'time' or 'both'. 
        When you leave it as default ([pickerType]=" 'both' "), the date-time-picker dialog would display the date calendar and time slider (you could toggle between them). 
        If you set it as 'date' or 'time', the date-time-picker dialog would only display date calendar or time slider.
    * **[position]=" 'bottom' "** --- Set the picker position in dropdown mode. This position means the picker would appear on the bottom ('top', 'left' or 'right') of your input box. 
        Default is 'bottom'. The option choice could be 'top', 'bottom', 'left', 'right'. (The default value is 'bottom').
    * **[positionOffset]=" '0%' "** --- Set the picker position offset in dropdown mode.
        <br />
        When you set your position to 'top' or 'bottom', the [positionOffset] is the percentage of your input box width and 
        it would modify the distance between the picker and the input box horizontally.
        <br />
        When you set your position to 'right' or 'left', the [positionOffset] is the percentage of your input box height and 
        it would modify the distance between the picker and the input box vertically.
        <br />
        The value could be minus like '-10%'.(The default value is '0%').
    * **[returnObject]=" 'js' "** --- You can set the return object type when you pick a moment from date-time-picker. 
        (Default value is 'js', this means the default return object type is javascript Date object. 
        The other options are: string, moment, json, array, iso and object).
    * **[showSeconds]=" true "** --- Set to show seconds slider in time picker. (The default value is false).
    * **[theme]=" '#0070ba' "** --- Set the theme color. The default color is '#0070ba'. You could provide any valid [8-Digit Hex Codes](https://css-tricks.com/8-digit-hex-codes/) to change the picker theme color. You can see the effect from the demo.
    * **[viewFormat]=" 'll' "** --- If you set your returnObject as 'string', you need to set the viewFormat. (Default value is 'll'. You can get more inform about the format from [MomentJS](http://momentjs.com/docs/#/parsing/string-format/)).
    * **Important: Do Not forget the single quote inside the double quote when you set the optional attributes string value.**
 * Emit Events
    * **(dateTimePickerChange)** --- emit a value whenever a date or time is selected.
    * **(dateTimePickerError)** --- emit a message whenever a invalid date or time is selected.
## Demo
Online demo is [here](https://danielykpan.github.io/date-time-picker/)

## License
* License: MIT

## Author
* Author: Daniel Pan
