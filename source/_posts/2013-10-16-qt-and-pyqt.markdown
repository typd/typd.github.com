---
layout: post
title: "Qt and PyQt"
date: 2013-10-16 18:46
comments: true
categories: 
---

Sometimes it bothers me how to write UI program cross-platform, or just get rid of Visual Studio. Qt has been referenced a lot for that. Here are some notes based on my experience, understanding of Qt, pyQt.

# What's Qt

+ Quoted, [Qt](http://qt-project.org/) is a cross-platform application and UI framework for developers using C++ or QML, a CSS & JavaScript like language.

+ Owned by Nokia previously, then was sold to Digia.

+ Natively, you need to write C++.

+ Qt Creator is the supporting Qt IDE. Within it, Qt Designer is used for composing UI. Seems it looks pretty much like the WinForm drag down support from Visual Studio.

+ Highlights: cross-platform, native appearance based on platform, which means by using same code base, the release program may look like a windows program on windows, and a mac one on mac.

+ Latest version, Qt5.1

# Python solution

Of course you don't have to write C++. PyQt and pySide are the py solutions.

- PyQt
  - Uses same verion number as Qt, PyQt4 is for Qt4, PyQt5 is for PyQt5. 
  - Owned by riverbank, a uk company.
  - Licenses including GPL v3 and a commercial license. Which means for commercial usages, pay it [here](http://www.riverbankcomputing.co.uk/commercial/buy)
- pySide
  - License LGPL, no need to pay for commercial usage
  - Seems not under actively developing, release for Qt5 is still not ready yet, [pySide roadmap](http://qt-project.org/wiki/PySide_Roadmap)

I choose [PyQt5](http://www.riverbankcomputing.com/software/pyqt/download5).

# Setup them

Things to do

- Install Qt5, which contains Qt Creator
  - [download](http://qt-project.org/downloads)
- Install PyQt
  - note, I had problem with python3, python2 works fine
  - Install SIP, seems SIP is used for converting C++ code to python
    - [download](http://www.riverbankcomputing.com/software/sip/download)
    - note, the hg checked out version has a problem on sip.h, the tar ball works fine
    - python configurate.py && make && make install
    - add sip executor to your PATH
  - Install PyQt5
    - [download](http://www.riverbankcomputing.co.uk/software/pyqt/download5)
    - python configurate.py && make && make install

# Examples

PyQt examples are included in the tar ball, PyQt-gpl-5.1/examples. Start it from PyQt-gpl-5.1/examples/qtdemo/qtdemo.py

An example can be as simple as

    import sys

    from PyQt5.QtWidgets import QApplication
    from PyQt5.QtWidgets import QWidget

    class Window(QWidget):
        def __init__(self, parent=None):
            super(Window, self).__init__(parent)
            self.resize(360, 150)

    if __name__ == "__main__":
        app = QApplication(sys.argv)
        window = Window()
        window.show();
        app.exec_()

# Some more

Qt, PyQt, pySide seems all these are not well maintained. The offical sides are as convinient as I suppose they should be. Instructions, readmes, sample code contains some bug and mistakes more or less.
