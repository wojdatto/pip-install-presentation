---
marp: true
---
<!-- theme: default
backgroundColor: #ffffff
_class: lead
 -->

# **pip install <your-package>**

## On packaging in Python

![bg right:43% width:450px](
https://user-images.githubusercontent.com/49607727/162530425-acc4968f-1560-497e-98d2-797c140499de.jpg
)

Tomasz Wojdat

April 2022

---

# Agenda

* A bit of history
* Library vs. application
* `pip` (`install`), or not to `pip`?
* Tips & caveats

---

![bg right:47% height:100% width:100%](
https://user-images.githubusercontent.com/49607727/162536865-ac3fcfe8-3aa5-4588-ba5b-6325ff13ea3a.jpg
)

# Python is old...

* ...and had a lot of relationships with different package managers.

---

![bg height:90%](
https://user-images.githubusercontent.com/49607727/162634162-cc52b5d3-2469-4f47-b839-29aa375f8818.png
)

<!-- Superfund sites are polluted locations in the United States
requiring a long-term response to clean up hazardous material
contaminations -->

---

# The year is 2001, and I want to find Python code. Where should I look?

* # **The Vaults of Parnassus**

---

![bg height:90%](
https://user-images.githubusercontent.com/49607727/162634473-3343cdf0-27ff-4e8b-9a4f-381cfbd2ffba.png
)

<!-- Mount Parnassus is a mountain in Greece, sacred in mythology and a
metaphor for the arts and learning. -->

---

# How do I build downloaded code?

* Using `distutils`
* Which is included in the standard library since year 2000 (Python 1.6)
* The code is shipped in the form of the source distribution
* Also known as `sdist`
* `python setup.py sdist`

---

# But building takes too long!

* Especially when you have to compile C extensions by yourself
* Solution: use build distributions
* Also known as `bdist`
* `python setup.py bdist`

---

# How can I "do" packaging?

* But every system comes with a package manager, doesn't it?

---

![bg height:50%](
https://user-images.githubusercontent.com/49607727/162635524-e674ad47-afc4-4a2f-93a0-1f7ed295d024.png
)

<!-- BTW: Apple also doesn't provide a default package manager. -->

---

# Another problem: I want the newest version now!

---

# The birth of the Python Package Index

* Also known as PyPI
* (and not PyPy)
* And also known as "The Cheeseshop"

<!-- Why Cheeseshop? when PyPI was first created there was nothing in
it. Exactly like in the sketch from Monty Python  -->

---

![bg height:90%](
https://user-images.githubusercontent.com/49607727/162635894-7ec6ba47-07a0-4661-8c1c-5230c0fecef8.png
)

---

# PyPI wasn't hosting packages

* It was only indexing them
* And there were downloaded from various 3rd party domains

<!-- We will come back to this later. -->

---

# How can I specify dependencies?

* Using `setuptools`
* Which is a monkey patch of `disutils`

<!-- A monkey patch is a way to extend or modify the runtime code of
dynamic languages without altering the original source code. -->

---

## But installing package with all dependencies is too hard!

* Solution: `easy_install`
* Which came with a new `egg` distribution
* Which is a zip file that contains code/byte code, and metadata

<!-- Why such name? Snake lays eggs. -->

<!-- Dymola ships its Python interface as the `.egg` file -->

---

# There is a problem
---

![bg height:50%](
https://user-images.githubusercontent.com/49607727/162637578-62c78cf6-00d7-4c32-b3eb-fc677888a7fe.png
)

---

# The egg is broken

* And `easy_install` have a lot of problems
* It cannot uninstall packages
* Or even list already installed packages

<!-- Egg format had problems with specification,
and people didn't like it. -->

<!-- `easy_install` also mocked around with sys.path which is
generally not a good idea. -->

---

# Let's clean it

* Solution: `pyinstall`
* Created in 2008 by Ian Bicking
* But `pyinstall install <some-package>` is too long
* The name was changed to `pip`

---

# `pip`

![bg right:40% height:500px](
https://user-images.githubusercontent.com/49607727/162529517-4acad509-9447-4413-8981-5b5e1f41c686.jpg
)

* "The" Python package manager since 2011
* Since then, maintained by Python Packaging Authority (PyPA)
* At the beginning relies only on `sdist`

<!-- Only `sdist` because eggs had bad reputation. -->

---

### But what's the deal with the new name!?

![bg left:40% height:400px](
https://user-images.githubusercontent.com/49607727/162535300-c755508c-cade-4fa2-bf24-e44b14f1957e.jpg
)

<br>

* # **p**ip **i**nstalls **p**ackages

---

# Application dependencies

* `requirements.txt`
* `pip install -r requirements.txt`
* `pip` is used only to install application dependencies
* There is no top level project to install

---

# PyPI needs to adapt

* Installing from it is often slow...
* ...and we need to trust 3rd party domains
* PyPI becomes a hosting platform

---

![bg height:90%](
https://user-images.githubusercontent.com/49607727/162636934-a5a3dad5-e00a-43b1-b07e-84c5328b9b3a.png
)

---

# What to do with the spilled egg?

* Installing from source takes too much time
* Solution: "The Wheel Distribution"
* Also known as `bdist_wheel`

---

![bg height:90%](
https://user-images.githubusercontent.com/49607727/162637771-d313d022-1c8c-49cf-a171-b5d2616ed005.png
)

<!-- PEP stands for Python Enhancement Program -->

---

# But why this name?

---

![bg height:90%](
https://user-images.githubusercontent.com/49607727/162637334-1cf8da75-8a80-4b82-9513-12f2f67b9042.png
)

---

# There are more problems

* `python setup.py upload` doesn't use HTTPS
* Anyone can sniff our password
* The birth of `twine`
* Which securely allows uploading our package to PyPI
* The name?
* > Strong thread or string consisting of two or more strands of hemp,
  > cotton, or nylon twisted together.

---

![bg height:90%](
https://user-images.githubusercontent.com/49607727/162638121-211960ae-f6f6-4964-b6ff-d5de5225f464.png
)

<!-- This name is not ideal because `twine` doesn't do anything to our
package. It only sends it. -->

---

# This is not everything

* Because there is also the entire `conda` ecosystem
* But let's focus on the `pip` side

<!-- `conda` is very convenient for installing complicated sciency things,
but breaks a lot of expectations for how Python usually works, especially
on Windows. And it's very very heavy. -->

---

# Application vs. library

---

# Application

* Something that is specifically deployed somewhere
* Usually has a lot of dependencies, and can be very complex
* We want to ensure **repeatable** builds
* The version of code you tested with is the same version that goes to
  production
* There are no unattended upgrades of third-party packages that can
  break your app
* Each commit should represent a precise deployment (code and its
  dependencies)
* So you can always easily see what changed between two deployments
* And count on being able to revert changes

---

# Library

* Maximization of compatibility is desired
* We want to know about incompatibilities with other libraries as soon
  as possible
* The best practice is to only loosely pin requirements
* And only when absolutely necessary
* This approach applies also to tools like `pre-commit`, `FMPy`, or
  `pyzet`

---

# Project layout for applications

---

```plaintext
├── venv/
├── requirements.txt
├── requirements-minimal.txt
├── requirements-dev.txt
├── requirements-dev-minimal.txt
├── module_name/
│   ├── submodule_name/ (too much nesting might not be a good idea)
│   │   ├── __init__.py
│   │   ├── __main__.py
│   │   └── <...>
│   ├── __init__.py
│   ├── __main__.py
│   ├── main.py
│   └── <...>
├── tests/
│   ├── __init__.py
│   └── <*_test.py files>
│── testing/
│   └── <misc files used for testing>
└── <other config files, readme etc.>
```

* `python -m <module_name>`

<!-- Naming tests `*_test.py` makes it easier to use autocompletion. -->
<!-- The `-m` command should be run in `venv`, of course. -->

---

# `requirements` files

* `requirements.txt`
  * all packages with constrained versions

* `requirements-minimal.txt`
  * import-only packages with no (or minimal) version constraints

* `requirements-dev.txt`
  * all development packages with constrained versions
  * but they shouldn't duplicate anything from `requirements.txt`

* `requirements-dev-minimal.txt`
  * import-only development packages with no (or minimal) version
    constraints

---

# Project layout for libraries

---

```plaintext
├── venv/
├── setup.py
├── setup.cfg
├── pyproject.toml
├── requirements-dev.txt
├── src/
│   └── module_name/
│       ├── submodule_name/ (too much nesting might not be a good idea)
│       │   ├── __init__.py
│       │   ├── __main__.py
│       │   └── <...>
│       ├── __init__.py
│       ├── __main__.py
│       ├── main.py
│       └── <...>
├── tests/
│   ├── __init__.py
│   └── <*_test.py files>
│── testing/
│   └── <misc files used for testing>
├── tox.ini
```

* `pip install -e .`

---

# Setup files

* `setup.py`
  * defines package using Python code
  * because of that it might be not the most secure solution
* `setup.cfg`
  * declarative way of defining the same information
  * the most popular solution among open-source packages
  * there are tools that can generate it from `setup.py`
  * e.g. <https://github.com/asottile/setup-py-upgrade>
* `pyproject.toml`
  * the newest format defined in PEP 518
  * not yet widely used
  * however, some tools make use of it, e.g. `poetry`

---

## Classic layout

```plaintext
└── module_name/
    ├── __init__.py
    ├── __main__.py
    ├── main.py
    └── <...>
```

## `src` layout

```plaintext
└── src/
    └── module_name/
        ├── __init__.py
        ├── __main__.py
        ├── main.py
        └── <...>
```

---

# Reasons to use `src` layout

* In standard layout, package installation might be broken, but all
  tests can still pass

* Because Python automatically adds module folder to `PYTHONPATH`

* So, there is a risk of deploying a broken package

* `src` layout approach was created to avoid this issue

* It increases nesting by one, so the module won't be automatically
  added to `PYTHONPATH`

* So, package has to be installed correctly for tests to pass

---

# When to choose which approach?

* Libraries usually require more attention
* They have to be actively maintained
* Library code might be fine, but the package might be broken
* Packaging some less standard libraries is usually tricky
* Sharing code is great, but we shouldn't overestimate it

<!-- By less standard I mean libraries that contain not only Python code,
but some other crucial files, or C extensions etc. -->

---

# References

* <https://packaging.python.org/en/latest/> &ndash; Python packaging
  user guide

* <https://nickmccullum.com/history-python-package-managers/> &ndash;
  The history of Python package managers

* <https://youtu.be/AQsZsgJ30AE> &ndash; Dustin Ingram &ndash; Inside
the Cheeseshop: How Python Packaging Works &ndash; PyCon 2018

* <https://github.com/Yelp/requirements-tools> &ndash; Scripts for
  working with Python requirements, primarily in applications

* <https://youtu.be/GaWs-LenLYE> &ndash; Python packaging: basic
  setup.py and declarative metadata

* <https://youtu.be/sW1qUZ_nSXk> &ndash; Python packaging: src layout

* <https://youtu.be/bfyIrX4_yL8> &ndash; Python packaging: data files
