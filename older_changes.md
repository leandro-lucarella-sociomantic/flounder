Older changes
=============

This is truncated from the readme file to keep down the size

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


0.4.5
-----

+ [default] the default `data` is now `[]` in case of initially empty dropdowns
+ [deps] changed how microbe is required and installed


0.4.4
-----

+ [default] adjusted handling of numbers as values
+ [default] unless specified, the default on multiple enabled flounders is nothing selected
+ [build] moved reconfigure `reconfigure is depreciated from the api and will be removed in 0.5.0`
+ [build] modified data type detection
+ [build] selectDataOverride now clears the unused option tags
+ [api] reconfigure is depreciated to an internal function.  rebuild now handles both use cases
+ [api] modified native select rebuilt values
+ [api] rebuild `rebuilt`
+ [api] `destroy` now removes placeholder
+ [api] added css for loading and failed loading
+ [utils] added `removeAllChildren`


0.4.3
-----

+ [tests] added flounder tests
+ [test] added constructor tests
+ [flounder] added read-only version number
+ [flounder] fixed a bug affecting defaultValues with an index 0
+ [default] multiTag flounders now get a default placeholder if not supplied
+ [version] added `src/core/version.js`
+ [version] added `scripts/version_bump.js`
+ [search] search is now initialized only when it will be used
+ [build] added `___isBound` to `this` bound functions for clarity and testing
+ [build] improves multiTag support for data that's initially supplied as a string


0.4.2
-----

+ [api] added `buildFromUrl`
+ [api] added `loadDataFromUrl`
+ [api] added `onFirstTouch`
+ [build] select boxes that have no options as targets now use data
+ [default] the default option when not specified if the data set is empty is the default placeholder
+ [default] changed the default value priority
+ [flounder] changed sortData to not break with strings
+ [flounder] microbe and promise now required to build
+ [config] added `selectDataOverride` for empty select boxes


0.4.1
-----

+ [build] `setSelectValue` is now bound to flounder again


0.4.0
-----

+ [api] changed language of all contextual statements `setIndex` becomes `setByIndex`, etc
+ [config] added `onComponentWillUnmount`
+ [config] added try/catch to all config functions
+ [build] placeholder will only be added to selectboxes that do not have a first option with '' as a value.  otherwise the text will be changed to the new placeholder value.
+ [build] fixed bugs in construction when using a selectbox as a target
+ [utils] tweaked `addClass`


0.3.2
-----

+ [api] added clickText, disableText, enableText, and setText
+ [api] correctly bound this to mapped set and click functions


0.3.1
-----

+ [search] fixed a bug in value length detection
+ [defaults] removed defaultTextIndent.  this can be handled by css
+ [api] added disableIndex and disableValue
+ [api] added enableIndex and enableValue


0.3.0
-----

+ [api] getOption is now getData
+ [api] getData now provides all data when no number is given
+ [api] getSelectedOptions is now getSelected
+ [api] rebuildSelect is now rebuild
+ [api] added clickIndex and clickValue
+ [api] added props
+ [api] added reconfigure
+ [default] multipleTags is now false by default
+ [search] added Sole (a ROVer derivitive) for fuzzy search


0.2.9
-----

+ checkClickTarget now fails better


0.2.8
-----

+ structure style tweaked
+ internal abstractions
+ fixed a multi-tag event leak


0.2.7
-----

+ fixed a destroy event leak
+ fixed a selectbox event leak
+ added "destroy all" demo button
+ changed flounder <-> element references in react
+ $ now sets flounder as 'flounder' with data
+ µ now sets flounder as 'flounder' with set
+ flounder now detects, destroys, and re-instantiates with the new options if it is given an element that already has a flounder


0.2.6
-----

+ split file structure
+ removed the checks for 0 length flounder creation objects.  If there is nothing to render, flounder will just render nothing
+ onOpen and onClose will now not fire until flounder is set up
+ destroy now preserves the container it was built in
+ better checks for target


0.2.5
-----

+ fixed removeClass
+ added qunit
+ added nightmare testing


0.2.4
-----

+ updated default defaults
+ added better error message for 0 length targets
+ now allows for native selection by letter
+ flounder leaves references to itself on .flounder and the original target
+ destroy cleans up references
+ selection after a search clears the search field
+ defaults are correctly determined inside header based flounders
+ removeClass fix
+ search opens properly with keypresses
+ hidden search options no longer appear on keypress
+ search input now clears on up/down navigation
+ space in a search field no longer closes the field
+ selected field gets out of the way on search


0.2.3
-----

+ simplified how keypresses are handled
+ fixed first keypress bug (#23)
+ updated examples and example pics
+ updated default css
+ added additional package keywords
+ updates to readme
+ fixed a bug based on select tags NOT being arrays
+ fixed a bug that stopped data from being passed from the config object
+ brought back _slice and the constructor position


0.2.2
-----

+ improvements in defaults
+ react improvements
+ debug mode added to demo page
+ added better aria support
+ programmatically setting value or index no longer triggers onSelect
+ changed rebuildOptions to rebuildSelect for clarity
+ changed this.options to this.data for clarity
+ added the ability to build sections with headers
+ refactored some build functions


0.2.1
-----

+ added setValue to API
+ added disable classes to the css
+ internal fixes
+ added hasClass
+ changed setValueClick
+ added disable to API
+ added classes config object
+ broke up the main flounder file
+ readme updates


0.2.0
-----

+ user callbacks now keep their name internally for dynamic changes
+ some users callback now give the array of selected values (see examples)
+ _default is now defaultValue
+ the constructor now accepts µ and $ objects and returns an array of flounders
+ a call to the constructor without and arguments now returns the constructor
+ added getSelectedValues() to API
+ added the ability to give options unique classes
+ added wrapper to the class options
+ changed the flounder class option from container to flounder
+ restructured folders and files


0.1.5
-----

+ added rebuildOption and getOptions
+ added dynamic options
+ added getSelected
+ fixes in keypress handlers
+ added support for AMD loaders
+ added a jquery plugin wrapper
+ added a microbe plugin wrapper
+ fixed multi-select with dynamic options


0.1.4
-----

+ flounder now detroys itself properly


0.1.3
-----

+ fresh opening a menu now scrolls to selected (non-multiple)
+ events in setValue are now normalized


0.1.0
-----

+ all callback functions all start with `on` for clarity (`init` becomes `onInit`)