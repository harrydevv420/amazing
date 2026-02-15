# Phase 1: Environment & Architecture Setup:
Before writing logic, ensure your development environment meets the strict submission standards.

- [DONE] Initialize Git Repository: Create a root directory.
- [DONE?] Create .gitignore: Exclude __pycache__, *.pyc, .venv, .mypy_cache, and build//dist/ directories.
- [Negative] Set up Virtual Environmen:
    [Negative] Create a venv (python3 -m venv .venv).
    [Negative] Activate it. (check my notes)
- [Done] Create the Makefile:
    [Done] Implement the mandatory rules:
    [Done] install: Run pip install . or pip install -r requirements.txt.
    [Done] run: python3 a_maze_ing.py config.txt.
    [Done] debug: python3 -m pdb a_maze_ing.py config.txt.
    [Done] clean: Remove cache folders and build artifacts.
    [Done] lint: Run flake8 and mypy with the required flags (--warn-return-any, etc.).
- [Done] Install Dev Tools: Install flake8, mypy, and build (for packaging).

# Phase 2: The Reusable Module (mazegen):
You must build the generator as a standalone library first. This is the "Code reusability" requirement.

- [ ] Folder Structure: Create a folder named mazegen (or similar) with an __init__.py.
- [ ] Define MazeGenerator Class:
    Initialize with width, height, seed.
    Use a grid data structure (e.g., 2D list or NumPy array) to store cell states (walls).
- [ ] Implement Wall Bitmasking:
    Define constants: NORTH=1, EAST=2, SOUTH=4, WEST=8.
    Helper functions to check/set walls using bitwise operations (|, &, ^).
- [ ] Implement Generation Algorithm (Recursive Backtracker recommended):
    This algorithm naturally creates a "Perfect" maze (Spinning Tree).
    Implement a stack-based approach to avoid Python recursion depth limits on large mazes.
[ ] Implement the "42" Feature:
    Create a hardcoded binary mask or coordinate set representing the number "42".
    Logic to overwrite the center of the maze with these "fully closed" cells.
    Crucial: Ensure the maze remains connected around the "42" block (the algorithm shouldn't get stuck entering the closed block).
[ ] Implement Pathfinding (Solver):
    Implement BFS (Breadth-First Search) or A* to find the shortest path from Entry to Exit.
    Return the path as a list of coordinates or directions.
[ ] Coherency Check: Ensure if Cell A has a South wall, Cell B (below A) has a North wall.

# Phase 3: Packaging:
The module must be installable via pip.

[ ] Create pyproject.toml or setup.py:
    Define metadata (name=mazegen-yourname, version=1.0.0).
[ ] Build the Package:
    Run python3 -m build.
    Verify .whl and .tar.gz are created in dist/.
[ ] Write Module Documentation:
    Create a README specific to the library explaining how to import and use MazeGenerator.

# Phase 4: The Application (a_maze_ing.py):
This is the script that uses your library to satisfy the subject requirements.

[ ] Config Parsing:
    Read config.txt.
    Parse KEY=VALUE pairs.
    Error Handling: Raise clear errors for missing keys, non-integers, or invalid coordinates.
[ ] Argument Validation:
    Ensure Entry/Exit are within bounds.
    Ensure maze size accommodates the "42" pattern (if not, print warning as requested).
[ ] Integration:
    Import your mazegen module.
    Instantiate the generator with config values.
[ ] Output File Generation (hex format):
    Convert internal cell representation to the specific Hex format requested.
    Write the grid row by row.
    Append Entry, Exit, and Solution Path (N, E, S, W strings) at the end.
[ ] Context Managers: Use with open(...) for all file I/O.

# Phase 5: Visualization & Interaction
You need a visual interface. The Terminal (Curses or Standard Out with loop) is usually easiest for Python unless you are comfortable binding C-MiniLibX to Python (rare/difficult).

[ ] Render Logic:
    Map wall bitmasks to ASCII characters (e.g., ██, __, |).
    Draw the "42" blocks distinctively.
    Highlight the Solution Path.
[ ] Interactive Loop:
    Wait for user input.
    Key R: Re-seed and re-generate.
    Key S: Toggle solution visibility.
    Key C: Cycle colors (using ANSI escape codes).
    Key Q or ESC: Exit cleanly.


# Phase 6: Quality Assurance (QA):

[ ] Type Checking: Run mypy --strict . and fix all red squiggles.
[ ] Linting: Run flake8 to ensure PEP 8 compliance.
[ ] Crash Testing:
    Test with a non-existent config file.
    Test with a config file containing garbage text.
    Test with a 5x5 maze (too small for "42" -> check error message).
[ ] Documentation: Ensure all functions have Google/NumPy style docstrings.

- Technical Concept: The Hex Bitmask:
Since the subject requires specific Hex output, pay close attention to the bit order.
Requirement: 0 (LSB) North, 1 East, 2 South, 3 West.
Example: Binary 0011 (Decimal 3) = North(1) + East(1) = Walls on North and East. Open on South and West.
When writing your hex writer:
def cell_to_hex(cell_value: int) -> str:
    # Format as uppercase hex, strip the '0x' prefix
    return format(cell_value, 'X')

- Visual Concept: The "42" Pattern:
To satisfy the "42" requirement without breaking the maze connectivity, treat the "42" cells as "Walls" in your grid before running the maze generation algorithm.
Initialize grid with all walls.
Mark the cells corresponding to "42" as "Permanent Walls" (visited).
Run the Recursive Backtracker. It will carve paths around the "42" but will treat those cells as already visited boundaries, naturally embedding the shape into the maze walls.
