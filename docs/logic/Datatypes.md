# Data and Parameter Types

A datatype is what its name suggests, a type of data. This outlines the types of variables (or values) you can give to or get from an instruction. "Parameter only" means that it can only be used as a parameter for an instruction, and is not returned by one.

### bool

A __bool__ean. Can either be true or false, 1 or 0. 

### int

An __int__eger; a **whole** number with no decimal.

### double

A __Double__ Precision Floating Point; a number with an optional decimal.

### Unit

A type of Object that represents a __unit__, including the player.

### Building

A type of Object that represents a building.

### String

A string enclosed in quotes, e.g. `"hello mindustry"`

### Val

A variable to hold or read a __val__ue from. This can reference any variable of any type. For an instruction that can write to a variable, this is it's "output".

### Sensable

**Parameter only.**

An Item, Liquid, or Building property that can be __sense__d by `sensor` and similar instructions. *A full list is shown when the pencil button in the "Sensor" instruction is pressed.*

<img src="/wiki-testing/images/misc/logic-datatypes-senseable-sensor.png">

This also involves **Unit and Building names**, such as `@flare` or `@smelter`, but those cannot be used with `sensor`. You can instead check those against the `@type` Senseable, which you *can* use with `sensor`.

### Target

**Parameter only.**

A trait to filter a unit or block __target__ by. Used primarily in `radar` and similar instructions. *A full list is shown when an argument after "target" is pressed in the "Radar" instruction.*

<img src="/wiki-testing/images/misc/logic-datatypes-target-sensor.png">

### Op

**Parameter only.**

A mathematical __op__eration. Keep in mind that this is different from the `op` instruction. *A full list can be found when pressing the "+" or operation button in the "Operation" instruction block.*

<img src="/wiki-testing/images/misc/logic-datatypes-op-operation.png">

For the more complex ones, you can Google "\<operation name\> Java math".

### Comp

**Parameter only.**

A __comp__arison. Primarily used in the `jump` instruction when comparing two values. *A full list can be found when pressing the "+" or operation button in the "Jump" instruction block.*

<img src="/wiki-testing/images/misc/logic-datatypes-comp-jump.png">