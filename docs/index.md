# Introduction

**Welcome to the official Wiki for [Mindustry](https://github.com/Anuken/Mindustry)!** This site is still very limited, and under construction. You can view progress in the GitHub repository for the project. However, there is no longer a roadmap.

**Contribution is highly encouraged.** If you find anything in the game that is not listed in these articles and would like to help, please feel free to hop onto the [GitHub Repo](https://github.com/MindustryGame/wiki) and open a Pull Request with the changes. If you are new to Markdown, I **strongly** advise you to visit this [beautiful guide](https://commonmark.org/help/) by CommonMark. It has a tutorial (Click "Try our 10-minute Markdown Tutorial") to help you learn Markdown, and a quick reference for the most important aspects of Markdown.

# Getting Started

Getting started with Mindustry is easy. This article covers how to install Mindustry on different platforms and situations. 

## Typical Setup

This is your typical, run-of-the-mill setup process.

### Desktop

#### Steam 

As of recently, you can now [buy the game on Steam](https://store.steampowered.com/app/1127400/) if you would like to support Anuke!

#### Itch.io

1. Visit the game's [itch.io page](https://anuke.itch.io/mindustry), then download a copy of the game from there.
2. Once the `.zip` file is downloaded, unzip it. Usually that is just done by opening it like normal. When it's done, navigate to the folder it extracted into.
3. 
    1. **Windows**: simply open `desktop-release.exe`.
    2. **MacOS**: run `Mindustry.app.`
    3. **Linux**: run `Mindustry`. 

If you have JRE already installed (which is recommended), you can also run `desktop-release.jar` on Windows and Linux.

For bleeding edge builds that are created for every commit, download them on the [MindustryBuilds GitHub repository.](https://github.com/Anuken/MindustryBuilds/releases)

### Android

#### Play Store

There are two different versions of Mindustry on the Play Store; Mindustry and Mindustry Classic. If you want to get the latest releases of Mindustry, go get **Mindustry**. Otherwise, if you want the old classic version, you can get **Mindustry Classic**.

#### F-Droid

F-Droid is an open source app repository that makes sure all apps are secure and not tampered with. First, you will have to download the F-Droid app [here.](https://f-droid.org/) After it has installed, you can install Mindustry from there.

Notice: You will usually get the latest updates through the Play Store before F-Droid.

### iOS

The latest released builds are available on iOS devices only for purchase.

## For Contributors

If you would like to contribute to the game's source code, the best way to go is to compile the game yourself. To compile it yourself:

1. If you haven't already, install at least JRE and JDK 8. 
2. Open a terminal in the root directory, then run these commands: 
    1. For Windows:
        1. Running: `gradlew desktop:run`
        2. Building: `gradlew desktop:dist`
    2. For Linux:
        1. Running: `./gradlew desktop:run`
        2. Building: `./gradlew desktop:dist`
    3. For Server builds, replace `desktop` with `server`. Example: `./gradlew server:run`
