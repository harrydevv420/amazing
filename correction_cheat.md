# Basics:

__submitted files and Norm:__
Check if all expected files are present in the Git repository:
    - README.md
    - a_maze_ing.py
    - mazegen.tar.gz
    - a configuration file
    - all needed elements to build the maze generator package again Other files can be present. Also the flake8 Norm must pass on the python files, as well as mypy.
If any of the required elements is missing, the grade is 0.

__README.md file:__
Does the repository contain a README.md file at its root, and does it include all of the following?
    - The first line is italicized and formatted exactly as: This project has been created as part of the 42 curriculum by <login>, <login>.
    - A "Description" section explaining the project's purpose and providing a brief overview.
    - An "Instructions" section with relevant details about compilation, installation, and/or execution.
    - A "Resources" section listing external references (documentation, tutorials, etc.) and explaining how AI was used, specifying for which tasks and which parts of the project.
    - The complete description of the configuration file.
    - The chosen maze algorithm.
    - The reason of choosing this algorithm.
    - A short documentation about the maze generator reusable module.
    - The team and project management :
        * The roles of each team member.
        * Your anticipated planning and how it evolved until the end.
        * Wath worked well and what could be improved.
        * Have you used any specific tools? Which ones?
Other relevant sections / elements are allowed in this file.
If any of the required elements is missing, the grade is 0.





# Standard usage:

__Display:__
Run the a_maze_ing.py script, using a default configuration file.
You should get a maze randomly generated, displayed on the terminal or using a
dedicated graphic window, and a way to interact with the program.

__Interactive menu:__
Among the possible interactions, control that the mandatory ones are present:
    - Re-generate a new maze.
    - A toggle button to show and hide the shortest path from entry to exit.
    - A button to change the colours of the walls. Extra interactions are possible (e.g., changing the colour of the '42' pattern, quitting the program, ...).





# Configuration file:

__Format:__
Control that the configuration files follow the requirements:
    - Comments lines start with '#'.
    - Each line is in the 'KEY=VALUE' format (lower case is also OK).
    - The expected keys are present (WIDTH, HEIGHT, ENTRY, EXIT, OUTPUT_FILE, PERFECT).

__Error Management:__
Edit the configuration file to ensure that the program correctly handles its errors:
    - Remove a mandatory key.
    - Add a line that does not respect the 'KEY=VALUE' format (e.g., without the '=' sign).
    - Replace numbers by letters.
    - Use an incorrect boolean parameter for 'PERFECT'.
    - Use a wrong format of int tuple for 'ENTRY' or 'EXIT'. Reminder: in case of unexpected end of the program, the evaluation stops and final grade is 0.





# Output file:

__Format:__
Run the a_maze_ing.py script and verify that the first generated (and displayed) maze is also stored in the defined output file. You should find:
    - 'HEIGHT' lines of 'WIDTH' chars each,
    - an empty line,
    - the 'ENTRY' tuple,
    - the 'EXIT' tuple,
    - the shortest path from entry to exit described using directions 'N', 'E', 'S', 'W'. Use the validation script provided with the subject to control the walls coherence. Control that the shortest path sequence in the output file matches its visual representation. Any error will mark this question as failed.





# Maze Generator module:

__Maze generation:__
The maze generator module follow the subject's expectations:
    - A randomly generated maze, eventually using a suitable standard module of Python (e.g., the module 'random').
    - Adopt a relevant behaviour in case some parameters may be inconsistent (e.g., the entry or exit cells are outside the maze, width or height is negative, ...).
    - All cells can be reached, except, eventually, those creating the '42' pattern.
    - Have walls all around the maze.
    - There is no 3x3 or larger open zone without walls. Ask how this was implemented or verified in the code.
    - There is the '42' pattern in the maze (except is size does not allow it, then you should have a message on the terminal).
    - A perfect maze if the 'PERFECT' key in the configuration file is set to True.
    - The same maze is replicable when using an identical seed (update the configuration file or the code to verify). Are all these expectations fulfilled?

__Reusable module:__
Have the evaluated student/team re-generate the package, most preferably in a virtualenv or similar.
This must re-create the mazegen-*.tar.gz or .whl file.
Then, in a different virtualenv or similar, install the newly created package, and test it with the a_maze_ing.py script and its
configuration file.
Is everything working properly?





# Bonuses:
__Do you want more?__
The bonuses can only be considered if all the previous questions were successful.
You can validate up to 5 different working bonuses. Each bonus must represent a fair amount of work.
Possible ideas:
    - Support multiple maze generation algorithms.
    - Add animation during maze generation.
