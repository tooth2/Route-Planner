# Open Street Map Route-Planner
Using OpenStreetMap data and look at IO2D map display code by extending the IO2D map display code to use A*,
to find a path between two points on the map. When the user selects starting and ending areas on a city map, and it will find
a path along the city streets to connect the start and end.

- A route planner that plots a path between two points on a map using real map data from the OpenStreeMap project

## Background - OpenStreetMap
The OpenStreetMap project is an open source, collaborative endeavor to create free, user-generated maps of every part of the world. These maps are similar to the maps like Google Maps or the Apple Maps app, but they are completely generated by individuals who volunteer to perform ground surveys of their local environment.
OpenStreetMap data can come in several different formats. The data that is used for this project comes in the form of an OSM XML file (.osm file).

### OSM(OpenStreetMap) Data Format
OSM XML File is mainly composed of three important XML type elements; Nodes, Ways, and Relations.
* Node
    * one of the most basic elements in the OpenStreetMap data model. e.g. A single point on the bus route. 
    * Each node indicates a single point with an identifier id, latitude lat, and longitude lon.  
* Way 
    * An ordered list of nodes that represents a feature in the map. e.g. A collection of roads the form the entire route.  
    * Each way has at least one tag which denotes some information about the way, and each way also belongs to at least one relation.
* Relation: 
    * a data structure which documents a relationship between other data elements 
    * A route relation: A collection of points that form a road on the bus route
    * A multipolygon: an area with holes, where the outer and inner boundaries of the area are given by two ways.

## Code Structure
The src directory contains the following files:
```
root
|--src
|   |--main.cpp
|   |--model.h and model.cpp
|   |--render.hand render.cpp
|   |--route_model.h and route_model.cpp
|   |--route_planner.h and route_planner.cpp
|--build: contains some .cmake files stating necessary libraries.  
|--test: contains unit tests, implemented using the Google Test framework
|--thirdparty: third party libraries included with this project
```
### RoutePlanner implementation
![route_planner](route_planner.png)

- A RouteModel object is created to store the OSM data in usable data structures.
- A RoutePlanner object is created using the RouteModel. This planner will eventually carry out the A* search on the model data and store the search results in the RouteModel.
- The RouteModel data is rendered using the IO2D library.
- The model.h and model.cpp files come from the IO2D example code. 
- the model.h file, as the method implementations in model.cpp : These files are used to define the data structures and methods that read in and store OSM data. OSM data is stored in a Model class which contains nested structs for Nodes, Ways, Roads, and other OSM objects. 
- RouteModel: These files contain classes which are used to extend the Model and Node data structures from model.h and model.cpp using class inheritance. Remember that inheritance in this case will allow you to use all of the public methods and attributes of the Model class and Node struct in the derived RouteModel and RouteModel::Node classes.
The reason for extending the existing Model class and Node struct is to include additional methods and variables which are useful for A* search. In particular, the new RouteModel::Node class now allows nodes to store the following:
    - the h-value,
    - the g-value,
    - a "visited" flag, a vector of pointers to neighboring nodes.
- The render.h and render.cpp files come from the IO2D. These take map data that is stored in a Model object and render that data as a map including three methods which render the start point, end point, and path from the A* search

### User Input 
- A user should be able to input values between 0 and 100 for the start x, start y, end x, and end y coordinates of the search, and the result shows a path between the points.
- The coordinate (0, 0) should roughly correspond with the lower left corner of the map, and (100, 100) with the upper right.
### Result 
|(5,5,75,75)| (5,5,45,50)|
|--|--|
|<img src="compile.png" width=400 />)|<img src="test.png" width=400 />|
|![2](route2.png)| ![5](route5.png)| 
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

## Reference
- [Open Street Map](https://www.openstreetmap.org/)
- [2D Graphics library : IO2D](https://github.com/cpp-io2d/P0267_RefImpl/tree/master/P0267_RefImpl/Samples/maps)
