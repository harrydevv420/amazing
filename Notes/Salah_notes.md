# Definitions:

#### - Graph theory: 
Graph theory is a branch of mathematics that studies graphs, a mathematical structure for modelling pairwise relations between objects. The definition of a graph can vary, but one can understand that a graph is a structure that contains the vertices (also called nodes or points) and edges (also called arcs, links, or lines). 
Two vertices of an edge are called the endpoints.
### - Perfect mazes -> one unique path between any two points
---- (shoutout to [**Spanning tree**](https://en.wikipedia.org/wiki/Spanning_tree))


### Some famous algorithms:
- [Prim](https://en.wikipedia.org/wiki/Maze_generation_algorithm#Iterative_randomized_Prim's_algorithm_(without_stack,_without_sets))
- [Kruskal](https://en.wikipedia.org/wiki/Maze_generation_algorithm#Iterative_randomized_Kruskal's_algorithm_(with_sets))
- [recursive backtracker](https://en.wikipedia.org/wiki/Maze_generation_algorithm#Recursive_implementation)

## Why I need to setup Virtual Environment in python?:
A virtual environment should be used for every Python project. By default, all Python projects share the same location to store packages. This can cause problems if two projects need different versions of the same package, like Django. A virtual environment solves this by creating a separate space for each project’s packages, so they don’t interfere with each other. It’s basically a folder with its own Python setup. Using a virtual environment helps avoid conflicts and keeps your projects clean and organized
- Avoid Dependency Conflicts
- Isolate Project Environments
- Simplifies Project Management
- Prevents System Interference
- Enables Reproducibility.

**Ps: but in our case we don't have root so it will not work! (i asked Othmane about this) which means not needed**

### Makefile in python:
#### Installing packages:
```python
.PHONY: install_deps
install_deps:
    pip install numpy pandas etc
```
#### Building Python Projects:
```python
.PHONY: build
build:
    python setup.py sdist bdist_wheel
```
#### Testing code:
```python
.PHONY: test
test:
    python -m unittest discover
```


#### first impreation:
playing around with mlx! feels nice already! lets goo