# Quantified Self project

## Schema

Json objects, every object has a `type`.  Other fields decend from the type.

### Types

#### measure

A type of `measure` indicates a datapoint for a thing that varies over time.  For example, weight, body-fat percentage.

A `thing` field is required, indicating what is measured.  The thing strictly maps to information about units (for example)

A `source` field is optional, may indicate the device or system used to capture this measure.

A `timestamp` field is required, numeric UTC epoch time in seconds (eg, as output by `date +%s`)

A `scope` field is optional, this can be used to indicate the measure should be applied to that scope, for example "day".  If I'm capturing my subjective experience of the last day, I'll specify a scope of "day".  

A `timezone` field is optional, as a UTC offset in hours.  For example, PDT would be `-7`.  Timezone should be specified if using a scope of "day"

#### event

A type of `event` indicates a thing that happend, for example.  I drank a cup of coffee, I urinated.

`action` is a required field.  This is what happend.  It is a strict mapping to 
to a table of actions.  Examples may include "coffee" or "pee".

`quantity` is an optional field.  Some actions may require it.  Any action that requires a quantity defines it's units and meaning

`duration` is an optional field.  Some actions may require it.

`timestamp` is a required field.  UTC epoch seconds.

`timezone` is optional

#### update

A type of `update` reflects a state change.  Examples might include: "I went to sleep", changing my state from `awake` to `asleep`.   Or: "I started a low-carb diet".

`timestamp` required

`property` is required.  This is the thing that has a changing state. It defines the units and meaning of the `state` field.

`state` is required, this must be a number.  For binary states `1` means on and `0` means off.  For example `"property":"sleep", "state":0` means I woke up.  It could also be the current dosage of a drug that is used regularly.
