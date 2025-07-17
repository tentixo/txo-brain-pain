# VS Code Problem

How to fix so you can run your Python scripts in VS Code in global settings.json for vscode
```text
"terminal.integrated.env.windows": {"PYTHONPATH": "${workspaceFolder}"},
```
In project `.vscode` folder in `launch.json`
```json
{
  "name": "Python: Current File",
  "type": "python",
  "request": "launch",
  "program": "${file}",
  "console": "integratedTerminal",
  "cwd": "${fileDirname}",
  "env": {
    "PYTHONPATH": "${workspaceFolder}${pathSeparator}${env:PYTHONPATH}"
  },
  "args": [
    "zt-atg"
  ]
}
```
In project `.vscode` folder in `settings.json`
```json
{
  "python.pythonPath": "${workspaceFolder}\\venv\\Scripts\\python.exe",
  "terminal.integrated.env.windows": {
    "PYTHONPATH": "${workspaceFolder}"
  }
}
```

## Form Source Site
I have a situation that I believe is relatively common. I want a script to import a module from another directory. My
python project is laid out as follows:
```text
~/project/
  |
  |---modules/
        |
        |---mod.py
  |---scripts/
        |---script.py
```
in `script.py`, I have `from modules import mod`. So my `PYTHONPATH` needs to be set to `~/project/` (something that 
PyCharm does automatically).  
VSCode is a great editor, but everywhere else, it falls short, in my opinion. This is a perfect example of that.  
I create a default `launch.json` file to "run the current file". A `"cwd": "${fileDirname}"` line has to be added to
make things work like they do in PyCharm (FYI, a list of the built-in variables can be found [here](https://code.visualstudio.com/docs/editor/variables-reference)).

# Debugging
For debugging (the "play" button on the sidebar, or the F5 key), the `PYTHONPATH` set in `launch.json` or your `.env`
file takes effect. Note that in the `.env` file, you cannot use variables such as `${workspaceRoot}`, but you can easily
append or insert to the path by using the proper separator for your platform (`;` for Windows and `:` for everyone
else).  
Because I want to take advantage of that variable, I put this in my `launch.json`:
```text
  "env": {
    "PYTHONPATH": "${workspaceFolder}${pathSeparator}${env:PYTHONPATH}"
  }
```
(Thanks to @someonr for the suggestion to use `${pathSeparator}`.)  

It appears that you can prepend/append to whatever is inherited from the environment (this is not true for
`settings.json`; see below).  
This will also work for the hotkey Ctrl+F5 (run without debugging).  
For reference, here's the full file, which replicates what PyCharm does automatically:
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: Current File",
      "type": "python",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal",
      "cwd": "${fileDirname}",
      "env": {
        "PYTHONPATH": "${workspaceFolder}${pathSeparator}${env:PYTHONPATH}"
      }
    }
  ]
}
```

# Run in Terminal
If I hit the "play" button that appears on the top right of the editor window (when a python file is the active tab), it
will not work. This runs the current file in a terminal, which doesn't pay attention to `launch.json` at all.  
To make that work, you have to define `PYTHONPATH` in a `settings.json` file, by adding this:
```text
    "terminal.integrated.env.windows": {
	    "PYTHONPATH": "${workspaceFolder}"
	}
```
(Note there are different values for each platform.) If you've selected a python interpreter (e.g. from a virtual
environment), you will already have a `settings.json` file in the `.vscode` directory. Mine looks like this:
```json
{
  "python.pythonPath": "/Users/me/project/venv/bin/python3",
  "terminal.integrated.env.osx": {
    "PYTHONPATH": "${workspaceFolder}"
  }
}
```
You can't append or insert values into the inherited `PYTHONPATH` via the `settings.json` file. It will only take one
string, and it will not parse separators. So even though you could get the value using `${env:PYTHONPATH}`, you won't be
able to do anything with it.  
Moreover, you can't set the current working directory. Even though it would seem you could set it with
`"terminal.integrated.cwd": "${workspaceFolder}"`, it doesn't work. So if any of your scripts do anything with paths
relative to their location in the tree, they won't work. The working directory will be your project root.  
Note that any changes to the `settings.json` file will require that you exit the integrated terminal and restart it.

# Linting
Nothing I do to `launch.json` regarding `PYTHONPATH` makes any difference to `pylint`, which will red-underline
`from modules import mod`, despite the fact I can put the cursor on `mod`, hit F12, and the file opens.  
Snooping around linting settings, the defaults for `mypy` include `--ignore-missing-imports`. To replicate this behavior 
with pylint, add this to your `settings.json`:
```text
    "python.linting.pylintArgs": [
        "--disable=F0401"
    ] 
```
Shame that we just have to work around this, but the autocomplete helps a lot when writing the import statements to
begin with.

# Conclusion
There are many layers to VSCode and it's hard to get things to work together. It seems multiple environments are
floating around. In the end:
1. I cannot "run in terminal" because I can't set the current working directory to be the path containing the current
   file.
2. I cannot set `PYTHONPATH` for `pylint` as that runs in some environment different than the integrated terminal and
   whatever is controlled by `launch.json`, so I can only tell `pylint` to ignore import errors.
3. Running with F5 works if you set `PYTHONPATH` either via an `.env` file or in `launch.json`
 