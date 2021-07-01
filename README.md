# QTermWidget

## Overview

A terminal emulator widget for Qt 5.

QTermWidget is an open-source project originally based on the KDE4 Konsole application, but it took its own direction later on.
The main goal of this project is to provide a Unicode-enabled, embeddable Qt widget for using as a built-in console (or terminal emulation widget).

It is compatible with BSD, Linux and OS X.

This project is licensed under the terms of the [GPLv2](https://www.gnu.org/licenses/gpl-2.0.en.html) or any later version. See the LICENSE file for the full text of the license. Some files are published under compatible licenses:
```
Files: example/main.cpp
       lib/TerminalCharacterDecoder.cpp
       lib/TerminalCharacterDecoder.h
       lib/kprocess.cpp
       lib/kprocess.h
       lib/kpty.cpp
       lib/kpty.h
       lib/kpty_p.h
       lib/kptydevice.cpp
       lib/kptydevice.h
       lib/kptyprocess.cpp
       lib/kptyprocess.h
       lib/qtermwidget.cpp
       lib/qtermwidget.h
Copyright: Author Adriaan de Groot <groot@kde.org>
           2010, KDE e.V <kde-ev-board@kde.org>
           2002-2007, Oswald Buddenhagen <ossi@kde.org>
           2006-2008, Robert Knight <robertknight@gmail.com>
           2002, Waldo Bastian <bastian@kde.org>
           2008, e_k <e_k@users.sourceforge.net>
License: LGPL-2+

Files: pyqt/cmake/*
Copyright: 2012, Luca Beltrame <lbeltrame@kde.org>
           2012, Rolf Eike Beer <eike@sf-mail.de>
           2007-2014, Simon Edwards <simon@simonzone.com>
License: BSD-3-clause

Files: cmake/FindUtf8Proc.cmake
Copyright: 2009-2011, Kitware, Inc
           2009-2011, Philip Lowman <philip@yhbt.com>
License: BSD-3-clause

Files: pyqt/cmake/PythonCompile.py
License: public-domain
```

## Installation

### Compiling sources

The only runtime dependency is qtbase ≥ 5.12.0.
Build dependencies are as follows:
- CMake ≥ 3.1.0 serves as the build system and therefore needs to be present to compile.
- The latest [lxqt-build-tools](https://github.com/lxqt/lxqt-build-tools/) is also needed for compilation.
- Git is needed to optionally pull latest VCS checkouts.

Code configuration is handled by CMake. CMake variable `CMAKE_INSTALL_PREFIX` will normally have to be set to `/usr`, depending on the way library paths are dealt with on 64bit systems. Variables like `CMAKE_INSTALL_LIBDIR` may have to be set as well.

To build, run `make`. To install, run `make install` which accepts variable `DESTDIR` as usual.

To build PyQt bindings, specify an additional CMake option `QTERMWIDGET_BUILD_PYTHON_BINDING=ON` when building this library.

### Binary packages

The library is provided by all major Linux distributions. This includes Arch Linux, Debian, Fedora, openSUSE and all of their children, given they use the same package repositories.
Just use the distributions' package managers to search for string `qtermwidget`.


### Translation

Translations can be done in [LXQt-Weblate](https://translate.lxqt-project.org/projects/lxqt-desktop/qtermwidget/)

<a href="https://translate.lxqt-project.org/projects/lxqt-desktop/qtermwidget/">
<img src="https://translate.lxqt-project.org/widgets/lxqt-desktop/-/qtermwidget/multi-auto.svg" alt="Translation status" />
</a>

## API
### Public Types
Type | Variable
| ---: | :---
enum | ScrollBarPosition { NoScrollBar, ScrollBarLeft, ScrollBarRight }
enum | KeyboardCursorShape { BlockCursor, UnderlineCursor, IBeamCursor }

### Properties
* flowControlEnabled : bool
* getPtySlaveFd : const int
* getShellPID : int
* getTerminalFont : QFont
* historyLinesCount : int
* icon : const QString
* keyBindings : QString
* screenColumnsCount : int
* selectedText(bool _preserveLineBreaks_ = true) : QString
* sizeHint : const QSize
* terminalSizeHint : bool
* title : const QString
* workingDirectory : QString

### Public Functions
Type | Function
| ---: | :---
| | QTermWidget(int _startnow_ = 1, QWidget *_parent_ = 0)
virtual | ~QTermWidget()
void | changeDir(const QString _&dir_)
void | getSelectionEnd(int &_row_, int &_column_)
void | getSelectionStart(int &_row_, int &_column_)
void | scrollToEnd()
void | sendText(QString &_text_)
void | setArgs(QStringList &_args_)
void | setAutoClose(bool _enabled_)
void | setColorScheme(const QString &_name_)
void | setEnvironment(const QStringList &_environment_)
void | setFlowControlEnabled(bool _enabled_)
void | setFlowControlWarningEnabled(bool _enabled_)
void | setHistorySize(int _lines_)
void | setKeyboardCursorShape(QTermWidget::KeyboardCursorShape _shape_)
void | setMonitorActivity(bool _enabled_)
void | setMonitorSilence(bool _enabled_)
void | setMotionAfterPasting(int _action_)
void | setScrollBarPosition(QTermWidget::ScrollBarPosition _pos_)
void | setSelectionEnd(int _row_, int _column_)
void | setSelectionStart(int _row_, int _column_)
void | setShellProgram(const QString &_program_)
void | setSilenceTimeout(int _seconds_)
void | setTerminalFont(QFont &_font_)
void | setTerminalOpacity(qreal _level_)
void | setTerminalSizeHint(bool _enabled_)
void | setTextCodec(QTextCodec *_codec_)
void | setWorkingDirectory(const QString &_dir_)
void | startShellProgram()
void | startTerminalTeletype()

### Public Slots
Type | Function
| ---: | :---
void | copyClipboard()
void | pasteClipboard()
void | pasteSelection()
void | zoomIn()
void | zoomOut()
void | setSize(_const QSize &_)
void | setKeyBindings(const QString &_kb_)
void | clear()
void | toggleShowSearchBar()

### Signals
Type | Function
| ---: | :---
void | activity()
void | bell(const QString &_message_)
void | copyAvailable(bool)
void | finished()
void | profileChanged(const QString &_profile_)
void | receivedData(const QString &_text_)
void | sendData(const char*, int)
void | silence()
void | termGetFocus()
void | termKeyPressed(QKeyEvent*)
void | termLostFocus()
void | titleChanged()
void | urlActivated(const QUrl &, bool _fromContextMenu_)

### Static Public Members
Type | Function
| ---: | :---
static QStringList | availableColorSchemes()
static QStringList | availableKeyBindings()
static void | addCustomColorSchemeDir(const QString &*custom_dir*)

### Protected Functions
Type | Function
| ---: | :---
virtual void | resizeEvent(_QResizeEvent_*)

### Protected Slots
Type | Function
| ---: | :---
void | sessionFinished()
void | selectionChanged(bool _textSelected_)

### Member Type Documentation
**enum QTermWidget::ScrollBarPosition**\
This enum describes the location where the scroll bar is positioned in the display widget when calling QTermWidget::setScrollBarPosition().

Constant | Value | Description
| --- | :---: | --- |
QTermWidget::NoScrollBar | 0x0 | Do not show the scroll bar.
QTermWidget::ScrollBarLeft | 0x1 | Show the scroll bar on the left side of the display.
QTermWidget::ScrollBarRight | 0x2 | Show the scroll bar on the right side of the display.

\
**enum QTermWidget::KeyboardCursorShape**\
This enum describes the available shapes for the keyboard cursor when calling QTermWidget::setKeyboardCursorShape().

Constant | Value | Description
| --- | :---: | --- |
QTermWidget::BlockCursor | 0x0 | A rectangular block which covers the entire area of the cursor character.
QTermWidget::UnderlineCursor | 0x1 | A single flat line which occupies the space at the bottom of the cursor character's area.
QTermWidget::IBeamCursor | 0x2 | A cursor shaped like the capital letter 'I', similar to the IBeam cursor used in Qt/KDE text editors.

### Property Documentation
**flowControlEnabled : bool**\
Returns whether flow control is enabled.

**getPtySlaveFd : const int**\
Returns a pty slave file descriptor. This can be used for display and control a remote terminal.

<!--**getShellPID : int**\-->
<!--**getTerminalFont : QFont**\-->

**historyLinesCount : int**\
Returns the number of lines in the history buffer.

<!--**icon : const QString**\-->

**keyBindings : QString**\
Returns current key bindings.

<!--**screenColumnsCount : int**\-->

**selectedText(bool _preserveLineBreaks_ = true) : QString**\
Returns the currently selected text.

<!--**sizeHint : const QSize**\-->
<!--**terminalSizeHint : bool**\-->
<!--**title : const QString**\-->
<!--**workingDirectory : QString**\-->

### Member Function Documentation
<!--__void activity()__\-->
<!--__void bell(const QString &_message_)__\-->

__void changeDir(const QString _&dir_)__\
Attempt to change shell directory (Linux only).

__void clear()__\
Clear the terminal content and move to home position.

<!--__void copyAvailable(bool)__\-->

__void copyClipboard()__\
Copy selection to clipboard.

<!--__void finished()__\-->
<!--__void getSelectionEnd(int &_row_, int &_column_)__\-->
<!--__void getSelectionStart(int &_row_, int &_column_)__\-->

__void pasteClipboard()__\
Paste clipboard to terminal.

__void pasteSelection()__\
Paste selection to terminal.

<!--__void profileChanged(const QString &_profile_)__\-->

__void receivedData(const QString &_text_)__\
Signals that we received new data from the process running in the terminal emulator.

__void scrollToEnd()__\
Wrapped, scroll to end of text.

__void sendData(const char*, int)__\
Emitted when emulator send data to the terminal process (redirected for external recipient). It can be used for control and display the remote terminal.

__void sendText(QString &_text_)__\
Send text to terminal.

__void setArgs(QStringList &_args_)__\
Sets the shell program arguments, default is none.

__void setAutoClose(bool _enabled_)__\
Automatically close the terminal session after the shell process exits or keep it running.

__void setColorScheme(const QString &_name_)__\
Sets the color scheme, default is white on black.

__void setEnvironment(const QStringList &_environment_)__\
Sets environment variables.

__void setFlowControlEnabled(bool _enabled_)__\
Sets whether flow control is enabled.

__void setFlowControlWarningEnabled(bool _enabled_)__\
Sets whether the flow control warning box should be shown when the flow control stop key (Ctrl+S) is pressed.

__void setHistorySize(int _lines_)__\
History size for scrolling.

__void setKeyBindings(const QString &_kb_)__\
Set named key binding for given widget.

__void setKeyboardCursorShape(QTermWidget::KeyboardCursorShape _shape_)__\
Sets the shape of the keyboard cursor.  This is the cursor drawn at the position in the terminal where keyboard input will appear.

<!--__void setMonitorActivity(bool _enabled_)__\-->
<!--__void setMonitorSilence(bool _enabled_)__\-->
<!--__void setMotionAfterPasting(int _action_)__\-->

__void setScrollBarPosition(QTermWidget::ScrollBarPosition _pos_)__\
Sets presence and position of scrollbar.

<!--__void setSelectionEnd(int _row_, int _column_)__\-->
<!--__void setSelectionStart(int _row_, int _column_)__\-->

__void setShellProgram(const QString &_program_)__\
Sets the shell program, default is /bin/bash.

<!--__void setSilenceTimeout(int _seconds_)__\-->
<!--__void setSize(_const QSize &_)__\-->

__void setTerminalFont(QFont &_font_)__\
Sets terminal font. Default is application font with family Monospace, size 10. Beware of a performance penalty and display/alignment issues when using a proportional font.

<!--__void setTerminalOpacity(qreal _level_)__\-->

__void setTerminalSizeHint(bool _enabled_)__\
Exposes TerminalDisplay::TerminalSizeHint.

__void setTextCodec(QTextCodec *_codec_)__\
Sets text codec, default is UTF-8.

<!--__void setWorkingDirectory(const QString &_dir_)__\-->
<!--__void silence()__\-->

__void startShellProgram()__\
Starts shell program if it was not started in constructor.

__void startTerminalTeletype()__\
Starts terminal teletype as is and redirect data for external recipient. It can be used for display and control a remote terminal.

<!--__void termGetFocus()__\-->
<!--__void termKeyPressed(QKeyEvent*)__\-->
<!--__void termLostFocus()__\-->
<!--__void titleChanged()__\-->
<!--__void toggleShowSearchBar()__\-->
<!--__void urlActivated(const QUrl &, bool _fromContextMenu_)__\-->

__void zoomIn()__\
Zooms in on the text.

__void zoomOut()__\
Zooms out in on the text.
