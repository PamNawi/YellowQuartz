---
tags:
  - BindingOfIsaac
  - ProceduralGeneration
  - DungeonGeneration
  - LevelDesign
---
# How each room is choose to be placed?

## Special rooms
- Boss rooms are placed by reading the last item from the end room list from the floorplan.
- The generator searchs for an empty cell that is next to at least three rooms and not next to any end rooms. If doesn't find one after 300 attempts, it loosens the criteria a bit, and after 600 attempts loosens it even futher. This procedure ensures that the secret room will always be placed, but generally they are wedged near intersections so they are next to a lot of rooms.
- Nearly all other special rooms are placed at a random end room. Some will be guaranteed to spawn, others will have a small chance.

## Normal Rooms
- Rooms are randomly picked from a pool. Rooms include both the layout and the monsters. Both are subject to random variations like champion monsters, tinted rocks and red fireplaces.

- For normal rooms, there's 3 pools of rooms : easy, medium and hard.
	- The first stage draws from easy and medium
	- The second stage from medium hard
	
- The first chapter, the basement, has 174 normals rooms in the pools. 
- The "alternative chapters" such as cellar can replace the basement randomly and have a slightly different set of rooms.

## Highlight:
- First place all the special rooms following the rules for each kind
- After that the normal rooms are placed by picking from a pool depending of the level difficult

## Reference:
https://www.boristhebrave.com/2020/09/12/dungeon-generation-in-binding-of-isaac/