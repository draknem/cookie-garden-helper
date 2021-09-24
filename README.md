# cookie-garden-helper

Forked to optimize for learning new seeds faster and make the mod work on steam reliably

## How to use

Copy this code and save it as a bookmark. Paste it in the URL section.
To activate, click the bookmark when the game's open.

```javascript
javascript: (function () {
    Game.LoadMod('https://draknem.github.io/cookie-garden-helper/cookie-garden-helper.js');
}());
```
To use it with Steam version:

Create a folder named "cookieGardenHelper" in your mods/workshop/ or mods/local folder.

Inside of it create a file named "main.js" and paste the javascript fragment above in it.

Create a file named "info.txt" and paste the following it it:

```json
{
	"Name": "Cookie Garden Helper",
	"ID": "cookieGardenHelper",
	"Author": "yannprada, lstomberg, draknem",
	"Description": "Automation and cheating tool for Garden minigame",
	"Date": "24/09/2021",
	"Dependencies": [],
	"Disabled": 1,
	"AllowSteamAchievs": 1
}
```
Or simply download this repository and copy cookie-garden-helper folder to your mods/workshop/ or mods/local folder.


## How it works

To begin, click the button ***Cookie Garden Helper***, at the bottom of your
garden / farms. There, you can configure how you would like the mod to operate.

The mod loop through each unlocked tile, then tries to auto-harvest
or auto-plant, depending on what is activated.

### Auto-harvest

First, it will check if the tile is empty.

If not, it will check if the plant is immortal. If it is, and the **Avoid immortals** option is **ON**, ignore this tile.

If not, it will compute the plant stage. Below is a list of these stages, and
the conditions when the plant will be harvested:

- young:
  - if it is a weed, and the option **Remove weeds** is **ON**
  - if the option **Clean garden** is **ON**, the corresponding saved slot is
  empty and the plant is already unlocked
  - if the option **Clean garden** is **ON**, the corresponding saved slot is
  not empty but the young plant don't match and is unlocked
- mature:
  - if it is a new seed, and the option **New seeds** is **ON**
  - if the option **All** is **ON**
  - if the option **Check CpS Mult** is **ON**, and the current CpS multiplier
  is above or equal to the one specified at **Mini CpS multiplier**
- dying:
  - if the option **Check CpS Mult** is **ON**, and the current CpS
  multiplier is above or equal to the one specified at
**Mini CpS multiplier**
  - if the plant is dying, the last tick is 5 seconds from expiring,
  and the option **Dying plants** is **ON**

### Auto-plant

This one will work if:

- the tile is empty
- a plot has been previously saved with the button **Save plot**
- the option **Check CpS Mult** is:
  - **ON**, and the current CpS multiplier is
below or equal to the one specified at **Maxi CpS multiplier**
  - **OFF**

***Note:*** mouse over the message *Plot saved*, to see what was saved.

### Manual tools

- **Plant selected seed**:
  - select a seed you have unlocked
  - click this button to fill all the empty tiles of your plot
  - (don't forget to deselect the seed)

- **Cheat timer**:
  - Forces next update to happen within a second
  - Coded in a first way I found so works in an inefficient, roundabout way.

## Sacrifice garden

When you sacrifice your garden, a few things will happen:

- your saved plot will be erased
- the auto-harvest will be toggled OFF
- the auto-plant will be toggled OFF

This is to prevent planting locked seeds, as well as allowing you to verify your
configuration before restarting automation.

The rest of your configuration will remain.
