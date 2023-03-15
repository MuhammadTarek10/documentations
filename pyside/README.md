# Table of contents
- [Table of contents](#table-of-contents)
- [Why PySide6](#why-pyside6)
- [Responsive With PySide6](#responsive-with-pyside6)
- [Generating .py files](#generating-py-files)
  - [Making .py from .ui](#making-py-from-ui)
  - [Making .py from .qrc](#making-py-from-qrc)
- [Packaging programs](#packaging-programs)
  - [Making .exe](#making-exe)
  - [Making .exe with .ui and .qrc](#making-exe-with-ui-and-qrc)
- [Dealing with PySide6](#dealing-with-pyside6)
  - [Showing screen](#showing-screen)

# Why PySide6
If you don't know, `PyQt5` is not supported anymore, so we can use `PyQt6`, but theres a problem with getting .py file from .qrc. So I use `PySide6` because if supports all `PyQt` functionalities.
# Responsive With PySide6
To make ui responsive, you have to use `containers` that can be expanded, I personally use `QFrame` and `Layout` functionalities to get everything responsive.

# Generating .py files
## Making .py from .ui
```
pyside6-uic layout.ui -o layout.py
```

## Making .py from .qrc
```
pyside6-rcc resources.qrc -o resources_rc.py
```

# Packaging programs 
## Making .exe
```
pyinstaller --onefile --windowed --icon=icon.ico main.py
```

## Making .exe with .ui and .qrc
```
pyinstaller --onefile --windowed --icon=icon.ico --add-data "layout.ui;." --add-data "resources.qrc;." main.py
```
# Dealing with PySide6
## Showing screen
```
import sys
from PySide6.QtWidgets import QApplication, QMainWindow
from main_windows import Ui_MainWindow as View

class MainWindow(QMainWindow, View):
    def __init__(self):
        super(MainWindow, self).__init__(parent)
        self.setupUi(self)
        self.show()

if __name__ == "__main__":
    app = QApplication(sys.argv)
    window = MainWindow()
    sys.exit(app.exec())
```