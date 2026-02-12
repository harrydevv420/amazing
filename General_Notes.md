Backtracking
BFS
Dfs
Parsing, config...
Maze rendring
Packaging
---------------------------------------------------------

Create your own maze generator and display its result!


# Introduction:
Maze generation is more than just fun: it’s a practical application of algorithms, randomness, and graph theory. Some famous algorithms used for maze generation — like __Prim’s__, __Kruskal’s__, or the __recursive backtracker__.
Perfect mazes (with one unique path between any two points) are
directly related to __spanning trees__ in __graph theory__.


# Common Instructions:

1. General Rules:
- Use try-except blocks to manage potential errors.
- Prefer __context managers__ for resources like files or connections to ensure automatic cleanup
- If your program crashes due to unhandled exceptions during the review, it will be considered non-functional.
- All resources (e.g., file handles, __network connections__) must be properly managed to prevent leaks. Use __context managers__ where possible for automatic handling.
- Your code must include __type hints__ for function parameters, return types, and vari- ables where applicable (using the __typing module__).
- Use __mypy__ for __static type checking__. All functions must pass mypy without errors.
- Include docstrings in functions and classes following __PEP 257__ (e.g., Google or NumPy style) to document purpose, parameters, and returns.

2. Makefile:
- Include a Makefile in your project to automate common tasks.
- It must contain the following rules (__mandatory lint__ implies the specified flags; it is strongly recommended to __try–strict__ for enhanced checking).
- **install**: Install project dependencies using pip, uv, pipx, or any other package manager of your choice.
- **run**: Execute the main script of your project (e.g., via Python interpreter).
- **debug**: Run the main script in debug mode using Python’s built-in debugger (e.g., pdb).
- **clean**: Remove temporary files or caches (e.g., __pycache__, .mypy_cache) to
keep the project environment clean.
- **lint**: Execute the commands flake8 and mypy.
--warn-return-any --warn-unused-ignores --ignore-missing-imports --disallow-untyped-defs --check-untyped-defs.
- **lint-strict** (optional): Execute the commands flake8 and mypy --strict


# Additional Guidelines:
- Create test programs to verify project functionality (not submitted or graded). Use frameworks like pytest or unittest for unit tests, covering edge cases.
- Include a .gitignore file to exclude Python artifacts.
- It is recommended to use virtual environments (e.g., venv or conda) for dependency isolation during development.



# Mandatory part:

1. Summary:
You will implement a __maze generator__ in Python that takes a __configuration file__, __generates a maze__, eventually perfect (with a single path between entrance and exit), and __writes it to a file__ using a __hexadecimal wall representation__. You will also provide a __visual representation of the maze__ and organize your code so that the generation logic can be reused later.

2. Usage:
- Your program must be run with the following command:
```python3 a_maze_ing.py config.txt```
- a_maze_ing.py is your main program file. You must use this name.
- config.txt is the only argument. It is a plain text file that defines the maze generation options. You can use a different filename.
- Your program must handle all errors gracefully:
invalid configuration.
file not found.
bad syntax.
impossible maze parameters, etc...
It must never crash unexpectedly, and must always provide a clear error message to the user.

3. Configuration file format:
- The configuration file must contain one ‘KEY=VALUE‘ pair per line.
WIDTH (Maze width (number of cells)) WIDTH=20
HEIGHT (Maze height) HEIGHT=15
ENTRY (Entry coordinates (x,y)) ENTRY=0,0
EXIT (Exit coordinates (x,y)) EXIT=19,14
OUTPUT_FILE (Output filename) OUTPUT_FILE=maze.txt
PERFECT (Is the maze perfect?) PERFECT=True
- You may add additional keys (e.g., seed, algorithm, display mode) if useful.
- A default configuration file must be available in your Git repository.

4. Maze Requirements:
- The maze must be randomly generated, but reproducibility via a seed is required.
- Each cell of the maze has between 0 and 4 walls, at each cardinal point (North, Est, South, West).
- The maze must be valid, meaning:
    - Entry and exit exist and are different, inside the maze bounds.
    - The structure ensures full connectivity and no isolated cells (except the ’42’ pattern).
    - As entry and exist are specific cells, there must be walls at the external borders.
    - Your generated data must be coherent: each neighbouring cell must have the same wall if any. E.g., it is forbidden to have a first cell with a wall on the east side, and the second cell behind that wall without a wall on the west side.
    - The maze can’t have large open areas. Corridors can’t be wider than 2 cells. For example, you can have 2x3 or 3x2 open area, but never a 3x3 open area.
- When visually represented (see below), the maze must contain a visible “42” drawn by several fully closed cells.
- If the PERFECT flag is activated, the maze must contain exactly one path between the entry and the exit (i.e., it must be a perfect maze).
NOTE: The “42” pattern may be omitted in case the maze size does not allow it (i.e. too small). Print an error message on the console in that case.

4. Output File Format:
- The maze must be written in the output file using one hexadecimal digit per cell, where
each digit encodes which walls are closed:
-----------------
Bit | Direction
-----------------
0   | (LSB) North
1   | East
2   | South
3   | West
-----------------

- A wall being closed sets the bit to 1, open means 0.
Example: 3 (binary 0011) means walls are open to the south and west. Or A (binary 1010) means that east and west walls are closed.
- Cells are stored row by row, one row per line.
- After an empty line, the following 3 elements are inserted in the output file on 3 lines:
the entry coordinates, the exit coordinates, and the shortest valid path from entry to exit, using the four letters N, E, S, W.
- All lines end with a \n.

Note: In conjunction with its specific configuration file, this output file could be tested automatically by a Moulinette. Also, a validation script is provided with this subject to control that the output file contains coherent data.

Output file example: Page 9.

# Visual representation:

- Your program must provide a way to display the maze visually, using either:
    • Terminal ASCII rendering, or:
    • A graphical display using the MiniLibX (MLX) library.

- The visual should clearly show walls, entry, exit, and the solution path.
- User interactions must be available, at least for the following tasks:
    • Re-generate a new maze and display it.
    • Show/Hide a valid shortest path from the entrance to the exit.
    • Change maze wall colours.
    • Optional: set specific colours to display the “42” pattern.
- You can add extra user interactions.
- Terminal default rendering of the maze (Page 11).

# Code reusability requirements:

- You must implement the maze generation as a unique class (e.g., ‘MazeGenerator‘) inside a standalone module that can be imported in a future project.
- You must provide a short documentation describing how to:
    • Instantiate and use your generator, with at least a basic example.
    • Pass custom parameters (e.g., size, seed).
    • Access the generated structure, and access at least a solution.

Note: The maze generator module grants access to the maze structure, but it is not necessarily the same format as the output file.

- This entire reusable module (code and documentation) must be available in a single file suitable for a later installation by pip.
- This package must be called mazegen-* and the file must be located at the root of your git repository.
- Both .tar.gz and .whl extensions are allowed, as generated by the standard build of a Python package.
Example of a full filename: mazegen-1.0.0-py3-none-any.whl.

- You must provide in you Git repository all needed elements to build the package. This will be asked during the evaluation: in a virtualenv or equivalent, install the needed tools and build your package again from your sources.
- The main README.md file (not part of the reusable module) must also contain this short documentation.

# Bonuses:

You may add various bonuses to your project. Here are possible examples:
• Support multiple maze generation algorithms.
• Add animation during maze generation.
