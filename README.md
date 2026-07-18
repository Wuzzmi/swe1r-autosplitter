# Star Wars Racer Auto Splitter (for LibreSplit)
An auto splitter script that automates LibreSplit's timer, for Star Wars Episode I Racer speedruns.  

### Features
* Auto Start, Split, and Reset (based on settings)
* In script settings including:  
  - presets for run catagory  
  - and/or advanced full settings control
* Option to view extra information in terminal (when LibreSplit is run through terminal)

### Requires
* Installation of the re-released PC versions of Star Wars Episode I Racer (Steam, GOG, etc.).  
    - Does not work with the original CD version.
* [LibreSplit](https://github.com/LibreSplit/LibreSplit/tree/main)

## Quick Setup (TLDR)
* Download the auto splitter (swe1r-autosplitter.lua).
* Open the script and edit settings (under "AUTO SPLITTER SETTINGS") with a text editor
* Load and Enable the script in LibreSplit
* Open Star Wars Racer if not already open
* Race!

## Setup / Settings Breakdown
### Script Navigation
<!-- <img align="right" src="https://github.com/Wuzzmi/swe1r-autosplitter/blob/main/img/autosplitter-settings3.png"> -->
Once you have downloaded the auto splitter, proceed to open it in your prefered text editor.  
At the top, you will find:
* Information about the auto splitter
* Settings tips
  
Below these, labeled as "AUTO SPLITTER SETTING" are the script settings themselves. 

### Settings Configuration
By default the script is already set up for:
* Any%
* Amateur Circuit
* Semi-Pro Circuit
  
If this is your chosen format you will likely not need to change anything.
  
---
> [!caution]
> All settings are contained as variables in a lau   **```table { name = value, }```**.  
> It is important that you:  
> * Only edit the **```value```** of variables.
> * Make sure that any **```value```** is ended with a comma. **```name = value,```**
>   
> Changing any other syntax, like variable **```names```** etc. or missing any commas **```,```** probably will break the script.
---

### Choose Run Format 
**Default: ```preset = 1,```**  
|Preset| None | Any%-Am/Semi Circuit | 100% | New Game + |
|:----:|:----:|:--------------------:|:----:|:----------:|
|**Value**|  0   |           1          |   2  |      3     |  
 
 Setting **```preset```** to **```1```,  ```2```, or ```3```** will override the values of a number of other settings. For this reason **```preset``` ```0```** exists, allowing for full settings control for special use cases (advanced users).

 > [!tip]
> The **```preset```** variable is the only setting that requires adjustment, in order to properly run all formats.

WIP...
