
#### Step 1: Create the Project Directory
+ **Action**: Create a dedicated project directory (e.g., `python_basics`) and navigate to it.
```
mkdir -p /Users/william/Source/Python/ProjectName/piython_basics
cd /Users/william/Source/Python/ProjectName/python_basics
```
+ Notes: Starting with a clean directory ensures no unrelated files are included. The ==`-p`== flag in ==`mkdir`== creates parent directories if they don’t exist (e.g., ==`ProjectName`==).
#### Step 2: Initialize Git Repo
+ **Action**: Run ==`git init`== to create a Git repository.
```
git init
```
+ Parameter Explanation: 
	+ ==`git init`==: Creates a ==`.git/`== directory, initializing an empty Git repository.  No additional parameters are needed for a basic setup.
+ **Why First**: Initializing a Git before creating the virtual environment or source files sets up version control early, allowing you to track all subsequent changes (e.g., adding ==`.gitignore`==, ==`iterators.py`==). This reduces the risk of missing initial files.

#### Step 3: Create ==`.gitignore`==
+ **Action**: Create a ==`.gitignore`== file to exclude the virtual environment and other Python-related files.
```
echo -e "basics/\n__pycache__/\n*.pyc\n*.pyo\n*.pyd\n*.log\n*.egg-info/\n*.dist-info/\n.env\n.venv/" > .gitignore
```
+ Parameter Explanation:
	+ ==`echo -e`==: Enables interpretation of escape characters (e.g., ==`\n`== for newlines) to write multiple lines to ==`.gitignore`==.
    - ==`> .gitignore`==: Overwrites or creates ==`.gitignore`== with the specified content.
- **Why**: Adding ==`.gitignore`== immediately after ==`git init`== ensures that files like ==`basics/`== are ignored from the start, preventing accidental staging with ==`git add .`==. The listed patterns cover:
    - ==`basics/`==: Your virtual environment folder.
    - ==`__pycache__/`==, ==`.pyc`==, ==`.pyo`==, ==`.pyd`==: Python bytecode files.
    - ==`.log`==: Log files.
    - ==`.egg-info/`==, ==`.dist-info/`==: Package metadata.
    - ==`.env`==, ==`.venv/`==: Common names for virtual environments or environment variable files.
- **Alternative**: Use a text editor (e.g., ==`nano .gitignore`==) or a ==`.gitignore`== template for Python from GitHub (e.g., GitHub’s Python ==`.gitignore`==).

#### Step 4: Commit ==`.gitignore`==
+ **Action**: Stage and commit ==`.gitignore`== to track it in Git.
```
git add .gitignore
git commit -m "Add .gitignore for Python project"
```
+ Parameter Explanation:
	+ ==`git add .gitignore`==: Stages the ==`.gitignore`== file.
    - ==`git commit -m`==: Commits staged files with a message (e.g., ==`"Add .gitignore for Python project"`==).
- **Why**: Committing ==`.gitignore`== early ensures that ignore rules are versioned and shared with collaborators, preventing ==`basics/`== from being tracked.

#### Step 5: Create the Virtual Environment
+ **Action**: Create the virtual environment using ==`python3`==.
```
python3 -m venv basics
```
+ Parameter Explanation:
	+ ==`-m venv`==: Runs the ==`venv`== module to create a virtual environment named ==`basics`==.
    - ==`python3`==: Ensures Python 3 is used, as discussed previously (necessary on macOS/Linux where ==`python`== may point to Python 2).
- **Why After Git**: Creating the virtual environment after ==`git init`== and ==`.gitignore`== ensures ==`basics/`== is ignored by Git. This order prevents accidental inclusion if you run ==`git add .`== later.

#### Step 6:  Activate the Virtual Environment and Set Up ==`pip`==
+ **Action**: Activate the virtual environment and upgrade ==`pip`==.
```
source basics/bin/activate
pip install --upgrade pip
```
+ Parameter Explanation:
	+ ==`source basics/bin/activate`==: Activates the ==`basics`== virtual environment on macOS/Linux, modifying the ==`PATH`== to use ==`basics/bin/python`== and ==`basics/bin/pip`==.
    - ==`--upgrade`==: Upgrades ==`pip`== to the latest version for compatibility with packages.
- **Why**: Activating the virtual environment ensures all ==`pip`== commands affect only the ==`basics`== environment. Upgrading ==`pip`== avoids issues with package installations.

#### Step 7:  Install Initial Packages and Create ==`requirements.txt`==
+ **Action**: Install your packages (e.g., ==`scipy`==, ==`requests`==, etc.) and ==`generate requirements.txt`==
```
pip i scipy requests numpy pandas matplotlib seaborn scikit-learn pytest
pip freeze > requirements.txt
```
+ Parameter Explanation:
	+ ==`pip i`==: Installs the listed packages into ==`basics/lib/python3.x/site-packages`==.
    - ==`pip freeze`==: Outputs installed packages and their versions.
    - ==`> requirements.txt`==: Writes the output to ==`requirements.txt`== for reproducibility.
- **Why**: Installing packages early sets up the environment for development. ==`requirements.txt`== documents dependencies, making it easy to recreate the environment later or share with others.

#### Step 8:  Commit ==`requirements.txt`==
+ **Action**: Stage and commit ==`requirements.txt`==
```
git add requirements.txt
git commit -m "Add initial dependencies in requirements.txt"
```
+ **Why**: Tracking ==`requirements.txt`== ensures collaborators can install the same packages with ==`pip i -r requirements.txt`==.

#### Step 9:  Create Source Files
+ **Action**: Create your Python files (e.g., ==`iterators.py`==).
```
touch iterators.py
```
+ **Why Last**: Creating source files after setting up the virtual environment and Git allows you to immediately test code with the correct Python version and libraries. It also ensures ==`iterators.py`== is tracked by Git from its creation.

#### Step 10:  Add and Commit Source Files
+ **Action**: Stage and commit ==`iterators.py`==.
```
git add iterators.py
git commit -m "Add initial iterators.py script"
```
+ **Why**: This tracks your code, keeping the repository up-to-date as you develop.

#### Workflow Reasoning
1. **Prevents Accidental Commits**:
    - By creating ==`.gitignore`== immediately after ==`git init`==, you ensure ==`basics/`== is never staged, even if you use ==`git add .`== carelessly.
2. **Sets Up Git Early**:
    - Initializing Git before creating the virtual environment or source files allows you to track all project files (e.g., ==`.gitignore`==, ==`requirements.txt`==, ==`iterators.py`==) from the start, improving version control history.
3. **Establishes Dependencies First**:
    - Creating the virtual environment and installing packages before writing code ensures ==`iterators.py`== can use libraries like ==`scipy`== immediately, reducing setup errors.
4. **Clear Structure**:
	+ The workflow produces a clean project structure:
```
/Users/william/Source/Python/ProjectName/python_basics/
├── basics/           # Virtual environment (ignored)
├── iterators.py      # Source file (tracked)
├── requirements.txt  # Dependencies (tracked)
├── .gitignore        # Ignore rules (tracked)
└── .git/            # Git repository
```
5. **Reproducibility**:
	+ Committing ==`requirements.txt`== early makes it easy for others to set up the same environment with ==`python3 -m venv basics`== and ==`pip i -r requirements.txt`==.


#### Document Setup
+ Add ==`README.md`== to explain how to setup project.
```
echo -e "# ProjectName\n\n## Setup\n1. Create virtual environment: \`python3 -m venv basics\`\n2. Activate: \`source basics/bin/activate\`\n3. Install dependencies: \`pip install -r requirements.txt\`" > README.md
git add README.md
git commit -m "Add README with setup instructions"
```

