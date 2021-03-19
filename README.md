# Open Street Map Route-Planner
Using OpenStreetMap data and look at IO2D map display code by extending the IO2D map display code to use A*,
to find a path between two points on the map. When the user selects starting and ending areas on a city map, and it will find
a path along the city streets to connect the start and end.

- A route planner that plots a path between two points on a map using real map data from the OpenStreeMap project

## Code Structure
The src directory contains the following files:
``₩
root
|--src
|   |--main.cpp
|   |--model.h and model.cpp
|   |--render.hand render.cpp
|   |--route_model.h and route_model.cpp
|   |--route_planner.h and route_planner.cpp
|--build
|--test
```
The main.cpp controls the flow of the program, accomplishing four primary tasks:

- The OSM data is read into the program.
- A RouteModel object is created to store the OSM data in usable data structures.
- A RoutePlanner object is created using the RouteModel. This planner will eventually carry out the A* search on the model data and store the search results in the RouteModel.
- The RouteModel data is rendered using the IO2D library.

## A* search implementation


## User Input 
- A user should be able to input values between 0 and 100 for the start x, start y, end x, and end y coordinates of the search, and the result shows a path between the points.
- The coordinate (0, 0) should roughly correspond with the lower left corner of the map, and (100, 100) with the upper right.

### Dependencies for Runtime Environment
* [cmake >= 3.11.3](https://cmake.org/install/)
* [make >= 4.1](https://developer.apple.com/xcode/features/)
* [gcc/g++ >= 7.4.0](https://developer.apple.com/xcode/features/)
* [MinGW](http://www.mingw.org/)
* [IO2D](https://github.com/cpp-io2d/P0267_RefImpl/blob/master/BUILDING.md)

### Running
The executable will be placed in the `build` directory. From within `build`, you can run the project as follows:
```
./OSM_A_star_search
```
Or to specify a map file:
```
./OSM_A_star_search -f ../<your_osm_file.osm>
```

### Reference
- [2D Graphics library : IO2D](https://github.com/cpp-io2d/P0267_RefImpl/tree/master/P0267_RefImpl/Samples/maps)
