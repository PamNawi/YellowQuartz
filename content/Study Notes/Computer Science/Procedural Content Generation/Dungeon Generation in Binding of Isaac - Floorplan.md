---
tags:
  - "#BindingOfIsaac"
  - ProceduralGeneration
  - DungeonGeneration
  - LevelDesign
  - "#Question"
---
# **Question:** How Binding of Isaac does their dungeon generation?

There's a number of square rooms that are connected adjacently to each other, some of this rooms are special: shops, rewards and boss rooms and with the exception of the secret room, there's no loops in the dungeon.

The level is generated on a 9 x 8 grid and convenience the cells are numbered, with unit digits indicating their x position and the tens digit indicating their y position. This means that is possible to move up, down, left and right by just adding +10, -10, +1 or -1. The cells swith x position of 0 are unused, which means that most of the code, don't worry about the boundaries of the map. so the top left cell of the map is 01 and the bottom right is 79.

The floor plan decides which cells will contain rooms and the content of the room is decided later.

The number of rooms is determined by random(2) + 5 + level * 2.6, meaning that levels starts with 7 or 8 rooms and are increase by 2 or 3 each time.

The game then places a starting room at cell 35, then it loops over the queue, it loops over the 4 cardinal directions and does the following:
	- Determine the neigbour cell by adding +10/-10/+1/-1 to the currency cell
	- If the neighbour cell is already occupied, give up
	- If the neighbour cell itself has more than one filled neighour, give up
	- If already have enough rooms, give up
	- Random 50% chance, give up
	- Otherwise, mark the neighbour cell as having a room in it, and add it to the queue

If a cell don't add a room to any neighbours, it's a dead end, and it can be added to the list of end rooms for later use.

In the case of maps needing more than 16 rooms, the starting room is reseeded into the queue periodically to encourage more growth

Essentially is a breadth first exploration. The restriction that it won't add a room which already has 2 neighbors, keeping the rooms in separated corridors that never loop around. The floorplan is then checked for consistency. It must have the right number of rooms and the boss room cannot be adjacent to starting room.

## Curse of the Labyrinth 
These are a double sized maps that occur randomly. Aside from the obvious duplication of special rooms, and two adjacent boss rooms, there's small details too:
- 80%+ more normal rooms (max 45)
- Only use the 6 furthest away end rooms for special rooms
- It pulls from easy, medium and hard pools
- Randomly add extra normla rooms to the floorplan with similar placement logic to the secret room.

## Highlight:
- Its a breadth first exploration with some restrictions to guarantee that no looping will occur, the number of rooms is correct and the boss room is far from the beginning room.

## Reference:
- https://www.boristhebrave.com/2020/09/12/dungeon-generation-in-binding-of-isaac/