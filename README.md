pyvfx-boilerplate
==================

A boilerplate for creating PyQt4/PySide and PyQt5/PySide2 applications running in Maya, Nuke or completely standalone.

## Documentation

### Version 2.0

#### Changes from 1.0

- Complete rewrite of the boilerplate.
- Requires the [`Qt.py`](https://github.com/mottosso/Qt.py) module (v0.2.5) to detect Qt bindings.
- Uses `PySide.QUiTools` instead of `pysideuic`.
- No longer uses the complex "wrap instance" approach in favor for simpler code. Because of this, UIs are no longer loaded into `self`.
- Maya palette removed (will be back soon).
- Git repo name change: all lowercase.
- Pretty much PEP8 compliant.
- Now comes with Qt.WindowStaysOnTopHint out of the box.
- Can be run in multiple ways (see examples).

#### Examples

```python
# Download, install and run standalone
git clone https://github.com/pyvfx-boilerplate.git
cd pyvfx-boilerplate
pip install -U Qt.py
python
>>> import boilerplate
>>> boilerplate.run_standalone()
```

```python
# Just run as standalone
pip install Qt.py
python boilerplate.py
```

```python
# Run in Maya or Nuke
import sys
sys.path.append('/path/to/pyvfx-boilerplate')
import boilerplate

boilerplate.run_maya()  # or boilerplate.run_nuke()
```


You can also copy-paste the boilerplate.py contents into your DCC application.

#### Usage

Since the boilerplate relies on [`Qt.py`](https://github.com/mottosso/Qt.py), you should design your application as if you were designing it for PyQt5/PySide2. This means creating widgets using `QtWidgets` rather than `QtGui`. The `Qt.py` module takes care of the remapping and makes for compatibility with PyQt4/PySide. Read more over at the [`Qt.py` repository](https://github.com/mottosso/Qt.py).

Tip: when you cannot rely on `Qt.py`, create an issue and/or detect which binding is being used:

```python
from Qt import __binding__

if __binding__.startswith('PyQt'):
    ...
elif __binding.startswith('PySide'):
    ...
```

#### Modifying the boilerplate

Set up the filepath to the UI files (optional):

```python
ui_dir = _ui_dir('/path/to/ui_files')
```

If the `Qt` module isn't picked up, define where it can be found:

```python
_sitepackages_setup([
    'C:/Python27/Lib/site-packages',  # Windows
    '/usr/lib/python2.7/site-packages',  # Linux
    '/Library/Python/2.7/site-packages',  # OS X

    '/usr/local/Cellar/python/2.7.11/Frameworks/Python.framework/Versions/' +
    'Current/lib/python2.7/site-packages'  # Homebrew location, Python 2.7.11
])
```

Set the window title and the object name:

```python
WINDOW_TITLE = 'Boilerplate'
WINDOW_OBJECT = 'boilerPlate'
```

Rename every occurance of `boil` in the code to reflect a unique name for your application.

Make sure the 

Change the class `Boilerplate` to your heart's content!

Options:
- If you wish to force a binding, define `QT_PREFERRED_BINDING`.
- Dock UI with Maya UI by setting `DOCK_WITH_MAYA_UI`.
- Dock UI with Nuke UI by setting `DOCK_WITH_NUKE_UI`.



### Version 1.0

Edit boilerplate.py and edit the "QT_BINDINGS" variable to say either "Auto", "PySide" or "PyQt". 
Then just execute boilerplate.py either inside of Nuke, Maya or as standalone. Please note that Maya 2013 and above as well as Nuke 6.3 and above has native support for PySide.

The script is setup in such a way that .ui files are loaded the same way whether you use PySide or PyQt, which is the main reason for why I created this boilerplate.

I've dumped the Maya 2015 QPalette, which can be used if you run your app in Standalone mode, outside of your DCC app. The first step of making a "Pro" app ;)

More information on usage and customization over at the project's wiki: https://github.com/fredrikaverpil/pyvfx-boilerplate/wiki
