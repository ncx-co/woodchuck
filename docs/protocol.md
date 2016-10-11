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
  * stand-name - string
  * bounds - geojson-multipolygon
  * contact-email - email
  * notes - string
  * cruise-date - datetime
  * plots - list of PLOT
  * protocol - a PROTOCOL
* PLOT
  * id - int
  * label - string or numeric
  * sampling - sampling
  * subplots - list of PLOT (but in the PROTOCOL object, this will be an integer of the number of subplots).
  * target-loc - geojson-point
  * actual-loc - geojson-point
  * actual-loc-accuracy - float
  * notes - string
  * time-collected - datetime
  * time-last-edited - datetime
  * cruiser - email address or string
  * trees - list of TREE
* TREE
  * expansion - float
  * species - string
  * species-group - species-group
  * segments - list of SEGMENT
  * age - integer
  * crown_ratio - percent
  * notes - string
  * count - integer
  * height/diameter - dictionary of height/diameter pairs
* SEGMENT
  * start_height - numeric
  * stop_height - numeric
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
* required
  * true/false
* type - what sort of data this is
  * Geojson options: geojson-point, geojson-multipolygon
  * Numeric options: int, float
  * Other options: boolean, string, email, datetime
  * Special SilviaTerra options: sampling, species-group, height-diameter
  * Image options: not dealing with this for now.  Maybe one day.
* units
  * inches, feet, 8' log, 16' log, 32' log, centimeters, meters, years, percent 
* default - some value.  Defaults to null
* options - a list of acceptable options or null
* ui-options - a list of options to display in the dropdown or null.  If null, defaults to options if it exists
* ui-display - should this field be displayed in the UI?  Useful for fields that we'd like to get data for but don't want the user to enter (things like "time_collected" which are automatically filled in by the app)
  * true/false
* ui-widget - how data will be entered.  Defaults listed below.  If ui-options is specified, we'll also have a select menu that drops down as well (like in the current PH)
  * checkbox - boolean
  * input type=number - int, float, height-diameter
  * input type=text - string
  * textarea - not default for any type
  * select - default if "options" specified

### Specialized field options

#### NUMERIC ONLY 

(int, float, height-diameter [when there is one fixed value])

* lt-warn - warn if less than this value
* lte-warn - less than or equal
* lt-error - throw an error if less than
* lte-error - ditto
* gt-warn - ditto
* gte-warn - ditto
* gt-error - ditto
* gte-error - ditto

#### SAMPLING ONLY

* expansion-area - "acre" or "hectare"
* expansion-functions - dictionary of {**sampling_method**: **function**}
* Note that the function receives a TREE object and returns a trees-per-**expansion-area**

#### HEIGHT-DIAMETER ONLY

* height - the fixed height
* diameter - the fixed diameter (note that both cannot be fixed at once)
* height-units - units for height
* diameter-units - units for diameter

#### SPECIES-GROUP ONLY

* groups - a dictionary of {**group_name**: **species-ids-or-CATCHALL**}
