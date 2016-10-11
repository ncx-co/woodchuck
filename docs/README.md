There are a few major concepts:

There are 4 major levels at which data is collected: Cruise, Plot, Tree, Segment

A ["Protocol"](protocol.md) is a JSON object that tells us what the fields are
(and acceptable values for each) at each level. It also contains the merch specs.
The Protocol serves double duty by:

 * Telling the Plot Hound UI which fields to display and what the units are for each field
 * Specifying acceptable values for each field and more complicated rules about how fields relate to each other.

["CruiseData"](cruise-data.md) is a JSON object that contains lots of nested 
objects at each level and contains all the information collected during a cruise.
Note that CruiseData stores the data in the units in which it was collected.

A ["Validator"](validator.md) checks that CruiseData conforms to the Protocol.

A ["Normalizer"](normalizer.md) takes CruiseData and converts it to a canonical
data model for easy analysis by the rest of our stack.  This does things like
converting units to metric and changing things like 75% to 0.75.
