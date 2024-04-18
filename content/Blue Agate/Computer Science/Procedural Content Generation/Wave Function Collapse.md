Tags: #WaveFunctionCollapse #ProceduralGeneration #DungeonGeneration
<h2>Question: </h2>
What is Wave Function Collapse (WFC)?
<h2>Answer:</h2>
Is a contraint problem with a twist with thousands of possible solutions. The idea is that if we make our guesses at random, instead of getting a solver, we ge a generator.

The objective is to fill a grid with tiles such that nearby tiles connect to each other. Each tile is a different value, and each cell in the grid is a variable representing the choice of of tile. the rules about which tiles can be placed are the constraints! With a reasonable choice of tiles, and a sensible randomization routine, rarely is necessary to backtrack so is possible to skip implementing that. The algorithm works as follows:
- For each cell, create a boolean array representing the domain of that variable. The domain has one entry per tile, and they are all initialized to true. A tile is in the domain if that entry is true.
- While there are still cells that have multiple items in the domain:
	- Pick a random cell using the "least entropy" heuristic.
	- Pick a random tile from that cell's domain, and remove all other tiles from the domain
	- Update the domains of the other cells based on this new information (propagate cells). This needs to be done repeatdly as changes to those cells may have further implications.

<h3>Least Entropy:</h3>
Some choices are better thant others when picking the next tile to fill. We want to pick cells that are least likely to cause trouble later. Pick the cell with the fewest possible values ramaining in the domain. This is a good choice because:
	- Likely to be near other filled cells
	- If we leave it until later, it could be a trouble as there are already few possibilities.

If all tiles have the same just pick the tile with the smallest domain. But if the tiles are being choosen based on a weighted random distribution, is recomended to select a cell that minimizes:

entropy = - sum(p_i * Log(p_i) )
<h2>Highlight:</h2>
- Its a method that uses constraint programming to create a generator and not a solver for tilemaps.
	- Each cell in the grid is a variable
	- The domain of each variable is a set of possible tiles for that cell
	- The constraints are the rules on how each cell should be picking a tile
	
<h2>Reference: </h2>
https://www.boristhebrave.com/2020/04/13/wave-function-collapse-explained/
There's a GDC about it: https://www.youtube.com/watch?v=AdCgi9E90jw

<h2>Internal Links:</h2>
#ContraintProgramming