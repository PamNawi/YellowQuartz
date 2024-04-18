Tags: #BindingOfIsaac #ProceduralGeneration #DungeonGeneration
<h2>Question: </h2>
What is the difference between the original version and the rebirth version for the procedural generation

<h2>Answer:</h2>
They added 11 large rooms: 2x2, 2x1, L-shaped, and narrow corridors in different rotations.

Instead of looping over the cardinal directions, it loops over all exits of a room instead. There can up to on a 2x2 room.

When it comes to inserting a room, it randomly tries to use a big room instead. The neighbour check still only applies to the first cell, but it does check that there's empty space for the rest of the room. This cause that big rooms create some loops in the level. Its common for two large rooms be generated side by side looping between each other.

If there's no space for a big room, another candidate is tried. 

When large rooms are successfully inserted, there's a 95% they are removed from the pool.

Large boss rooms need better treatment: The boss rooms are always placed as far as possible from the starting room. If a large room is desired, the generator replaces the designated single room.

<h2>Highlight:</h2>
- Larger rooms create some loops in the floor plan
<h2>Reference: </h2>
https://www.boristhebrave.com/2020/09/12/dungeon-generation-in-binding-of-isaac/