Flounder.js 0.6.3
=================

[![Flounder build status](https://travis-ci.org/sociomantic-tsunami/flounder.svg)](https://travis-ci.org)

(for modern browsers and ie9+)

Flounder is a styled select box replacement aimed at being easily configurable while conforming to native functionality and accessibility standards.

```js
// npm
require('flounder');

// es6
import Flounder from 'flounder';
```


Usage
=====

Flounder can be used in vanilla js or with [react](http://facebook.github.io/react/), [requirejs](http://requirejs.org/), [jquery](http://jquery.com/), and [microbe](https://github.com/sociomantic-tsunami/microbe).

```js
// vanilla
new Flounder( target, configOptions );

// react
ReactDOM.render( React.createElement( FlounderReact, configOptions ), target );

// react (JSX)
React.render( <FlounderReact option1="" option2="">, target );

// react has some caveats.  If you want to use react flounder, you should
// build it from the source file.  ./dist/flounder.react.js is so
// large because it already has a copy of react included.  Additionally,
// react flounder can only be attached to a container, and not an
// INPUT or SELECT

// requirejs
requirejs( [ 'flounder' ], function( Flounder )
{
    new Flounder( target, configOptions );
} );

// jQuery plugin
$( '.example--class' ).flounder( configOptions );

// microbe plugin
µ( '.example--class' ).flounder( configOptions )
```

Flounder also adds a reference of itself to its target element.  So if you lose the reference, you can just grab it from the element again
```js
document.querySelector( '#vanilla--select' ).flounder.destroy()
```


###Target options

Flounder's target is quite flexible.

you can give it an element:

```js
new Flounder( document.getElementsByTagName( 'input--el' )[0], options );
```

an array:

```js
new Flounder( [ el1, el2, el3 ], options );
```

an HTML collection:

```js
new Flounder( document.getElementsByTagName( 'input' ), options );
```

a jQuery object:

```js
new Flounder( $( 'input' ), options );
```

a microbe:

```js
new Flounder( µ( 'input' ), options );
```

or, just a selector string:

```js
new Flounder( 'input', options );
```

If flounder is fed an element that already has a flounder, it will destroy it and re initialize it with the new options.


###Available config options

```js
{
    allowHTML               : false,
    classes                 : {
        flounder    : 'class--to--give--the--main--flounder--element',
        hidden      : 'class--to--denote--hidden',
        selected    : 'class--to--denote--selected--option',
        wrapper     : 'additional--class--to--give--the--wrapper'
    },
    data                    : dataObject,
    defaultValue            : defaultValue,
    defaultIndex            : defaultIndex,
    keepChangesOnDestroy    : false,
    multiple                : false,
    multipleTags            : false,
    multipleMessage         : '(Multiple Items Selected)',
    onClose                 : function( e, valueArray ){},
    onComponentDidMount     : function(){},
    onComponentWillUnmount  : function(){},
    onFirstTouch            : function( e ){},
    onInit                  : function(){},
    onOpen                  : function( e, valueArray ){},
    onSelect                : function( e, valueArray ){}
    placeholder             : 'Please choose an option',
    search                  : false,
    selectDataOverride      : false
}
```

+ `allowHTML`- (boolean) Renders the data text as HTML.  With this option enabled, any api call that must compare text will need the exact html in order to be a match

+ `classes`- (object) Contains configurable classes for various elements.  The are additional classes, not replacement classes.

+ `data` - (array) select box options to build in the select box.  Can be organized various ways

+ `defaultValue` - (string) Sets the default value to the passed value but only if it matches one of the select box options. Multi-tag select boxes only support placeholders

+ `defaultIndex` - (number) Sets the default option to the passed index but only if it exists.  This overrides defaultValue. Multi-tag select boxes only support placeholders.

+ `keepChangesOnDestroy` - (boolean) Determines whether on destroy the old element is restored, or the flounder changes to the select box are kept.  This only applies when the initial element for flounder is a select box

+ `multiple` - (boolean) Determines whether it is a multi-select box or single

+ `multipleTags` - (boolean) Determines how a multi-select box is displayed

+ `multipleMessage` - (string) If there are no tags, this is the message that will be displayed in the selected area when there are multiple options selected

+ `onClose` - (function) Triggered when the selectbox is closed

+ `onComponentDidMount` - (function) Triggered when the selectbox is finished building

+ `onComponentWillUnmount` - (function) Triggered right before flounder is removed from the dom

+ `onFirstTouch` - (function) Triggered the first time flounder is interacted with. An example usage would be calling an api for a list of data to populate a drop down, but waiting to see if the user interacts with it

+ `onInit` - (function) Triggered when the selectbox is initiated, but before it's built

+ `onOpen` - (function) Triggered when the selectbox is opened

+ `onSelect` - (function) Triggered when an option selectbox is closed

+ `placeholder` - (string) Builds a blank option with the placeholder text that is selected by default.  This overrides defaultIndex

+ `search` - (boolean) Determines whether the select box is searchable

+ `selectDataOverride` - (boolean) If this is true, flounder will ignore sleect box options tags and just apply the passed data

*IMPORTANT DEFAULT PRIORITY*
```
1 ) placeholder
2 ) defaultIndex
3 ) defaultValue
4 ) whatever is at index 0
```

Building the select box
=======================

selectbox data must be passed as an array of objects

```js
[
    {
        text        : 'probably the string you want to see',
        value       : 'return value',
        description : 'a longer description of this element', // optional, string
        extraClass  : 'extra--classname',                   // optional, string
        disabled    : false                                 // optional, boolean
    },
    ...
]
```

or a simple array of strings. The passed text will be both the text and the value.  There would be no description in this case

```js
[
    'value 1',
    'value 2',
    'value 3',
    ...
]
```

or, if you want section headers.  You can even add uncatagorized things intermingled

```js
[
    {
        header : header1,
        data : [ option1, option2, ... ]
    },
    {
        text        : 'probably the string you want to see',
        value       : 'return value',
        description : 'a longer description of this element'
    },
    {
        header : header2,
        data : [ option1, option2, ... ]
    },
    ...
]

```

all extra properties passed in an option that are not shown here will be added as data attributes for the sake of reference later.  The data can be accessed in the init (before building) as this.data if they need reformatting or filtering.


API
===

These functions are intended for use in the user provided event callbacks

```js
this.buildFromUrl( url, callback )
this.clickByIndex( index, multiple )
this.clickByText( text, multiple )
this.clickByValue( value, multiple )
this.deselectAll()
this.destroy()
this.disable( bool )
this.disableByIndex( index )
this.disableByText( text )
this.disableByValue( value )
this.enableByIndex( index )
this.enableByText( text )
this.enableByValue( value )
this.getData( [ num ] )
this.getSelected()
this.getSelectedValues()
this.loadDataFromUrl( url, callback )
this.props
this.rebuild( [ data, props ] )
this.refs
this.setByIndex( index, multiple )
this.setByText( text, multiple )
this.setByValue( value, multiple )
```

+ `buildFromUrl( url, callback )` loads data from a remote address, passes it to a callback, then builds the flounder object

+ `clickByIndex( index, multiple )` sets the item with the passed index as selected.  If multiple is true and it is a multi-select box, it is selected additionally.  Otherwise it's selected instead.  This accepts arrays as well.  Without multiple equaling true it will only select the last option. This fires the onClick event.  A negative index will start counting from the end.

+ `clickByText( text, multiple )` sets the item with the passed text as selected.  If multiple is true and it is a multi-select box, it is selected additionally.  Otherwise it's selected instead. This accepts arrays as well.  Without multiple equaling true it will only select the last option. This fires the onClick event

+ `clickByValue( value, multiple )` sets the item with the passed value as selected.  If multiple is true and it is a multi-select box, it is selected additionally.  Otherwise it's selected instead. This accepts arrays as well.  Without multiple equaling true it will only select the last option. This fires the onClick event

+ `deselectAll()` deselects all data

+ `destroy()` removes event listeners, then flounder.  this will return the element to it's original state

+ `disable( bool )` disables or reenables flounder

+ `disableByIndex( index )` disables a flounder option by index.  A negative index will start counting from the end.

+ `disableByText( text )` disables a flounder option by text

+ `disableByValue( value )` disables a flounder option by value

+ `enableByIndex( index )` enables a flounder option by index. A negative index will start counting from the end.

+ `enableByText( text )` enables a flounder option by text

+ `enableByValue( value )` enables a flounder option by value

+ `getData( [ num ] )` returns the option element and the div element at a specified index as an object `{ option : option element, div : div element }`. If no number is given, it will return all data.

+ `getSelected()` returns the currently selected option tags in an array

+ `getSelectedValues()` returns the currently selected values in an array

+ `loadDataFromUrl( url, callback )` loads data from a remote address and returns it to a passed callback.

+ `props` the props set in the initial constructor

+ `rebuild( data, props )` rebuilds the select box options with new or altered data.  If props are set, this completely rebuilds flounder

+ `refs` contains references to all flounder elements

+ `setByIndex( index, multiple )` sets the item with the passed index as selected.  If multiple is true and it is a multi-select box, it is selected additionally.  Otherwise it's selected instead.  This accepts arrays as well.  Without multiple equaling true it will only select the last option. This does not fire the onClick event.  A negative index will start counting from the end.

+ `setByText( text, multiple )` sets the item with the passed text as selected.  If multiple is true and it is a multi-select box, it is selected additionally.  Otherwise it's selected instead. This accepts arrays as well.  Without multiple equaling true it will only select the last option. This does not fire the onClick event.

+ `setByValue( value, multiple )` sets the item with the passed value as selected.  If multiple is true and it is a multi-select box, it is selected additionally.  Otherwise it's selected instead. This accepts arrays as well.  Without multiple equaling true it will only select the last option. This does not fire the onClick event.


Contributing
============

We gladly accept and review any pull-requests. Feel free! :heart:

Otherwise, if you just want to talk, we are very easy to get a hold of!

+ Slack:          [flounder.slack.com](https://flounder.slack.com)
+ Email:          [flounder@knoblau.ch](mailto:flounder@knoblau.ch)
+ Web:            <a href="http://flounderjs.com/" target="_blank">http://flounderjs.com/</a>
+ Git:            <a href="https://github.com/sociomantic-tsunami/flounder/" target="_blank">https://github.com/sociomantic-tsunami/flounder/</a>



This project adheres to the [Contributor Covenant](http://contributor-covenant.org/). By participating, you are expected to honor this code.

[Flounder - Code of Conduct](https://github.com/sociomantic-tsunami/flounder/blob/master/CODE_OF_CONDUCT.md)

Need to report something? [flounder@knoblau.ch](mailto:flounder@knoblau.ch)


Example
========

Given the example data:

```js

    var data = [
        {
            cssClass    : 'select-filters',
            id          : 'All',
            isTaxonomy  : true,
            text        : 'All'
        },
        {
            cssClass    : 'category',
            id          : 'category',
            isTaxonomy  : true,
            text        : 'Categories'
        },
        {
            cssClass    : 'tag',
            id          : 'tag',
            isTaxonomy  : true,
            text        : 'Tags'
        }
    ];
```

a vanilla flounder

flounder can be attached to basically anything

```js

    new flounder( document.getElementById( 'example' ), {
        placeholder         : 'placeholders!',

        onInit              : function()
        {
            var res = [];
            data.forEach( function( dataObj )
            {
                res.push( {
                    text        : dataObj.text,
                    value       : dataObj.id
                } );
            } );

            this.data = res;
        }
    } );
```

a react flounder

react flounder can only be attached to container elements (div, span, etc)


```js

    ReactDOM.render( React.createElement( FlounderReact, {
        placeholder         : 'placeholders!',

        onInit              : function()
        {
            var res = [];
            data.forEach( function( dataObj )
            {
                res.push( {
                    text        : dataObj.text,
                    value       : dataObj.id
                } );
            } );

            this.data = res;
        } } ), document.getElementById( 'example' )
    );
```


The result of either of these is shown here (only styled with the structural css)

closed

![closed](https://cloud.githubusercontent.com/assets/4903570/11898709/4ee0059a-a59a-11e5-83e9-d1d2e0dbe46e.png)

open menu

![open menu](https://cloud.githubusercontent.com/assets/4903570/11898721/629c0cbe-a59a-11e5-95ed-82f0ff557bde.png)

1 selected

![1 selected](https://cloud.githubusercontent.com/assets/4903570/11898730/708eaa02-a59a-11e5-930a-cccbc22f0401.png)

See more examples on the [demo page](./demo/index.html)


Change Log
==========

0.6.3
-----

+ tests
    + add test "blurOpenedDropdown" to cover fix

+ events
    + fixed addPlaceholder method for blur of opened dropdown


0.6.2
-----

+ tests
    + version test completed
    + default priority fixed

+ default
    + priority fixed
    + null default bug fixed


0.6.1
-----

+ tests
    + utils tests completed

+ demo
    + updates and cleanup

+ documentation
    + repo url update
    + general updates and clean up


0.6.0
-----

+ api
    + added allowHTML


0.5.0
-----

+ events
    + added `setSelectValue` to search keyup
    + mobile safari no longer selects things all by itself
    + fixed a bug with incrementing and firefox
    + added a blur event to catch mobile selection
    + search inputs now correctly display the selected values on blur
    + fixed placeholder logic

+ search
    + adjusted search weights
    + descriptions are now properly searchable
    + multiple `setValue` calls taken out

+ build
    + multiple is now automatically  enabled with `multipleTags : true`
    + search works in react
    + search is now mandataory enabled in a multiTag box (#7)
    + React now sets platform and isIos
    + original elements are now restored on destroy in the case of a select as a target
    + added `keepChangesOnDestroy` as an available prop

+ demo
    + fixed minor issues on the demo
    + changed debug button

+ default
    + refactored defaults functions into `./defaults.js`

+ api
    + added the ability to use negative indexes in api calls
    + removed querySelector from the api calls
    + default is now only applied after rebuild if there is nothing with the value left in the dropdown
    + the placeholder now deselects when choosing the first option (multiple)

+ flounder
    + slowly removing things that are not needed from the main object for the sake of a clearer api later

+ utils
    + no longer merged onto the main flounder object



Older Changes
=============

To keep the length of this file down, [older changes are here](./older_changes.md)
