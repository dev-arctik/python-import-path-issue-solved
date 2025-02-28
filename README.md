
# Python Import Path Fix for Windows

## Issue
When running Python files in certain directories on Windows, imports from modules outside the current folder may fail with a `ModuleNotFoundError`. Specifically, if you're trying to run a Python file in a subfolder and it tries to import from a parent directory or other external modules, Python may not be able to locate the necessary files, leading to errors like:

```
ModuleNotFoundError: No module named 'app'

or

ImportError: attempted relative import with no known parent package
```



## Solution

You can modify the `sys.path` at the beginning of your script to manually include the parent directories, allowing Python to find the necessary modules even if they are outside the current working directory.

Add the following code at the top of your Python file before the import statements:

```python
import sys
import os

# Get the absolute path to the project root
project_root = os.path.abspath(os.path.join(os.path.dirname(__file__), '..', '..'))
sys.path.insert(0, project_root)

# Ensure the current directory is also in the path
current_dir = os.path.dirname(os.path.abspath(__file__))
sys.path.insert(0, current_dir)
sys.path.insert(0, os.path.dirname(current_dir))
```

or else you can run the following command

```
PYTHONPATH=<path_to_project_root> python <path_to_script.py>
```

### For example
Let's say your project structure looks like this:
```
/AIEngine
    /Test
      test.py
  /app.py
```

and you are running test.py which has some import from app.py then run the following command
```
PYTHONPATH="d:AIEngine" python Test/test.py
```
