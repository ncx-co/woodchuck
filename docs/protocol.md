# Protocol specification

The Protocol is really at the heart of all this.  At each level, it specifies
the fields and various characteristics of each.

## Protocol keywords

At each level, there are a few reserved keywords for fields that correspond to
aspects of the Woodchuck data model.  These are things like "age" or "species"
and they have particular acceptable data types.  We can add additional
arbitrary fields, but they can't be named with a reserved keyword.

The fields below are used by Woodchuck internally as part of the nested
CruiseData structure to describe relationships between objects.

Reserved keywords at each level are:

* CRUISE
  * version - string
  * id - integer
  * label - string
  * bounds - geojson-multipolygon
  * contactEmail - email
  * notes - string
  * timestamp - datetime
  * plots - list of PLOT
  * protocol - a PROTOCOL
* PLOT
  * id - int
  * label - string or numeric
  * sampling - sampling
  * subplots - list of PLOT (but in the PROTOCOL object, this will be an integer of the number of subplots).
  * targetLocation - geojson-point
  * measuredLocation - geojson-point
  * measuredLocAccuracy - float
  * notes - string
  * timestamp - datetime
  * cruiser - email address or string
  * trees - list of TREE
* TREE
  * expansion - float
  * species - string
  * speciesGroup - species-group
  * segments - list of SEGMENT
  * age - integer
  * crownRatio - percent
  * notes - string
  * count - integer
  * height/diameter - dictionary of height/diameter pairs
  * created - datetime
  * edited - datetime
* SEGMENT
  * startHeight - numeric
  * stopHeight - numeric
  * product - string
  * percentage - percent

There are also keywords for SUBPLOT, SUBPLOT_TREE, SUBPLOT_SEGMENT levels which
are exactly what they sound like.

Each level also has a reserved "custom-validate" keyword that can optionally
map to a custom validation function.  This enables validation for fields that
depend on each other in that level (for example, make sure you can't call 
"pulp" on a cherry tree). 

You don't have to specify all these fields in every protocol.  Fields that are
excluded simply aren't included in the data collection UI or the CruiseData object.

## Field Options

Each field has a few characteristics that can be specified:

* name - what the field is called.  Special things happen if this is one of the reserved keywords
  * a string
* displayName - if present it will be used instead of name for display purposes
  * a string
* required
  * true/false
* type - what sort of data this is
  * Geojson options: geojson-point, geojson-multipolygon
  * Numeric options: int, float
  * Other options: boolean, string, email, datetime
  * Special SilviaTerra options: sampling, species-group, height-diameter
  * Image options: not dealing with this for now.  Maybe one day.
* displayName - if present it will be used instead of name for display purposes
* units
  * inches, feet, 8' log, 16' log, 32' log, centimeters, meters, years, percent 
* default - some value.  Defaults to null
* options - a list of acceptable options or null
* uiOptions - a list of options to display in the dropdown or null.  If null, defaults to options if it exists
* uiDisplay - should this field be displayed in the UI?  Useful for fields that we'd like to get data for but don't want the user to enter (things like "time_collected" which are automatically filled in by the app)
  * true/false
* uiWidget - how data will be entered.  Defaults listed below.  If ui-options is specified, we'll also have a select menu that drops down as well (like in the current PH)
  * checkbox - boolean
  * input type=number - int, float, height-diameter
  * input type=text - string
  * textarea - not default for any type
  * select - default if "options" specified
  * tabbedSelect

### Specialized field options

#### For uiWidget == tabbedSelect

 * uiTabs - list (in order) of tabs, e.g. ['common', 'all']
 * uiTabOptions - dictionary of values for each tab, e.g. {'common': ['white oak', ...], 'all': [ ... ]}

#### NUMERIC ONLY 

(int, float, height-diameter [when there is one fixed value])

* ltWarn - warn if less than this value
* lteWarn - less than or equal
* ltError - throw an error if less than
* lteError - ditto
* gtWarn - ditto
* gteWarn - ditto
* gtError - ditto
* gteError - ditto

#### SAMPLING ONLY

* expansionArea - "acre" or "hectare"
* expansionFunctions - dictionary of {**sampling_method**: **function**}
* Note that the function receives a TREE object and returns a trees-per-**expansion-area**

#### HEIGHT-DIAMETER ONLY

* height - the fixed height
* diameter - the fixed diameter (note that both cannot be fixed at once)
* heightUnits - units for height
* diameterUnits - units for diameter

#### SPECIES-GROUP ONLY

* groups - a dictionary of {**group_name**: **species-ids-or-CATCHALL**}
