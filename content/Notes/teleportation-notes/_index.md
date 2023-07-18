---
title: Notes on Teleportation
---

{{< hint info >}}
This document was originally published in 2019 on the 'Immersive Media Pocket Reference', a previous collection of design notes that has since been removed and replaced with more specific projects, like this one and the [guidebook](http://guidebook.hdyar.com). The tone/content of this page may seem different.

I am continuously working to "break apart" the notes from this original document to per-topic pages on this site. Further updates will happen there.
{{< /hint >}}
Teleportation is a simple mechanic to implement, but a difficult mechanic to implement well. Teleportation has a lot of depth.

See the [Glossary entry on Teleportation](../glossary/Locomotion/Teleportation.md) for definitions.

A good teleportation system...
- is intuitive
- is forgettable
- clearly indicates valid and invalid destinations
- makes it very hard to accidentally select the wrong destination
- does not have an overly noisy/bright/distracting Destination marker/parabola marker.
- Has a destination marker that "fits in" to the design of the world
- informs the player will know where they end up, limits "where am I" disorientation
- has a limited range that is appropriate for the environment
- does not obstruct other mechanics
- minimizes motion sickness
- does not limit the player needlessly
- allows for fine-tuned adjustment, for example
- can optionally show a room overlay (for granular teleportation systems)
- clearly indicates unique cases of teleportation, such as if one is teleporting to a new level, or going to change their scale.
- indicate players movement in multiplayer experiences

# Staying out of the way
My personal favorite implementation of teleportation is from Owlchemy Labs **Vacation Simulator**. It's zone-based teleportation that selects the next direction from gaze direction and a button press. The system gets out of the way and is forgotten as much as possible. If you were to talk about all of the mechanics in Vacation Simulator, you may forget to mention teleportation at all. It's easy to forget about. For such an immersion-breaking mechanic, that's a good thing. One wants the player to be focused on the experience, not on magical glowing parabolas or on selecting a destination that won't have them bonking real-world walls.

It is very important to allow the player to move around without having to think about their real-world environment or relative positioning, and Vacation Simulator pulls this off well.

# Design
The teleportation system should match the world. Even if the teleportation markers are more of a UI overlay than an 'in game' element, they should be designed with attention.

{{< video "https://xrinteractionlibrary.blob.core.windows.net/vrcaptures/teleportation/gardenofthesea-style-teleport.mp4" >}}

I particularly like the "Gooey" teleportation system in **Garden of the Sea**. Glowing laser-parabolas would not have fit in with the soft, inviting, and friendly world.

**Half + Half** also had an interesting teleportation design that fits well with it's world. It's gimbal-slingshot. It's fun to play with, and it doesn't just show a trajectory line of the teleporter, it also shoots a mini version of your avatar.

{{< columns >}} <!-- begin columns block -->

{{< rawhtml >}}
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Beautiful hand tool details in <a href="https://twitter.com/normalvr?ref_src=twsrc%5Etfw">@normalvr</a>’s Half + Half<br><br>like this gimballed teleportation slingshot for hide+seek<br><br>love these wonky mechanicals!<a href="https://twitter.com/maxweisel?ref_src=twsrc%5Etfw">@maxweisel</a> <a href="https://t.co/DN0oO5Kvti">pic.twitter.com/DN0oO5Kvti</a></p>&mdash; Gray Crawford → OC6 (@graycrawford) <a href="https://twitter.com/graycrawford/status/1172271680783360000?ref_src=twsrc%5Etfw">September 12, 2019</a></blockquote>
{{< /rawhtml >}}

<---> <!-- magic separator, between columns -->
{{< video "https://xrinteractionlibrary.blob.core.windows.net/vrcaptures/teleportation/half-half-slingshot.mp4" nopreload>}}

{{< /columns >}}

**Half + Half** is multiplayer, this slingshot helps communicate to other players when somebody teleports, and where they go, and watching the animation of the player travel slows down the player and discourages spamming, without being punishing. Slingshots are fun, not a hindrance.

# Orientation & Landmarks
It is considered a good practice not to re-orient the player when they teleport. They should be facing the same world-relative direction at the start and end of the teleportation. If a recognizable landmark is in the distance visible, and they teleport closer to it, it should still be visible. If the player teleports to in front of a work-bench, for example, the system should probably not "helpfully" snap the player to be facing that work bench. The player should initiate this turn themselves, either through controller input when selecting the destination or by just turning their body. 

We may wish to allow the player to re-orient themselves (their rotation) during the teleportation. The teleportation destination marker may include an arrow or indicator of some kind informing the user which direction they are going to be pointed when they teleport. 

# Laziness and Spamming
Laziness through teleporting is a problem.

{{< video "https://xrinteractionlibrary.blob.core.windows.net/vrcaptures/teleportation/short-teleport-thelab.mp4" nopreload>}}
*A player teleporting a very short distance to pet the dog in The Lab instead of taking a **single step** inside of their play space.*

Players are used to in-game locomotion mechanics. When given one, they often prefer to use the locomotion instead of moving their real body around. Moving ones legs takes effort! Far more than moving a finger tip. This is not ideal.

## Why Teleportation Spamming is a Problem
Moving their head around gives the player depth and parallax information that helps create presence, invites discovery/curiosity, and allows for more subtle and detailed world design.
Moving ones feet through the world creates a sense of presence that is threatened by constant player teleportation.
Counterintuitively, moving also reduces perceived fatigue. Players that are moving around, even slightly, tend not to feel tired as quickly.

{{< hint >}}
If you had to stand up for an hour, what would be harder for you: being allowed to pace around a room and stretch; or standing perfectly still without taking a single dstep?
{{< /hint >}}

World design can be a part of the problem. If one is limited in teleportation range yet given long open paths, then the player is likely to spam the teleportation, and thus get used to doing this for all locomotion - small movements too, not just large area traversal.

{{< video "https://xrinteractionlibrary.blob.core.windows.net/vrcaptures/teleportation/teleportation-spamming-forestry.mp4" nopreload>}}
*A player spamming teleportation in order to cover a large distance in **Forestry**. Note how the fast mid-teleportation animation, open design, and long visible paths encourage this behavior, and that the landmarks and limited range means the player can almost always recognize where they are when teleporting.*

One may wish to prevent the player from teleporting too close to themselves, but I believe this is a mistake, as sometimes a player may wish to "fine-tune" their position, especially when they have a smaller play area.

# Selection Accuracy 
Selecting a destination with a straight-line laser-pointer style selection is difficult for players. The required accuracy of their pointing increases exponentially as the distance away from themselves increases. To counter this, one common solution is to show the teleportation as a parabolic arc, calculated like a thrown object. This allows a change in the angle of the controller to more consistently map to a change in the distance of destination.

{{< video "https://xrinteractionlibrary.blob.core.windows.net/vrcaptures/teleportation/parabola-selection-forestry.mp4" nopreload>}}
*Calculating parabolic arc's from the hands position for teleportation improve accuracy and limit range.*

## Range
It is often desired to limit the range of the users teleportation destinations. This is often important from a design perspective, as it forces the user to be more aware of their surroundings and the path they take through an environment. It helps with the above issue of selection accuracy. It can be annoying for a player to teleport multiple times to reach a further destination. One would want to design environments that avoid "long straight hallways" when using limited ranges.

For zone based teleportation, one can be more flexible with range, especially if the destination can be clearly selected. 

## Teleporting For Level/World Changes and Scale changes
If zones are conceptually linked, teleporting towards a certain type of area or through something can trigger a level load and send the player to a whole new location. 

One can teleport through a doorway, and when they are done teleporting be in the middle of a new room, and not at the entrance by the door. Or teleporting to an archway and end up in a whole new environment.

The "exit" gates in **Vacation Simulator** are an example of this with zone-based teleportation, and the various magical doorways in **The Museum Of Other Realities** do this well with granular teleportation. 

{{< video "https://xrinteractionlibrary.blob.core.windows.net/vrcaptures/teleportation/moor-teleport-through-door-portal.mp4" nopreload >}}

It must always be clear to the player that they are about to end up "somewhere else", somewhere other than where their destination marker indicates. The biggest design challenge with such a system is indicating this to the player. If one is about to see a loading screen when they expect a quick blink, thats trouble. It needs to be clear that teleporting to this zone is "different" than how most of the teleporting systems work.

**Vacation Simulator** does this through unique in-world objects and signage - as well as having an advantage of being zone-based conceptually. **Museum Of Other Realities** communicates with a consistent use of this funky tie-dye magic-gate design. It doesn't tend to show the player where they will end up, as discovery and inviting curiosity is part of the design and joy of the museum.

**The Museum Of Other Realities** also has an exceptional use of teleporting into a different scale, when the player can go "into" various pieces of art.

{{< video "https://xrinteractionlibrary.blob.core.windows.net/vrcaptures/teleportation/moor-teleport-scale-change.mp4" nopreload>}}

{{< hint >}}
Teleporting 'into' art in Museum of Other Realities is a personal favorite experience. It feels so magical.
{{< /hint >}}

The destination marker shrinks/grows accordingly. **The Lab** does this when teleporting into the "Longbow" level, with a small avatar character to help show you your scale before/after the teleport. Scale shifts while teleporting are a interesting because ... they just work. Such scale shifts can be challenging with other locomotion systems. I would love to see more examples of this done well. Scale is still an under-explored mechanic in VR.

The following example is a player, unassisted and unprompted by anyone else, teleporting "down into" a piece of art in the **Museum of Other Realities**. This player has never been in this experience before, but the scale-shift during teleportation was perfectly intuitive.

## Obstacle Limitations
You want to prevent the teleportation system from allowing the player to teleport into an out-of-bounds area, or to an area that would be uncomfortable, like "into" a table. One must give the player feedback when a destination is invalid. One solution is to make the destination marker only appear when a valid destination is selected - indicating nothing would happen if the player pushed the teleport button. This works, but makes it harder the player to adjust their selection to a valid location. I consider it better to give the player feedback. Perhaps show an "invalid" indicator at the destination marker and change the color of a parabola.

{{< video "https://xrinteractionlibrary.blob.core.windows.net/vrcaptures/teleportation/gardenofthesea-teleport-valid-indication.mp4" nopreload>}}
*Garden of the Sea make's it clear when a valid destination is selected by changing the visuals, pattern, and opacity of the indicator.*

If the design of the teleportation system is so noisy that this feedback is distracting to the player, then there are more design problems than just the feedback. 

Another consideration is if the player can teleport "through" objects. It is probably a good idea to prevent them from doing this. If one is teleporting through an object, they probably have a less clear idea of what their destination looks like - no landmark will be visible both before and after the teleportation. This can lead to disorientation. It can also be used for dramatic or comedic effect. 

{{< video "https://xrinteractionlibrary.blob.core.windows.net/vrcaptures/teleportation/forestry-teleport-through-tree-obstacle.mp4" nopreload>}}
Forestry allows players to teleport through objects, but the world is open enough that disorientation or lack of landmarks is not generally an issue.

These limitations can slow a player down naturally, and force them to think before teleporting. Which is probably what we want the player to do, except for cases of large-area traversal.

## Mid-Teleportation Animation
It's generally a poor idea to instantly snap the player to their destination, as the sudden change in visuals can be jarring.

The most common effect is not to instantly snap the user to a new location, but to quickly fade the screen to black. This is effective at reducing disorientation. Some systems don't fade the screen completely to black, but just fade in a strong vignette.

Another commonly used animation is to quickly move the player along a path while they are teleporting. This is often used when the player is connected to an avatar that needs to move through the world to check for collisions. This can be uncomfortable, especially if done slowly. It is recommended to instantly speed the player up to the movement speed, and instantly stop moving them when they reach the destination, as velocity tends to be less troublesome than acceleration in terms of motion sickness. While doing this, introducing a screen vignette to darken or black-out the periphery also helps prevent motion sickness.

{{< video "https://xrinteractionlibrary.blob.core.windows.net/vrcaptures/teleportation/thelab-teleportation-interpolation-movement.mp4" nopreload >}}

*The Lab showing the player being linearly interpolated between the destinations. Also showing a form of zone-based teleportation.*

## Movement Trails
Particle effects, or a pre/post "dust trail" can help inform the user of the motion they just made. More importantly, it can inform other users in a multiplayer experience of what even happened. 

{{< video "https://xrinteractionlibrary.blob.core.windows.net/vrcaptures/teleportation/moor-teleport-movement-trails.mp4" nopreload >}}
*One player follows another easily in **The Museum of Other Realities** thanks to various trails (yellow leaves), "whooshes" (red action-lines), avatar movement, and destination marker indication.*

In multiplayer experiences, the teleporting player can "blink" to their destination while the avatar - for everyone else - linearly interpolates. I believe **Rec Room** uses such a system.

See the **Half + Half** system as well, which shows off the arc pre-teleport through a sling-shot animation.

## Head or Hand Control
Most teleportation systems use controller input for selecting where to look. This is effective for granular teleportation. When using zone-based teleportation, accuracy is not as critical, so long as the zone has a generous selection area. One can, instead of pointing the controller, just select the zone in the direction the player is looking. 

{{< video "https://xrinteractionlibrary.blob.core.windows.net/vrcaptures/teleportation/vacation-head-selection-location-display.mp4" nopreload >}}

*Zone based teleportation in Vacation Simulator. The destination is controlled by the players head position, not through controller pointing. Note there is more than just a destination marker: doors open and close automatically, the carpet changes color, and destination-specific sounds play.*

**Angry Birds: Isle Of Pigs** uses a Zone-based system. Each level only has a handful of zones. To select them, you just use a straight-line pointer. This works more effectively because you can point at a very wide area, and well above the zone marker itself, and the possible destination will still light up. It also is a smart design decision because the game, involving slingshots, is all about parabolas. If the teleportation system worked too similarly to the main mechanic of the game, it might confuse players who may not know which one they are about to do. The teleporter marker is clearly not the slingshot marker because it isn't a parabola.

### Gaze Limitation
Given the importance of ensuring the player will know where they will end up when teleporting, should a system limit a player from teleporting somewhere they are not looking? Using head/gaze for destination selection does this inherently, and is an advantage.

Yet, when using hand control, one should **not** limit the player to destinations in their field of view. Players will become proficient with the system, and you do not want to artificially lower the skill ceiling by limiting "advanced" moves like teleporting to a destination with the flick of a wrist. I believe in most cases players will feel more annoyed by this limitation than they will be confused if they accidentally press the teleport button.

### Use A Dedicated Button
Ensure that the trigger to teleport (the button) is always very clear. If it is a button on the controller, then ideally the button should only ever teleport the player, and not do anything else. This way the player avoids accidental teleports, and is unlikely to accidentally press it while looking away from the destination marker.

## Lessons From Headbanging
I once created a quick demo where the player teleported not on a button press, but by whipping their head in the direction they want to go ("headbanging"). It's **not** a good interface, but it's surprisingly not that bad either. The player's own head movement completely covers up the disorientation from the teleportation movement. The hands are completely free to manipulate/hold objects or do control something else. It's surprisingly intuitive (just imagine trying to point someone in a direction with both hands full of groceries), and it's fairly immune to players "spamming" the teleportation button, as teleporting multiple times in a row is inherently uncomfortable.

To be clear, I don't recommend "headbanging" teleportation for a number of accessibility, comfort, and safety reasons. Theres a risk to equipment, which could go flying off, and to faces, which could go flying towards walls. It's also difficult to calibrate when to teleport and when not to, as you want the teleportation to happen with as minimal head movement as possible without false positives. All that being said, the fact that such an absurd control method isn't as bad as it "should be" goes to show that teleportation is far from a "solved" problem in VR, and experimentation is still important.

## Play Area Overlay
One method for tackling the difficulty of granular teleportation for players is to show the player an outline of their play-area space while teleporting. While this does helps, it asks the player to be aware of their real-world space at all times.

I think it is a good idea to let such an outline be enabled in the settings, or automatically fade it in when it seems that the player may likely need the assistance, such as if they are teleporting multiple times without taking other actions, or the destination they are in the process of selecting would largely overlap the play area with out-of-bounds areas.

{{< video "https://xrinteractionlibrary.blob.core.windows.net/vrcaptures/teleportation/thelab-play-area-overlay.mp4" nopreload >}}
*An overlay of the player's play area boundaries are visible in **The Lab**.*

## Audio Considerations
OWLchemy labs discuss the importance of audio in the GDC talk linked below.

## Notes on Granular Teleportation
Granular Teleportation can be easier to implement than zone-based teleportation from a design perspective, but it is more challenging and asks for more attention from the user as a skill, which can lessen the sense of presence.

It is difficult for the user to know where they are in the real world, while still requiring them to be obliquely aware of such information in order to teleport effectively.

Granular teleportation tends to discourage physical movement. Users often just keep teleporting. This is immersion-breaking and makes building presence difficult. Yet sometimes this is crucial for accessibility, to work with users with limited or impaired mobility, and for players with small play-areas.

With granular teleportation, some users find a way to get themselves stuck with a disconnection between virtual and real spaces. For example, I have gotten myself into a situation where the real-world wall was right in front of me, and a virtual wall was right behind me. It was difficult to walk through the virtual wall in order to try and reset myself as the game went to black when moving through an object like the wall.

# Notes on Zone-Based Teleportation
Zone-based teleportation is easy for the user to understand and it can keep players away from real-world walls or from over-relying on teleportation. This allows presence to be built more easily. It is generally more difficult to design for and implement, especially in a situation where your level was not designed for VR, like an architecure sim or port of a video game.

One advantage of zone-based teleportation is you can teleport the "room", and not the "player position", preventing the player's play-area from ever becoming misaligned from the virtual play-area. This is a huge advantage, and a great reason to design environments for zone-based teleportation. 

{{< video "https://xrinteractionlibrary.blob.core.windows.net/vrcaptures/teleportation/vacation-teleport-to-zone.mp4" nopreload >}}

*Note how in Vacation Simulator, while selecting a teleportation destination, the destination marker will move as the player walks around. The 'room' is teleporting with the player in it.*

One disadvantage of zone-based teleportation is how one chooses to select the appropriate room while teleporting. Generally each zone would be connected to surrounding zones. One reason to do this is so that less zones are available to the player, and they won't accidentally select a zone "behind" the one they wanted to go to. This is especially important when using a head-position/gaze for selecting the destination zone, as it is less accurate.

{{< video "https://xrinteractionlibrary.blob.core.windows.net/vrcaptures/teleportation/vacation-teleport-along-graph-not-line-of-sight.mp4" nopreload >}}
Note how in the above Vacation Simulator clip, I can't teleport down to the water area from the deck, even though it is "right there". I have to "follow the path" through the building to get to the zone. It still feels like it *should* let me teleport there. The design of the level always has visual paths (literally: paths, steps, cobblestone, etc) to indicate valid nearby zones. There is no path connecting the deck to the water. Yet jumping off a deck into water feels perfectly natural even without a path.

## GDC Talk by OWLchemy Labs.
The following GDC Talk includes an excellent analysis of zone-based and granular teleportation systems.


{{< youtube q83f3sdQBBc >}}
