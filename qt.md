# Qt

## Slots & Signals

Bei überladenen Signalen ist ein `cast` notwendig. Folgender Code funktioniert z.B. nicht:

```cpp
connect(this->lspServer, &QProcess::finished, [=](int) {});
```

Die Lösung nutzt einen `static_cast`:

```cpp
exitCode){
connect(this->lspServer, static_cast<void(QProcess::*)(int, QProcess::ExitStatus)>(&QProcess::finished), [=](int exitCode){
  // …
});
```

## Eclipse + Finroc + Qt5

- Discover missing includes with the help of `pkg-config`:

  ```
  pkg-config --list-all | grep Qt
  pkg-config --cflags Qt5Core 
  ```

  ```
  -I/usr/include/x86_64-linux-gnu/qt5/QtCore -I/usr/include/x86_64-linux-gnu/qt5
  ```

  It is not necessary to add entries to `libdb.raw` und `libdb.raw.local`.

- Add Qt5 to **Eclipse**

  1. Project → Properties → C/C++ General → Path and Symbols → Includes → GNU C++

  1. Add the missing directories (see *discovery* above) `/usr/include/x86_64-linux-gnu/qt5` and `/usr/include/x86_64-linux-gnu/qt5/QtCore`

- Add the missing dependency `Qt5Core` to the **Finroc** project

  ```xml
  <?xml version="1.0" encoding="UTF-8" standalone="no"?>
  <targets>
    <library cxxflags="-fPIC" libs="Qt5Core">
      <sources exclude="pTest3000.cpp">
        *.cpp
      </sources>
    </library>
  
    <program name="finroc_test3000">
      <sources>
        pTest3000.cpp
      </sources>
    </program>
  </targets>
  ```

## QtCreator

1. Run qmake

2. Build all

### Ubuntu 18.04

```bash
apt install qtcreator qtcreator-doc qt5-default qt5-doc
```

### Documentation

```bash
apt install qtcreator-doc qt5-doc
```

### Problem: qmake doesn't create all h/cpp-files for ui-files

Disable "Qt shadow builds" in the project settings.

1. Projects in der Sidebar anklicken

2. General → Shadow Builds deaktivieren

## Gezielt Warnings in Qt unterdrücken

Warnings können bei `G++` gezielt abgeschaltet werden.
Qt erzeugt beispielsweise folgende Warnungen:

```
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h:944:1: note: ...this statement, but the latter is misleadingly indented as if it were guarded by the ‘if’
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h:944:1: error: this ‘while’ clause does not guard... [-Werror=misleading-indentation]
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h:944:1: note: ...this statement, but the latter is misleadingly indented as if it were guarded by the ‘while’
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h: In member function ‘bool QVectorIterator<T>::findPrevious(const T&)’:
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h:944:1: error: this ‘if’ clause does not guard... [-Werror=misleading-indentation]
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h:944:1: note: ...this statement, but the latter is misleadingly indented as if it were guarded by the ‘if’
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h:944:1: error: this ‘while’ clause does not guard... [-Werror=misleading-indentation]
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h:944:1: note: ...this statement, but the latter is misleadingly indented as if it were guarded by the ‘while’
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h: In member function ‘bool QMutableVectorIterator<T>::findNext(const T&)’:
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h:945:1: error: this ‘if’ clause does not guard... [-Werror=misleading-indentation]
 Q_DECLARE_MUTABLE_SEQUENTIAL_ITERATOR(Vector)
 ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h:945:1: note: ...this statement, but the latter is misleadingly indented as if it were guarded by the ‘if’
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h:945:1: error: this ‘while’ clause does not guard... [-Werror=misleading-indentation]
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h:945:1: note: ...this statement, but the latter is misleadingly indented as if it were guarded by the ‘while’
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h: In member function ‘bool QMutableVectorIterator<T>::findPrevious(const T&)’:
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h:945:1: error: this ‘if’ clause does not guard... [-Werror=misleading-indentation]
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h:945:1: note: ...this statement, but the latter is misleadingly indented as if it were guarded by the ‘if’
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h:945:1: error: this ‘while’ clause does not guard... [-Werror=misleading-indentation]
/usr/include/x86_64-linux-gnu/qt5/QtCore/qvector.h:945:1: note: ...this statement, but the latter is misleadingly indented as if it were guarded by the ‘while’
cc1plus: all warnings being treated as errors
Makefile.generated:258839: recipe for target 'build/linux_x86_64_debug/projects/ib2c_designer/import/mNetworkVisitor.o' failed
make[1]: *** [build/linux_x86_64_debug/projects/ib2c_designer/import/mNetworkVisitor.o] Error 1
Makefile:37: recipe for target 'build' failed
make: *** [build] Error 2

```

Da wir die Systembibliothek Qt nicht verändern wollen,
deaktivieren wir für Qt die entsprechenden Flags.

```
#if (defined __GNUC__) && (__GNUC__ > 5)
    #pragma GCC diagnostic push
    #pragma GCC diagnostic ignored "-Wmisleading-indentation"
    #include <QtCore/QString>
    #pragma GCC diagnostic pop
#else
    #include <QtCore/QString>
#endif
```
