# Glossary

This glossary provides more detailed explanations on many terms used in this manual.

## Data Types

There are two main datatypes in Mindustry; numbers and Objects.

### number

A number. Can be nagative or positive, have decimals or not, and can represent true (anything above 0) or false (0) values. Null is also represented as 0.

Some instructions can only accept whole numbers, so it is indicated accordingly in this manual.

### String

An Object that represents text enclosed in quotes, e.g. `"hello mindustry"`

### Building

An Object that represents a physical Building in a world. 

**This is different from a Block**; a Block is simply a type of Building, but a Building is a tangible Block - as in, it has health, interacts with power and items, etc.

Essentially, **a Building is a Block that physically exists in a world.**

For example, the `getlink` instruction will return a *Building* Object, which you can get information about using `sensor`.

### Unit

An Object that represents a Unit in a world, including the player.

For example, the `ubind` instruction will set a processor variable `@unit` to a Unit Object representing a bound unit.

## Parameter Types

These are like data types, but only work as parameters for instructions, and are not returned by any instruction.

### BuildingType

A type of Building. Starts with `@`.

Within the game's code, this is better referred to as "Block". However, for the sake of readability in this manual, we will call it BuildingType. *See [###Building] for an explanation on Building vs. Block.*

Unlike Items and Liquids, you cannot use this in `sensor`. However, you can use `@type` in `sensor`, and compare against it with `jump`.

Example: `@scatter`

### UnitType

A type of Unit. Starts with `@`.

Example: `@toxipid`

*A full list is shown under the pencil button in the "Unit Bind" instruction block.*

<img src="/wiki-testing/images/misc/logic-glossary-unitType-unitBind.png">

### Senseable

An Item, Liquid, or Building or Unit property that can be "sensed" by `sensor`. Starts with `@`.

Examples: `@scrap`, `@slag`, `@totalAmmo`

*A full list is shown under the pencil button in the "Sensor" instruction block.*

<img src="/wiki-testing/images/misc/logic-glossary-senseable-sensor.png">

### Target

A trait to filter a unit or block target by. Primarily used in `radar`, `uradar`, and `ulocate`. `radar` and `uradar` have the same Targets, but `uradar` is diferent, since it looks for Buildings.

*A full list is shown by pressing parameters after "target" in `radar` and `uradar`, or "find" and "type" in `uradar`.*

<img src="/wiki-testing/images/misc/logic-glossary-target-radar.png">

### Op

A mathematical operation. *This is different from the `op` instruction.* 

*A full list is shown under the "+" button in the "Operation" instruction block.*

<img src="/wiki-testing/images/misc/logic-glossary-op-operation.png">

For the more complex ones, you can Google "<operation name\> Java math".

### Comp

A comparison. Primarily used in the `jump` instruction when comparing two values. `always` will return true no matter what, so it will always cause a jump.

*A full list is shown under the comparison button in the "Jump" instruction block.*

<img src="/wiki-testing/images/misc/logic-glossary-comp-jump.png">