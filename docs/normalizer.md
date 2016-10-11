# Normalizer

Dealing with units is hell.  Woodchuck stores data in the units in which it was
collected in CruiseData, but for the purpose of actually processing it and
converting it to other formats, it is useful to use a "Normalizer" NodeJS script
which will convert all the units to metric (and percents to 0-1, etc).
