+++
title = 'Installing a local Python project'
date = 2022-03-22T10:34:36-08:00
lastmod = 2022-11-29T06:55:00-08:00
+++

You can make your own projects installable into your other projects as if you had downloaded them from PyPI following these steps.

**1.** In the project's root folder, create a file named setup.py with these contents:

```python
import setuptools
setuptools.setup()

```

**2.** In the same folder, create a file named setup.cfg with these contents:

```cfg
[metadata]
name = Your App Name Here

[options]
packages = your_package_name_here
python_requires = >=3.7
package_dir =
    =.

```

You may want to change the app name, package name, and minimum Python version. There's also a lot more that can be added to this file to help with certain situations (see links below).

**3.** In each package folder in your project, create an empty file named \_\_init__.py.

**4.** Use this terminal command while in the project's directory: `pip install -e .`

Now you can import your projects using statements like these:

```python
from app_name.module_name import class_or_function_or_variable
from app_name import other_module_name
```

You might want to add import statements to your \_\_init__.py files to simplify the import statements used for this project elsewhere.

## further reading

* [anthonywritescode's YouTube guide to Python packaging](https://youtu.be/GaWs-LenLYE?t=487)
* [Real Python's guide to Python imports](https://realpython.com/python-import/#create-and-install-a-local-package)
* [The Hitchhiker's Guide to Python on Structuring Your Project](https://docs.python-guide.org/writing/structure/)
