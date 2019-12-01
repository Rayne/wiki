# C++

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
