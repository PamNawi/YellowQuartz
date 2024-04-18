Tags: #Spelunky #ProceduralGeneration #RoomGeneration
<h2>Question: </h2>
How spelunky generate each individual room inside a level?

<h2>Answer:</h2>
Spelunky has four basic room types. Each room type has typically 8 to 16 templates that it chooses from. A template is a layout made by a 10x8 grid of tiles 
defining the overall room layout.  Each tile inside a template can be static and probabilistic, as well a obstacle block. 
- 0 means empty space
- 1 means 100% chance of a solid block
- L means a ladder
- P is the top of ladder

Static tiles are just it, a static, non-movable and solid block
Probabilistic tiles have a chance to have that block or not, like this examples:
	- 4 means there's a 25% chance of a pushblock at the top of the ladder
	- There is a 33% chance of spike here
	- There's a 50% of empty space or solid block here

Obstacle blocks is a 5x3 tile block that generally forms some kind of interesting structure for the player to manuever around. Obstacle blocks are often comprised of probabilistic tiles.

Another important thing to notice is that some of the rooms are randomly mirroed left/right. Most of the time you won't notice this because most rooms are symmetrical.
<h2>Highlight:</h2>
- Each room follows a predefined template made with a grid of tiles.
- There's a bunch of templates for each room, to keep variability and these templates was handcrafted

<h2>Reference: </h2>
http://tinysubversions.com/spelunkyGen2/