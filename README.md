# Star Wars Racer Auto Splitter (for LibreSplit)
A script that automates LibreSplit's timer, for Star Wars Episode I Racer speedruns.  

### Features
* Auto Start when file is opened, or (experimentally) when selecting "Start Race" for New Game +
* Split at race finsh
  * Option to require 1st place for 100%
* Reset on return to file selection
  * Option to disabled reset
* Run catagory presets (optional)
* Choose between IGT, LRT, RTA for timing methods 
* Ability to remove unfocused / tabbed out time when using LRT
* Option to view extra information in terminal (when LibreSplit is run through terminal)

### Requires
* Installation of the re-released PC version of Star Wars Episode I Racer (Steam, GOG, etc.).  
    - Does not work with the original CD version.
* [LibreSplit](https://github.com/LibreSplit/LibreSplit/tree/main)

## Quick Setup (TLDR)
* Download the script (swe1r-auto_splitter.lua).
* Open the script with a text editor
* under "AUTO SPLITTER SETTINGS" edit settings 
* Load and Enable the script in LibreSplit

## Configuring Settings

### Getting Started
After downloading the auto splitter, open it with a text editor.  
Beneath the script information at the top, there will be some settings notes, and under that the  
"AUTO SPLITTER SETTING" themselves. 

### Auto Splitter Settings
___
> [!caution]
> ```lua
> setting = "value",
> ```
> **When adjusting settings it is important that you:**
> * Only edit the **```value```**.
> * Only replace a **```value```** with another of its type. 
> * Make sure that any **```value```** is ended with a comma **```,```**.
>   
> Changing or removing any other syntax (like **```setting```** names, missing any commas **```,```** etc.) will break the script.
___
```lua
local sets = {
--____________________________________________________________________________
--------------------------- AUTOSPLITTER SETTINGS-----------------------------
--____________________________________________________________________________
-- Choose Run Catagory-->| None | Any%-Am/Semi Circuit | 100% |  NewGame+ |
   preset = 1, --     -->| [0]  |         [1]          | [2]  |    [3]    |
--_______________________|______|______________________|______|___________|___
----------------------------------------------------------|  FORMAT = SETS
-- Timing Method -   In race GT - RT No Loads - Real Time | [1,2,3] = [1](LRT)
   timeMethod = 1, -- [0](IGT)  -   [1](LRT)  - [2+](RTA) |      
----------------------------------------------------------|-------------------
-- Requires 1st place, or if [false] requires 4th place,  |     [2] = [true]
   req1st = false, --  and 3rd on SMR/BB/BEC.             |   [1,3] = [false] 
----------------------------------------------------------|-------------------
-- (semi-functional) Timer triggers at "Start Race",      |     [3] = [true]
   trigSR = false, -- instead of file select.             |   [1,2] = [false] 
-- Must move directly from "Track Select" > "Start Race"  |
----------------------------------------------------------|-------------------
-- Enable reset trigger - triggers at file selection.     |      
   reset = true, -- [false] for mid-run file switch.      |     [3] = [false]
----------------------------------------------------------\___________________
-- Real-Time No Loads removes unfocused time (tabbed out)
   noTab = false, -- Affects all presets [timeMethod = 1]
------------------------------------------------------------------------------
-- View Extra Info In Terminal (when LibreSplit is run through the terminal).
   termInfo = { view = false, -- Toggles the view of the following extra info.
--  --  --  --  --  --  --  --  --  --  --  --  --  --  --  --  --  --  --  --
                 totalRIGT = true, -- Total race IGT
                   curRIGT = false, -- Current race IGT
                 overHeats = true, -- Counts overheats over whole run
                    deaths = true, -- Counts deaths over whole run
   }--________________________________________________________________________
------------------------------------------------------------------------------
}
```
In the script, each setting is detailed to a minimal degree. This should be enough to work with, but below each setting is described in more detail.
___
### Choose Run Catagory 
```lua
preset = 1,
```
|Catagory| None | Any%-Am/Semi Circuit | 100% | New Game + |
|:---:|:---:|:---:|:---:|:---:|
|**Value**| 0 | 1 | 2 | 3 |  
 
**```preset```** is the most important setting. It functions as a parent setting for of a number of other settings. Setting **```preset```** to **```1```,  ```2```, or ```3```** will override these settings. For this reason **```preset``` ```0```** exists, allowing for full settings control for special use cases (advanced users).

 > [!note]
> The **```preset```** variable is the only setting that requires adjustment, in order to properly run all catagories.

___
**Timing Method**
```lua
timeMethod = 1,
```
|Method| In race Game Time (IGT) | Real Time No loads (LRT) | Real Time (RTA) |
|:---:|:---:|:---:|:---:|
|**Value**| 0 | 1 | 2+ |
| **```preset```** |  | **```1``` ```2``` ```3```** |  |
 
Here you are given the option to choose your prefered Timing Method. As shown all 3 catagory presets override to **```timeMethod = 1,``` (LRT)**. The other 2 aren't useful for recording official runs, but maybe useful for other specific use cases.

___
**Requires 1st place**
```lua
req1st = false,
```
| Win Condition | 1st | 4th / 3rd (on SMR/BB/BEC) |
|:---:|:---:|:---:|
|**Value**| true | false |
| **```preset```** | **```2```** | **```1``` ```3```** |

**``````** 
 
___
**(semi-functional) Timer triggers at "Start Race"**
```lua
trigSR = false,
```
|  |  |  |
|:---:|:---:|:---:|
|**Value**| true | false |
 
**``````** 

___
**Enable reset trigger**
```lua
reset = true,
```
|  |  |  |
|:---:|:---:|:---:|
|**Value**| true | false |
 
**``````** 

___
**Real-Time No Loads removes unfocused time (tabbed out)**
```lua
noTab = false,
```
|  |  |  |
|:---:|:---:|:---:|
|**Value**| true | false |
 
**``````** 

___
**View Extra Info In Terminal**
```lua
termInfo = { view = false,
```
|  |  |  |
|:---:|:---:|:---:|
|**Value**| true | false |
 
**``````** 
