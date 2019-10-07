# 251 Flatten 2D Vector

```java
/*
Implement an iterator to flatten a 2d vector.

For example,
Given 2d vector =

[
  [1,2],
  [3],
  [4,5,6]
]
By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,2,3,4,5,6].

Follow up:
As an added challenge, try to code it using only iterators in C++ or iterators in Java.
*/

public class Vector2D implements Iterator<Integer> {

    private Iterator<List<Integer>> listIter;
    private Iterator<Integer> iter;

    public Vector2D(List<List<Integer>> vec2d) {
        listIter = vec2d.iterator();
    }

    @Override
    public Integer next() {
        modify();
        return iter.next();
    }

    @Override
    public boolean hasNext() {
        modify();
        return iter != null && iter.hasNext();
    }

    private void modify() {
        while (iter == null || !iter.hasNext()) {
            if (listIter.hasNext()) {
                iter = listIter.next().iterator();
            } else {
                return;
            }
        }
    }

}

/**
 * Your Vector2D object will be instantiated and called as such:
 * Vector2D i = new Vector2D(vec2d);
 * while (i.hasNext()) v[f()] = i.next();
 */
```
