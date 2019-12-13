# C++

## Unused Variables

```cpp
__attribute__((__unused__)) auto variable = …
```

**Macro** from `/usr/include/libxml2/libxml/xmlversion.h` used by RRLIB XML serialization.

```cpp
#ifndef ATTRIBUTE_UNUSED
# if ((__GNUC__ > 2) || ((__GNUC__ == 2) && (__GNUC_MINOR__ >= 7)))
#  define ATTRIBUTE_UNUSED __attribute__((unused))
# else
#  define ATTRIBUTE_UNUSED
# endif
#endif
```

## Heredoc

```
auto msg = R"END(
)END";
```

## Error: expected type-specifier before 'ClassName'

Help the compiler by specifying the full namespace,
e.g. the global namespace (`::`) in the example below.

```cpp
class Scene: public QGraphicsScene
{
	enum Mode {ObstacleChain};
}

class ObstacleChain: QGraphicsItem {
}

new ::ObstacleChain;
```

More details at [StackOverflow](https://stackoverflow.com/a/9829860/870798).

## Shared Libraries

- Fehlende Libraries feststellen

  - `ldd` funktioniert nur bei Shared Libraries, z.B.

    ```shell script
    ldd export/linux_x86_64_debug/lib/librrlib_tof_camera_tof_camera_ifm_3d_mobile_camera.so
    ```

  - `nm` (zeigt auch die ge-mangle-ten Name)

- Linken (siehe [Manpage von g++](https://linux.die.net/man/1/g++))

  - `-llibrary` bzw. `-l library`:
    Sucht `library` während dem Linken

  - `-L dir`: Ergänzt die automatisch durchsuchten Verzeichnisse

  - `-I dir`: Fügt `dir` zu den Verzeichnissen mit Header-Files hinzu

## Internals

- [Copy Constructor in C++](https://www.geeksforgeeks.org/copy-constructor-in-cpp/)

- [Move Constructors and Move Assignment Operators (C++)](https://docs.microsoft.com/de-de/cpp/cpp/move-constructors-and-move-assignment-operators-cpp)

### Return Value Optimization

> In the context of the C++ programming language, return value optimization (RVO) is a compiler optimization that involves eliminating the temporary object created to hold a function's return value. RVO is particularly notable for being allowed to change the observable behaviour of the resulting program by the C++ standard.
>
> -- [Copy elision](https://en.wikipedia.org/wiki/Copy_elision#Return_value_optimization)
