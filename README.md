# Goal Oriented Actions Planning System (GOAP)
## Overall Design
The basic game level is a bounded rectangular area, styled as an outdoor terrain with a random, but relatively sparse distribution of trees and some garbage cans as well. Tree and garbage can locations are different on each playthrough, non-overlapping. There are 10 trees and5 garbage cans, while still allowing easy navigation through the area. A first-person view for the player character is provided.

Trees spawn nuts on the ground (non-overlapping) near them, about one every 2s and up to a maximum of 5 nuts at any one time in order to maintain a finite, (slowly) replenished supply. Garbage cans can be in either full or empty states, with their state initialized randomly. Once every 10s garbage cans may change state, provided no squirrels are in them (see below). The empty garbage can is yellow and full garbage can is red.

The terrain is populated with 5 squirrels, each of which is controlled by its own goal-oriented AI system. Each squirrel is associated with (and initially spawned at) a unique tree (its home tree). Squirrels generally explore and exhibit some kind of simple idle behaviour, gather food (either nuts or whatever they find in garbage cans) which they bring back to their home tree, and practice self-preservation by running away from a player who gets too close. Squirrels can observe their current state of the world around them (visual range is up to you) and retain limited memory of past observations, remembering only the locations of the last 5 nuts they observed, the current closest (based on Euclidean distance) tree, and the last 2 garbage cans. Squirrels cannot distinguish between empty and full garbage cans (without actually investigating them).

The squirrel AI will be based on GOAP. An appropriate world state and set of actions with corresponding pre/post-conditions that allow the squirrels to build plans that achieve their goals are fairly defined. The overall design enable the following behaviours.

• Two idle behaviours, involves roaming/exploring randomly.

• The ability to pick up nuts and bring them back to their home tree. Squirrels are only able to hold at most 3 nuts at one time, and must reach the home tree in order to drop the nuts.

• They sometimes gather food from garbage cans (at most one squirrel at a time). If the can is empty they remain stuck in the can for 2s, and if the can is full then they immediately acquire the food and the can is set to empty. Squirrels can only hold 1 unit of garbage at a time, may not combine that with nuts, and also must reach the home tree in order to deposit the food.

• If the player comes too close (choose a reasonable distance) they immediately flee, seeking refuge in a tree until the player is further away. No more than one squirrel can be in a given tree at the same time.

The player impacts the AI since squirrel’s run away. Pressing the space-bar should toggle the player in/out of a ghost-mode, during which the squirrels ignore the player. In ghost-mode, the player can create or destroy nuts or toggle the state of a garbage can by clicking on an empty spot on the ground or on a nut or an unoccupied can respectively.
