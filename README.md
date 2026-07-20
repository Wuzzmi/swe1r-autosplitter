# STAR WARS RACER AUTOSPLITTER (for LibreSplit)
**A script that automates LibreSplit's timer, for Star Wars Episode I Racer speedruns.**  
Based on [Galeforce's LiveSplit Autosplitter](https://github.com/everalert/swe1r-autosplitter) v0.5.1  
The same autosplitter logic, converted to LUA, with some additions/compatability changes.

### FEATURES
* Choice to auto Start when file is opened, or "Start Race" is selected 
* Auto split at race finish, with togglable 1st place requirment
* Option for auto reset, on return to file selection
* Option to use run catagory presets
* Choose between IGT, LRT and RTA timing methods 
* Ability to remove unfocused/tabbed-out time when using LRT
* Option to view extra stats in terminal

### REQUIRES
* [LibreSplit](https://github.com/LibreSplit/LibreSplit/tree/main)
* Installation of the re-released PC version of Star Wars Episode I Racer (Steam, GOG, etc.)  
    - does not work with the original CD version

## QUICK SETUP (TLDR)
* Download and open the script in a text editor
* Edit the settings, under "AUTOSPLITTER SETTINGS"
* Load and Enable the script in LibreSplit
___
___
## FULL SETUP
* Download the script
* Open the script in a text editor
   
At the top there are script notes, followed by a small settings guide, and under that will be the "AUTOSPLITTER SETTING". 

### AUTOSPLITTER SETTINGS
Here is where all settings can be modified. The script settings include commenting that minimally describes each option. This should be enough to work with, however each setting is described in greater detail below.  
  
> [!caution]
> ```lua
> setting = "value",
> ```
> **When adjusting a **```setting```** it is important that you:**
> * Only edit the **```value```**.
> * Only replace a **```value```** with another of its type. 
> * Make sure that any **```value```** is ended with a comma **```,```**.
>   
> Changing or removing any other syntax (like **```setting```** names, missing any commas **```,```** etc.) will break the script.
___
```lua
local sets = {
--____________________________________________________________________________
--------------------------- AUTOSPLITTER SETTINGS ----------------------------
--____________________________________________________________________________
-- CHOOSE RUN CATAGORY --> None | Any%-Am/Semi Circuit | 100% |  NewGame+ |
   preset = 1,         --> [0]  |         [1]          | [2]  |    [3]    |
--______________________________|______________________|______|___________|___
----------------------------------------------------------|  PRESET = SETS
-- TIMING METHOD  -->In race GT | RT No Loads | Real Time | [1,2,3] = [1](LRT)
   timeMethod = 1,--> [0](IGT)  |   [1](LRT)  | [2+](RTA) |      
----------------------------------------------------------|-------------------
-- REQUIRES 1ST PLACE, or if [false] requires 4th place,  |     [2] = [true]
   req1st = false, --  and 3rd on SMRSMR/BB/BEC           |   [1,3] = [false] 
----------------------------------------------------------|-------------------
-- "START RACE" TIMER TRIGGER (SEMIFUNCTIONAL) - Move     |
   trigSR = false, -- from "Track Select" > "START RACE"  |   [1,2] = [false] 
----------------------------------------------------------|-------------------
-- ENABLE RESET TRIGGER - triggers at file selection.     |      
   reset = true, -- [false] for mid-run file switch.      |     [3] = [false]
----------------------------------------------------------\___________________
-- REMOVE UNFOCUSED TIME (TABBED-OUT) requires RT No Loads 
   noTab = false, -- Affects all presets [timeMethod = 1]
------------------------------------------------------------------------------
-- VIEW EXTRA INFO IN TERMINAL (when LibreSplit is run through the terminal).
   viewTermStats = false, -- Toggles the view of the following extra info.
--  --  --  --  --  --  --  --  --  --  --  --  --  --  --  --  --  --  --  --
                viewIGT = true, -- Total race IGT
         viewCurRaceIGT = false, -- Current race IGT
          viewOverheats = true, -- Counts overheats over whole run
             viewDeaths = true, -- Counts viewDeaths over whole run
--____________________________________________________________________________
------------------------------------------------------------------------------
}
```
___
___
### CATAGORY PRESET 
```lua
preset = 1,
```
**```preset```** is a one setting adjustment for switching run catagories. It functions as a override for a number of other settings. For this reason **```preset``` ```0```** exists, allowing full settings control for special use cases.
|  | None | Any% - Amateur/Semi-Pro Circuit | 100% | New Game + |
|:---:|:---:|:---:|:---:|:---:|
| **preset =** | 0 | 1 | 2 | 3 |  
 > [!note]
> The **```preset```** variable is the only setting that requires adjustment to properly running every catagory.
___
___
**TIMING METHOD**
```lua
timeMethod = 1,
```
Use **```timeMethod```** to choose either IGT, LRT or RTA. As shown in the table below, every catagory **```preset```** overrides to LRT (**```timeMethod = 1,```**). The other timing methods are not useful for recording official runs, but are there if you find a use for them.
|  | In race Game Time (IGT) | Real Time No loads (LRT) | Real Time (RTA) |
|:---:|:---:|:---:|:---:|
|**timeMethod =**| 0 | 1 | 2+ |
| **```preset```** |  | **```1``` ```2``` ```3```** |  |
 
___
**REQUIRE 1ST PLACE**
```lua
req1st = false,
```
**```req1st```** toggles the 1st place win condition requirment to trigger a split. The normal win condition requires 4th place, or 3rd on the last track of a circuit ( SMR/BB/BEC ) to split. **```req1st```** is usually set **```true```** for 100% runs, not of much use otherwise.
|  | Require 1st | Require 4th, 3rd (on SMR/BB/BEC) |
|:---:|:---:|:---:|
|**req1st =**| true | false |
| **```preset```** | **```2```** | **```1``` ```3```** |

___
**"START RACE" TIMER TRIGGER (SEMIFUNCTIONAL)**
```lua
trigSR = false,
```
**```trigSR```** will trigger auto start when "Start Race" is selected. Otherwise autostart continue to start at file open. **```trigSR```** is used for the New Game + catagory, which requires timing to start when selecting "Start Race" for the first track. Otherwise it's uses are limited.
|  | "Start Race" trigger | File open trigger |
|:---:|:---:|:---:|
|**trigSR =**| true | false |
| **```preset```** | **```3```** | **```1``` ```2```** |
 > [!important]
> Currently the "Start Race" trigger is semifunctional. In order for the timer to trigger, you must enter the track selection scene, then move directly to select "Start Race". If you deviate, just return to the track selection scene before heading to "Start Race". 

___
**ENABLE RESET TRIGGER**
```lua
reset = true,
```
**```reset```** toggles auto reset on/off. It is very important to set **```reset = false```** for NG+ runs that require a file/mode change mid run. This will stop file/mode changes from reseting and ruining the run, which is why the NG+ **```preset```** overrides to **```reset = false```**. If your NG+ run doesn't need a file/mode change, and you would like to use **```reset```**, you will have to set **```preset = 0```** and manually set all settings. Aside from NG+ runs, **```reset```** is just personal preference.
|  | Auto Reset On | Auto Reset Off |
|:---:|:---:|:---:|
|**reset =**| true | false |
| **```preset```** |  | **```3```** |
 
___
**REMOVE UNFOCUSED TIME (TABBED-OUT)**
```lua
noTab = false,
```
Use **```noTab```** to set unfocused/tabbed-out time to registered as loading time, so it will not be counted on the timer. **```noTab```** will only take effect if **```timeMethod = 1,``` (LRT)** is set (most cases). Otherwise unfocused/tabbed-out time will be counted like normal. Usage of **```noTab```** is up to you.
|  | Tabbed Time Removed | Tabbed Time Counted |
|:---:|:---:|:---:|
|**noTab =**| true | false |

___
**VIEW EXTRA STATS IN TERMINAL**
```lua
viewTermStats = false,
```
**```viewTermStats```** toggles your enabeled stats to be viewable in the terminal. **```viewTermStats```** has no effect unless you are running LibreSplit through the terminal, so keep **```false```** if not. This is not ideal, but is currently the best option. "[LiveSplit's ASL variable viewer](https://github.com/hawkerm/LiveSplit.ASLVarViewer)" allows these stats to be viewed in [LiveSplit](https://github.com/LiveSplit/LiveSplit) (there is no LibreSplit alternative).   
  
  
|  | Enabled | Disabled |
|:---:|:---:|:---:|
|**viewTermStats =**| true | false |
|  |  |  |
|**viewIGT =**| true | false |
|**viewCurRaceIGT =**| true | etc... |  
  
Displaying each stat is set just like **```viewTermStats```**.
___
**DISPLAYABLE STATS**
___
**IGT**
```lua
viewIGT = true,
```
**```viewIGT```** displays you true IGT (totaled in game race times). This is very usefull if you are using LRT or RTA as your timing method and also want to track IGT. It is identical to the IGT timing method.
___
**CURRENT RACE IGT**
```lua
viewCurRaceIGT = false,
```
**```viewCurRaceIGT```** displays the IGT of your current race only. This is identical to the ingame race timer. Not of much use, but it's here if you want it... maybe you want to see your previous race IGT in the menu before starting your next race?
___
**OVERHEAT COUNT**
```lua
viewOverheats = true,
```
**```viewOverheats```** shows how many times you have overheated during your run.
___
**DEATH COUNT**
```lua
viewDeaths = true,
```
**```viewDeaths```** shows how man times you have died during your run.
___

## LOADING/RUNNING THE SCRIPT
To load the script, open LibreSplit normally, or through terminal if **```viewTermStats = true```**. Right click in the window and select "Open Auto Splitter" select the script and "Open" it. Ensure that "Enable Auto Splitter" is checked. 
![Load and Enable Autosplitter in LibreSplit](https://github.com/Wuzzmi/swe1r-auto_splitter/blob/main/img/libresplit-load-enable.png)
If you have edited your script settings after it was already loaded and enabled, you will need to uncheck and recheck "Enable Auto Splitter" for the changes to take effect. Now everything is all set and the autosplitter will function when you run the game!

