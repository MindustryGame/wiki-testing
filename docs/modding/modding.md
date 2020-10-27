
# Modding

Mindustry mods are simply directories of assests. There are many ways to use the modding API, depending on exactly what you want to do, and how far you're willing to go to do it.

You could just resprite existing game content, you can create new game content with the simpler Json API (which is the main focus of this documentation), you can add custom sounds (or reuse existing ones). It's possible to add maps to campaign mode, and add scripts to program special behavior into your mod, like custom effects. 

Sharing your mod is as simple as giving someone your project directory; mods are also cross platfrom to any platform that supports them. Realistically speaking you'll want to use [GitHub](#github), you should also checkout the Example Mod repository on GitHub: <https://github.com/Anuken/ExampleMod>

To make mods all you really need is any computer with a text editor.



## Directory Structure

Your project directory should look something like this:

    project
    ├── mod.json
    ├── content
    │   ├── items
    │   ├── blocks
    │   ├── mechs
    │   ├── liquids
    │   ├── units
    │   └── zones
    ├── maps
    ├── bundles
    ├── sounds
    ├── schematics
    ├── scripts
    ├── sprites-override
    └── sprites

-   [`mod.json`](#modjson) (required) metadata file for your mod,
-   `content/*` directories for game [Content](#content),
-   `maps/` directory for [Zone](#zone) maps,
-   `bundles/` directory for [Bundles](#bundles),
-   `sounds/` directory for [Sound](#sound) files,
-   `schematics/` directory for [Schematic](#schematic) files,
-   `scripts/` directory for [Scripts](#scripts),
-   `sprites-override/` [Sprites](#sprites) directory for overriding ingame content,
-   `sprites/` [Sprites](#sprites) directory for your content,

Every platform has a different user application data directory, and this is where your mods should be placed:

-   Linux: `~/.local/share/Mindustry/mods/`
-   Steam: `steam/steamapps/common/Mindustry/mods/`
-   Windows: `%appdata%/Mindustry/mods/`
-   Apple: `~/Library/Application Support/Mindustry/mods/`

*Note that your filenames should be lowercased and hyphen separated:*

-   correct: `my-custom-block.json`
-   incorrect: `My Custom Block.json`



## Hjson

Mindustry uses [Hjson](https://hjson.org/), which for anyone who knows Json, is simply a superset of the very popular serialization language known as [Json](https://en.wikipedia.org/wiki/JSON). &#x2013; This means that any valid Json will work, but you get extra useful stuff:

    # single line comment
    
    // single line comment
    
    /* multiline
    comment */
    
    key1: single line string
    
    key2:
    '''
    multiline
    string
    '''
    
    key3: [ value 1
            value 2
            value 3 ]
    
    key4: { key1: string
            key2: 0 }

If you don't know any of those words. &#x2013; A serialization language, is simply a language which encodes information for a program, and *encode* means to translate informantion from one form to another, and in this case, to translate text into Java data structures.



## `mod.json`

At the root of your project directory, you must have a `mod.json` which defines the basic metadata for your project. This file can also be (optionally) named `mod.hjson` to potentially help your text editor pick better syntax highlighting.

    name: Mod Name
    displayName: Mod [red]Name[]
    author: Yourself
    description: This is a useless description.
    version: "1.0"
    minGameVersion: "100.3"
    dependencies: [ ]

-   `name` will be used to reference to your mod, so name it carefully;
-   `displayName` this will be used as a display name for the UI, which you can use to add formatting to said name;
-   `description` of the mod will be rendered in the ingame mod manager, so keep it short and to the point;
-   `dependencies` is optional, if you want to know more about that, go to the [dependencies](#dependencies) section;
-   `minGameVersion` is the minimum build version of the game.



## Content

At the root of your project directory you can have a `content/` directory, and this is where all the Json/Hjson data goes. Inside of `content/` you have subdirectories for the various kinds of content, these are the current common ones:

-   `content/items/` for [items](#item), like `copper` and `surge-alloy`;
-   `content/blocks/` for [blocks](#block), like turrets and floors;
-   `content/mechs/` for [mechs](#mech), like `tau` and `glaive`;
-   `content/liquids/` for [liquids](#liquid), like `water` and `slag`;
-   `content/units/` for flying or ground [units](#unittype), like `reaper` and `dagger`;
-   `content/zones/` for [zones](#zone), configuration of campaign maps.

Note that each one of these subdirectories needs a specific content type. The filenames of these files is important, because the stem name of your path *(filename without the extension)* is used to reference it.

Furthermore the files within these `content/<content-type>/*` directories may be arbitrarly nested into other sub-directories of any name, to help you organize them further, for example:

-   `content/items/metals/iron.hjson`, which would respectively create an item named `iron`.

The content of these files will tend to look something like this:

    type: TypeOfThing
    name: Name Of Thing
    description: Description of thing.
    # ... more fields here ...

|field|type|notes|
|---|---|---|
|type|String|Content type of this object.|
|name|String|Displayed name of content.|
|description|String|Displayed description of content.|

Other fields included will be the fields of the type itself.



## Types

Types have numerous fields, but the important one is `type`; this is a special field used by the content parser, that changes which type your object is. *A `Router` type can't be a `Turret` type*, as they're just completely different.

Types *extend* each other, so if `MissileBulletType` extends `BasicBulletType`, you'll have access to all the fields of `BasicBulletType` inside of `MissileBulletType` like `damage`, `lifetime` and `speed`. Fields are case sensitive: `hitSize =/= hitsize`.

What you can expect a field to do is up to the specific type, some types do absolutely nothing with their fields, and work mostly as a base types will extend from. One such type is `Block`.

`type` can be refer to the actual type field of the object. A type may also refer to other things like `float` is a type so it means you can type `0.3` in a field.

Here you can see, the type of the top level object is `Revenant`, but the type of the `bullet` is `BulletType` so you can use `MissileBulletType`, because `MissileBulletType` extends `BulletType`.

    type: Revenant
    weapon: {
      bullet: {
        type: MissileBulletType
        damage: 9000
      }
    }



## Tech Tree

Much like `type` there exist another magical field known as `research` which can go at the root of any block object to put it in the techtree.

    research: duo

This would put your block after `duo` in the techtree, and to put it after your own mods block you would write your `<block-name>`, a mod name prefix is only required if you're using the content from another mod.

Research cost will be `40 + round(requirements ^ 1.25) * 6 rounded down to the nearest 10`, where `requirements` is the build cost of your block. *(in otherwords you can't set `requirements` and `research cost` individually)*



## Sprites

All you need to make sprites, is an image editor that supports transparency *(aka: not paint).* Block sprites should be `32 * size`, so a `2x2` block would require a `64x64` image. Images must be `.png` files with 32 bit depth.

Sprites can simply be dropped in the `sprites/` subdirectory. The content parser will look through it recursively, so you can organize them how ever you feel.

Content is going to look for sprites relative to it's own name. `content/blocks/my-hail.json` has the name `my-hail` and similarly `sprites/my-hail.png` has the name `my-hail`, so it'll be used by this content.

Content may look for multiple sprites. `my-hail` could be a turret, and it could look for the suffix `<name>-heat` and what this means is it'll look for `my-hail-heat`.

You can find all the vanilla sprites here:

-   <https://github.com/Anuken/Mindustry/tree/master/core/assets-raw/sprites>

Another thing to know about sprites is that some of them are modified by the game. Turrets specifically have a black border added to them, so you must account for that while making your sprites, leaving transparent space around turrets for example: [Ripple](https://raw.githubusercontent.com/Anuken/Mindustry/master/core/assets-raw/sprites/blocks/turrets/ripple.png)

To override ingame content sprites, you can simply put them in `sprites-override/`.



## Sound

Custom sounds can be added through the modding system by dropping them in the `sounds/` subdirectory. It doesn't matter where you put them. Two formats are needed:

-   `.ogg` required for Desktop/Android
-   `.mp3` required for iOS

Just like any other assets, you reference them by the stem of your filenames, so `pewpew.ogg` and `pewpew.mp3` can be referenced with `pewpew` from a field of type `Sound`.

Here's a list of built-in sounds:

$sounds

## Dependencies

You can add dependencies to your mod by simple adding other mods name in your `mod.json`:

    dependencies: [
      other-mod-name
      not-a-mod
    ]

The name of dependencies are lower-cased and spaces are replaced with `-` hyphens, for example `Other MOD NamE` becomes `other-mod-name`.

To reference the other mods assets, you must prefix the asset with the other mods name:

-   `other-mod-name-not-copper` would reference `not-copper` in `other-mod-name`
-   `other-mod-name-angry-dagger` would reference `angry-dagger` in `other-mod-name`
-   `not-a-mod-angry-dagger` would reference `angry-dagger` in `not-a-mod`



## Bundles

An optional addition to your mod is called bundles. The main use of bundles are give translations of your content, but there's no reason you couldn't use them in English. These are plaintext files which go in the `bundles/` subdirectory, and they should be named something like `bundle_ru.properties` (for Russian).

The contents of this file is very simple:

    block.example-mod-silver-wall.name = Серебряная Стена
    block.example-mod-silver-wall.description = Стена из серебра.

If you've read the first few sections of this guide, you'll spot it right away:

-   `<content type>.<mod name>-<content name>.name`
-   `<content type>.<mod name>-<content name>.description`

Notes:

-   mod/content names are lowercased and hyphen separated.

List of content type:

$contentTypes

List of filenames relative to languages:

$bundles


## Markup

The text renderer uses a simple makeup language for coloring text.

-   `[name]` sets the color by name, there's a few [built-in colors](#built-in-colors);
-   `[#rrggbb]` / `[#rrggbbaa]` sets the color by hex value, with each value being anything from `00` to `ff`:
    -   `rr` is the red value,
    -   `gg` is the green value,
    -   `bb` is the blue value,
    -   `aa` is the alpha value;
-   `[]` sets the color back to the previous color;
-   `[[` escapes the left bracket, so you can write `[[red]` to write and it'll render as `[red]`.

Notes:

-   erros/unknown colors will be silently ignored.

Example:

    [red]red
    [#ff0000]full-red
    [#ff000066]half-red
    [#ff000033]half-half-red
    [#00ff00]green
    []half-half-red



### Built-in Colors

    [clear]clear
    [black]black
    [white]white
    [lightgray]lightgray
    [gray]gray
    [darkgray]darkgray
    [blue]blue
    [navy]navy
    [royal]royal
    [slate]slate
    [sky]sky
    [cyan]cyan
    [teal]teal
    [green]green
    [acid]acid
    [lime]lime
    [forest]forest
    [olive]olive
    [yellow]yellow
    [gold]gold
    [goldenrod]goldenrod
    [orange]orange
    [brown]brown
    [tan]tan
    [brick]brick
    [red]red
    [scarlet]scarlet
    [coral]coral
    [salmon]salmon
    [pink]pink
    [magenta]magenta
    [purple]purple
    [violet]violet
    [maroon]maroon



## Schematic

Fields that require the type `Schematic` can either take a built-in loadout *(see the [Zone](#zone) section)* a base64 string, or the stem name of a `.msch` file in the `schematics/` subdirectory.

*As of now, the only purpose of schematics is to give a zone a loadout.*



## Scripts

Scripting in Mindustry is done with the [Rhino JavaScript](https://github.com/mozilla/rhino) runtime. Scripts may be added to your mod by putting them in `scripts/`. Using the built-in `extendContent` function, you can extend existing Java types from JS, using *allowed classes* which are injected into your namespace.

For example:

//TODO


## GitHub

Once you have a mod of some kind, you'll want to actually share it, and you may even want to work with other people on it, and to do that you can use [GitHub](https://github.com/). If you don't know what Git (or GitHub) is at all, then you should look into [GitHub Desktop](https://desktop.github.com/), otherwise simply use your favorite command line tool or text editor plugin. 

All you need understand is how to open repositories on GitHub, stage and commit changes in your local repository, and push changes to the GitHub repository. Once your project is on GitHub, there are three ways to share it:

-   with the endpoint, for example `Anuken/ExampleMod`, which could then be typed in the ingame GitHub interface, and that would download it;
-   with the zip file, for example `https://github.com/Anuken/ExampleMod/archive/master.zip`, which would download the repository as a zip file, and put in mod directory (unzipping is not required);
-   add the typic/tags `mindustry-mod` on your repository, which should cause the `#mods` Discord bot to pick it up and render it in it's listh.



## FAQ

-   `time` in game is calculated through `ticks`;
-   `ticks` *sometimes called `frames`,* are assumed to be 60/1 second;
-   `tilesize` is 8 units internally;
-   to calculate range out of `lifetime` and `speed` you can do `lifetime * speed = range`;
-   *Abstract* what is `abstract`? all you need to know about abstract types, is this is a Java specific term, which means you cannot instantiate/initialize this specific type by itself. If you do so you'll probably get an *"initialization exception"* of some kind;
-   what is a `NullPointerException`? This is an error message that indicates a field is null and shouldn't be null, meaning one of the required fields may be missing;
-   *bleeding-edge* what is `bleeding-edge`? This is the developer version of Mindustry, specifically it's refering to the Github master branch. Changes on bleeding-edge usually make it into Mindustry in the next release.


