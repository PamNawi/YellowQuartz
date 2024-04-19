Tags: #Spelunky #ProceduralGeneration #DungeonGeneration #LevelDesign 
<h2>Question: </h2>
How spelunky level generation works?

<h2>Answer:</h2>
Each level is composed by a 4x4 grid with 4 different types of rooms:
0 : a side room that is not on the solution path
1: a room that is guaranteed to have a left exit and a right exit
2: a room that is guaranteed to have exits on the left, right and bottom. If there's another "2" room above it, then it also is guaranteed a top exit
3: a room that is guaranteed to have exists on the left, right and top.

- The first thing it does is place a "start room" in the top row. The room type don't matter at this stage. 
- Every time a room is placed, is always a type 1 (left/right)
- Decides where to go next using a random number from 1 to 5:
	- 1 or 2: The solution path moves left
	- 3 or 4: The solution path moves right
	- 5 : The path goes down
	- If the solution path hits the edge of the screen, then immediately goes down and switch to left/right direction

If the algorithm decides to move left or right, everything is fine, because we placed down a room with guaranteed left/right exits. But if we've decided to move down, we need to change the current room to be a type 2 and then move down.

When move into the next room, it asks whether the last room placed was a type 2 (bottom drop), if is true, then this room _has_ tobe another type 2 or 3.

If we are on the bottom row of the level and we try to drop, its placed a exit room.

After the solution path is generated, then the every other cell on the grid that is not inside the solution it turns into a 0 type room. This algorithm generate some rooms that don't have any exit.

If there's a 3 or 4 rooms with type 0 making a vertical line, then there's a chance that rooms will become a snake pit. If they turn into a snake pit, you gonna se a sequence made from bottom to top of 7 8 9 or 7 8 8 9. The enemies and the jewels are placed manually by the devs.

<h2>Highlight:</h2>
- Its based on a grid system that creates a solution path with a garantee path for the players with a starting and ending point.
- Some of the rooms was handcraft and the algorithm place then at the final step

<h2>Reference: </h2>
http://tinysubversions.com/spelunkyGen/