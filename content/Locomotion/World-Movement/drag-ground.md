---
title: Drag The Ground
---

With a pointer reticule, selecting the ground allows the users to move it along the floor-plane in a familiar "click and drag" way.

It is easy to make small, precise adjustments, and easy to move in directions that are not connected to the users line of sight.

## Little Cities
- There is already heavy use of the pointer line, and "point at ground" is an extremely common verb in the game.
- This locomotion system is supplemented by an adjustable scale (zoom in and out), and snap-turning.
- The user often wants to hop around in nonsequential directions, as they look over their city construction.
- It feels good to quickly move oneselves "backward" to a precise spot from memory.
- The movement input takes exclusive control of the 'grab' buttons on the remote to prevent conflation of movement and selection.
- The blue grid that appears is not the users play space, but a "comfort cage" that provides a visual anchor to help mitigate motion sickness. I think a play-space outline would also work well here.
- The paraboloic selection arc somewhat keeps the world-movement-speed and amount-of-hand-adjustment linearly related. Without it, Selecting a spot further away will have the world dragging faster for the same amount of hand movement. This can lead undesired fast, sudden, and choppy movement; and make intuition harder to develop.

## Cons
- It can be easy for the user to give themselves an uncomfortable experience.
- Movements over large distances is repetative and annoying.

{{< hint type=warning >}}
Minimum Movement threshold, jitter prevention/smoothing, and a maximum drag speed should be explored.
{{< /hint >}}


{{< video "https://xrinteractionlibrary.blob.core.windows.net/vrcaptures/locomotion/drag-ground.mov" >}}