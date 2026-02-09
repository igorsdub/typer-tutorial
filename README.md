# Typer Tutorial

[Tutorial link](https://typer.tiangolo.com/tutorial/).

## Evironment Variables

An environment variable (also known as "env var") is a variable that lives outside of the Python code, in the operating system, and could be read by your Python code (or by other programs as well).

### Create and Use Env Vars

```bash
export MY_NAME="Wade Wilson"
echo "Hello $MY_NAME"
```

This command will print `Wade Wilson` in the terminal window. We can also create environment varaibles inside of Python.

### Read Env Vars in Python

```python
import os

name = os.getenv("MY_NAME", "World")
print(f"Hello {name} from Python")
```

```bash
python main.py
```

This will output:

```text
Hello World from Python
```

Now, we will combine two worlds: define an environmetal variable in a shell and read it in Python. The exisitng code needs no modification since it alrady access shell's environmental varaibales.

```bash
python main.py
export MY_NAME="Wade Wilson"
python main.py
```

```text
Hello Wade Wilson from Python
```

Nice! As environment variables can be set outside of the code, but can be read by the code, and don't have to be stored (committed to `git`) with the rest of the files, it's common to use them for configurations or settings. For example, `.env` file can store such configurations and be read by `python-dot` package whihc is the default way to pass env vars in the Cookie Cutter Data Science template.

In case if you only want to have a specific varibale available for the one time only use, you can create an environmental variable before the program itslef, on the same line:

```bash
MY_NAME="Nancy Sinatra" python main.py
```

```text
Hello Nancy Sinatra from Python
```

If re-run, the variable is reset to the defualt:

```bash
python main.py
```

```text
Hello World from Python
```

>[!CAUTION]
> Didn't work for me. I still had `Wade Wilson` as my env var. However, if I restart the shell, run the one-time env var example, then it will use `World` when run with no env var input.

### Types and Validation

The environmental varaibles the we have covered can only handle text strings, due to compatability reasons. That means that any value read in Python from an environmental variable will be `str`, and any other conversion to a differnt type must be done in code.

### `PATH` Environment Variable

The most famous and heavily used environmental varibale is `PATH`. It stores paths to programs on your machine.

The value of the variable `PATH` is a long string that is made of directories separated by a colon `:` on Linux and macOS, and by a semicolon `;` on Windows. For example:

```bash
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```

This means that the system should look for programs in the directories:

- `/usr/local/bin`
- `/usr/bin`
- `/bin`
- `/usr/sbin`
- `/sbin`

>[!TIP]
> That's why you shouldn't include `:` or any other special characther in directory or filenmanes, not to confuse the system when resolving or maniputaing paths.

When you type a command in the terminal, the operating system looks for the program in each of those directories listed in the `PATH` environment variable.

For example, when you type `python` in the terminal, the operating system looks for a program called `python` in the first directory in that list.

If it finds it, then it will use it. Otherwise it keeps looking in the other directories.
