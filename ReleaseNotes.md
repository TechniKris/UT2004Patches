# Unreal Tournament 2004 Release Notes

## General Information

### Official Unreal Tournament Web Sites

* [Unreal Tournament Home Page](https://www.unrealtournament.com)
* [Epic Games Home Page](https://epicgames.com)
* [Unreal Engine Technology Page](https://www.unrealengine.com)

### Independent Unreal Tournament Web Sites and Discord servers

* [OldUnreal site](https://www.oldunreal.com) / [OldUnreal Discord](https://discord.com/channels/143986633992175616/1053202987545264128)
* [MiA Forums](https://www.miasma/rocks)  / [MiA Discord](https://discord.gg/CxdXaEauya)
* [CEONS Forums](https://ceonss.net/) / [CEONS Discord](https://discord.com/channels/310878149158240257/310878149158240257)

## Unreal Tournament 2004 Version 3374 Release Notes

Version 3374 is completely network compatible with the previous public release of UT2004 (3369). 

### Patch Highlights

* We now natively support Linux and macOS systems with x86_64/amd64 and arm64/aarch64 CPUs 
* You can now play the game or run a server on a Raspberry Pi 4 or 5, albeit at rather slower frame-rate than on a PC!
* The Linux and macOS distributions of the patch now include a fully functional UCC with an UnrealScript compiler (UCC make)
* We dropped support for 32-bit CPUs, for old versions of Windows (i.e., Vista or earlier), and for DirectX 8
* The Windows version of the game now requires DirectX 9
* The Linux and macOS versions now use SDL3 instead of SDL1
* We dealt a first (minor) blow to the editor goblin! Unreal Editor will no longer freeze for several seconds when clicking a viewport

### Stability Improvements

#### Unreal Editor

* We fixed a bug that crashed Unreal Editor when converting meshes to brushes
* We fixed a bug that crashed Unreal Editor when you opened a map while the 3D viewport was in realtime mode

#### Networking and Netcode

* We fixed a networking bug that allowed players to perform illegal combo moves and to crash servers

#### Audio and 3D Rendering

* We fixed a bug that could crash the game when rendering skeletal meshes with invalid hierarchies

#### UnrealScript

* The game should no longer crash if you click a tab in an in-game menu whose content is still being rendered

#### Miscellaneous

* We fixed a bug that made the game crash when reading an Unreal package with an unexpected GUID
* We fixed a garbage collection bug that made the game crash upon shutdown
* We fixed a bug that made the game randomly crash when it tried to write to the log file during shutdown

### Bug Fixes

#### Unreal Editor and UCC

* The procedural sound context menus should now be fully functional
* The display checkbox for placeables actors in the actor browser should now work as expected
* We fixed a bug that made Unreal Editor create dummy packages when converting static meshes to or from brushes
* Unreal Editor now saves viewport sizes correctly even when viewports are minimized
* Large .int files are now saved correctly without truncation ([#12](../../issues/12))
* The UnrealScript compiler now parses and compiles scripts in the correct order after it processes `dependson` directives
* The editor no longer moves left and down when clicking on a viewport, when used on a multi-monitor setup
* Viewport selection no longer takes a century, instead acting instantly
* We fixed bugs that made Unreal Editor incorrectly import and export DDS files

#### Networking and Netcode

* The game now reports the correct progress percentage when downloading files from a game server

#### Audio and 3D Rendering

* We fixed a bug that made ambient sounds restart whenever the player camera switches to a different view target
* Music fadeouts should now work as expected

#### UnrealScript

* We fixed a plethora of accessed nones and UnrealScript-based exploits, crash bugs, and denial-of-service attacks (Thank you Wormbo and Shambler!)
* We fixed a bug that could make the SPMA camera explosion loop without stopping ([#24](../../issues/24))
* The PlayerController.AskForPawn function now jumps to the Spectating.Begin state correctly ([#10](../../issues/10))
* The PlayerController.ToggleScreenShotMode function no longer discards user preferences such as the weapon handedness, crosshair visibility, HUD visibility, and the TeamBeaconMaxDist and bHideVehicleNoEntryIndicator settings ([#11](../../issues/11))
* The DeathMatch.InitTeamSymbols function can no longer give multiple teams the same symbol ([#16](../../issues/16))
* We fixed a bug where gibbed players or monsters can be gibbed multiple times by sources of constant damage
* We fixed several bugs that made Engine.Canvas incorrectly process newline characters and color codes

#### Miscellaneous

* We now support command lines longer than 1024 characters

### Enhancements

#### Unreal Editor

* The Unreal Editor window no longer minimizes when testing a map
* The properties window now supports mouse wheel scrolling
* You can now expand and collapse items in the properties window using keyboard arrows
* The music browser now supports ogg files
* You can now import ASE and OBJ models as static meshes
* We overhauled the texture compression code and switched to a new texture compression support library (AMD Compressonator). The new code works on all platforms so you can now import compressed textures using UCC make
* You can now launch UCC from different folders on Linux and macOS

#### Networking and Netcode

* Download messages now include information about the number of packages to download and the percentage of total download completed
* The game client now downloads and collates game server information from multiple master servers
* Game servers can now connect to multiple community master servers
* You can now configure the UCC server query port number for admins. See [here](https://github.com/ukpiglet/UDPRelay) for an example of how this can be used on a Windows based UCC server
* Demos recorded in offline games will now work with mods that add packages to the package map using Actor.AddToPackageMap

#### Audio and 3D Rendering

* Full screen support is now available in the 64-bit Windows client
* You can now cap your frame rate for menus and for offline games using the MaxMenuFrameRate and MaxOfflineFrameRate settings (see Default.ini)
* The player model now renders in mirror reflections
* Vertex models now render in OverlayMaterial
* You can now crossfade between two music tracks using MusicEvents

#### Input and Windowing

* The log and terminal windows can now be minimized and maximized
* The Unreal Editor log window position now persists through restarts

#### UnrealScript

* The game now plays a "drowning" sound rather than "hit underwater" sound when the player is under water and starts losing health ([#18](../../issues/18))
* We added a new console command, `stat fpos`, that configures the placement of the `stat fps` output relative to the top-right corner of the screen. See Default.ini: `FPSPosX` and `FPSPosY`
* We added a new console command `is_pi`, which returns 1 when running on a Raspberry Pi
* We have added more default screen resolutions to the Display menu
* We added a new native function, Actor.KRagdollExists, to check if a named ragdoll exists for the actor
* Dying players now play their death animation if they do not have a ragdoll
* We improved several of the error messages the game logs when encountering errors in UnrealScript code
* You can now set the MaxWarnPerFunc option in the [Core.System] section of the ini file to limit how many errors individual UnrealScript functions can log before the game silences them
* You can now add asset files (ogg/ka) to the package map using the Actor.AddToPackageMap function

#### Miscellaneous

* The game will no longer truncate log files when it crashes
* We added a KarmaPath setting to the [Core.System] section of the ini file
* The game now reads and writes human-readable text color codes from and to the ini file
* The Linux binaries now perform a case-insensitive file search when they cannot open required localization files