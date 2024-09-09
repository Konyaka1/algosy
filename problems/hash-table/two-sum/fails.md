## Fails
#### Syntax improvements
In java we can return array in following way
```java
public int[] getArray() {
    Integer first = 234;
    int second = 25;
    char third = 'a';
    return new int[]{first, second, third, 0};
}
```