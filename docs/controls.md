# Controls

The port drives a **virtual Wii Remote + Nunchuk** from the keyboard and mouse (`[prime] keyboard_mouse = true`,
the default). Every binding below can be changed in **F1 > Controls**: click a cell, press the new key or mouse
button; right-click clears it. Changes save immediately to `UserData/Config.toml` (`[prime_keys]`).

The game's own button prompts (A, B, Z, C, +, -, 1, 2, D-pad, stick, gestures) are replaced by key caps that show
your current primary binding. Key names come from Windows, so they follow your keyboard layout and display language
(for example *Mayús* on a Spanish Windows, *Shift* on an English one).

## Buttons and pointer

| Keyboard / mouse | Wii Remote / Nunchuk | Notes |
| --- | --- | --- |
| Mouse movement | Pointer | Menus, map, aiming. In first person without a lock-on the camera follows the mouse (see below) |
| Left click, Enter | A | Select, fire, interact |
| Right click, Space | B | Jump, cancel |
| W / A / S / D | Nunchuk stick | Move |
| Left or right Shift | Z | Lock on |
| Left or right Ctrl | C | Morph Ball |
| Arrow keys; middle click = down | D-pad | Visors, seeker missiles |
| 1 | + | Pause / menu (Esc opens the port's exit prompt) |
| 2 | - | Visor select |
| Numpad 1 / Numpad 2 | 1 / 2 | |
| H | HOME | |

## Gestures

The game only recognises a handful of motion signals. Each one has a key:

| Signal the game detects | Used for | Key |
| --- | --- | --- |
| Push the remote forward / pull it back | Levers, ship controls, pulling objects | **E** / **Q** (hold briefly, then release; do not press both) |
| Twist the remote left / right | Valves and rotating mechanisms | **Z** / **X** (also Numpad 7 / 8) |
| Flick the Nunchuk | Grapple Lasso: throw / pull | **R** / **F** |
| Flick the remote up | Morph Ball spring jump | **T** |
| Shake both controllers | "Shake" prompts | **G** (hold) |
| Tilt the remote up / down | Aim at the ceiling / floor in some prompts | **U** / **J** (hold) |
| Twist the Nunchuk left / right | Rarely used | **N** / **M** (hold) |
| Tilt the Nunchuk up / down | Rarely used | **I** / **K** (hold) |
| Slow motion for twist and push gestures | Fine control of valves and levers | **Alt** (hold): Z/X and E/Q run at 35 % speed |

**F6** opens a live panel of what the game receives from the virtual remote (roll, depth, pointer, accelerometers),
useful when a gesture prompt does not react.

## Mouse look

Enabled by default (F1 > Controls > *Camera follows the mouse in first person*). While aiming in first person without
a lock-on, moving the mouse turns and pitches the camera like a PC shooter and the game's pointer stays centred.
In menus, the map, Morph Ball, cutscenes and while Samus is at the ship's controls the pointer is absolute again.

Settings in the same tab: sensitivity (degrees per pixel, 0.20 by default), vertical inversion and smoothing
(0 = none by default). The maximum turn rate is still the game's own: raise it in the game menu > Options > Controls >
Sensitivity (Advanced has the smallest dead zone and the fastest turn).

## Latency

Three options, all on by default, shorten the time between moving the mouse and seeing the result:

- **Pointer without the game's smoothing** (F1 > Controls): the game averages the Wii pointer to remove hand jitter; a mouse has none, so the filter only adds delay.
- **Single-frame present queue** (F1 > Performance): DirectX otherwise queues up to three images.
- **Borderless fullscreen** (F1 > Video): a bordered window also waits for the Windows compositor.

## Real Wii Remote (Bluetooth)

Set `keyboard_mouse = false` in F1 > Controls (restart), pair the remote in Windows Settings > Bluetooth (press 1+2 or
SYNC, leave the PIN empty), then check **F10 > Controller settings > Wii Remotes**. This path has had much less
testing than keyboard and mouse; reports are welcome.
