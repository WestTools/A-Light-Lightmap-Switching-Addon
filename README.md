# A-Light Lightmap Switching: Addon

<p>
  <img alt="Unity 2022.3+" src="https://img.shields.io/badge/Unity-2022.3%2B-222?logo=unity">
  <img alt="Needs A-Light" src="https://img.shields.io/badge/needs-A--Light-ff8a3d">
  <img alt="Free" src="https://img.shields.io/badge/price-free-8a6cff">
</p>

an addon for [A-Light](https://github.com/WestTools/A-Light-Unity-GPU-Lightmapper) that lets you bake a few different lighting setups and switch between them while the game is running. day and night, lights on and lights off, power cut, whatever you want

normally you only get one baked lighting setup per scene. this lets you have as many as you want

## what it does

- bake as many lighting **sets** as you want in one scene
- each set has its own list of objects to turn **on** and **off**, so you can put the sun in one set and the lamps in another
- **Bake All Sets** bakes every set in one go
- switch sets in game from a button, a trigger, or your own script
- each set has an **On Activate** event so you can change the skybox, fog, sounds and stuff at the same time
- every set gets its own copy of the lightmaps, so baking again doesnt overwrite your other sets

## what you need

- **A-Light**, grab it [here](https://github.com/WestTools/A-Light-Unity-GPU-Lightmapper/releases). without it this addon just does nothing
- **Unity 2022.3 or newer**

## how to install

1. install A-Light first if you havent already
2. grab `A-Light-Addon-LightmapSwitching.unitypackage` from [releases](../../releases)
3. in unity go **Assets › Import Package › Custom Package** and import it
4. open **A-Light › Render Lightmaps** and go to the **Addons** tab

## how to use it

1. in the **Addons** tab hit **Add Lightmap Switcher to this scene**. it starts you off with a Day and a Night set
2. drag the lights for each set into its **Enable Objects** list. put stuff that should be off into **Disable Objects**
3. hit **Bake** on each set, or **Bake All Sets** to do them all
4. hit **Use** on a set to see it in the editor

your sets get saved to `Assets/ALightLightmaps/Sets/`

## switching in game

the **A-Light Lightmap Switcher** object has these, you can call them from a button's OnClick, a UnityEvent, or a script:

| method | what it does |
|---|---|
| `SetLighting(int index)` | switch to a set by its number (first set is 0) |
| `SetLightingByName(string name)` | switch to a set by its name |
| `Next()` | go to the next set |
| `Previous()` | go to the previous set |

from a script:

```csharp
using ALightAddons.LightmapSwitching;
using UnityEngine;

public class NightButton : MonoBehaviour
{
    public ALLightmapSwitcher switcher;

    public void GoNight()
    {
        switcher.SetLightingByName("Night");
    }
}
```

turn on **Apply On Start** and pick a **Start Set** if you want the game to start on a certain set

## good to know

- dont move or change your static objects between baking sets. every set should be baked with the same geometry, only the lights should change
- if you change your map, bake all the sets again
- each set is a full copy of your lightmaps, so lots of sets = bigger build size
- switching is instant, it doesnt fade between sets

## contributing

bug reports with screenshots help the most. PRs are welcome

## disclaimer

this will ALWAYS be a free unity package. if anyone sells it to you, you got scammed. feel free to share it
