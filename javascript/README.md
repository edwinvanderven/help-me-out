# JavaScript

### Foreach

**Note**: `forEach` expects a [synchronous function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach).

An asynchronous version of a `forEach` could look like this:

```javascript
export const asyncForEach = async (array, callback) => {
  for (let index = 0; index < array.length; index++) {
    await callback(array[index], index, array);
  }
};
```
