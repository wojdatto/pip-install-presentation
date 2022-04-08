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

* Python & pip
* Library vs. application
* Pip, or not to pip?
* Tips & caveats:
  * sdist vs. wheel
  * src layout
* Live demo

---

![bg right:47% height:100% width:100%](
https://user-images.githubusercontent.com/49607727/162536865-ac3fcfe8-3aa5-4588-ba5b-6325ff13ea3a.jpg
)

* Python is old...
* ...and had a lot of package managers:
  * `disutils`
  * `setuptools`
  * `easy_install`
  * `pip`
* But there are more, e.g. `conda`

---

# Pip?

![bg right:45% height:500px](
https://user-images.githubusercontent.com/49607727/162529517-4acad509-9447-4413-8981-5b5e1f41c686.jpg
)

* Python package manager since 2011.
* By default downloads packages from PyPI (Python Package Index AKA
  Cheeseshop).
* Introduced in 2008 as pyinstall by Ian Bicking.
* Since 2011 maintained by PythWon Packaging Authority (PyPA).

---

### But what's the deal with the name!?

![bg left:47% height:400px](
https://user-images.githubusercontent.com/49607727/162535300-c755508c-cade-4fa2-bf24-e44b14f1957e.jpg
)

<br>

> Pip Installs Packages

---

# src layout

```python
print("hello")
```

---

# References

* <https://nickmccullum.com/history-python-package-managers/> &ndash;
  The history of Python package managers

* <https://youtu.be/AQsZsgJ30AE> &ndash; Dustin Ingram &ndash; Inside
the Cheeseshop: How Python Packaging Works &ndash; PyCon 2018

* <https://packaging.python.org/en/latest/> &ndash; Python packaging
  user guide

* <https://github.com/Yelp/requirements-tools> &ndash; Scripts for
  working with Python requirements, primarily in applications

* <https://youtu.be/GaWs-LenLYE> &ndash; Python packaging: basic
  setup.py and declarative metadata

* <https://youtu.be/sW1qUZ_nSXk> &ndash; Python packaging: src layout

* <https://youtu.be/bfyIrX4_yL8> &ndash; Python packaging: data files
