# Métodos de Arrays

## Mutating

There are many array methods that mutate the array. Mutating an array means that the resulting array will take a different form from before

### push() // Insert an element at the end

```javascript
const array = [1, 2, 3, 4];
array.push(10); // 5 (push returns the length of the new array)
// array = [1, 2, 3, 4, 10]
```

### pop() // Remove an element from the end

```javascript
const array = [1, 2, 3, 4];
array.pop(); // 4 (pop returns the element removed)
// array = [1, 2, 3]
```

### unshift() // Inserts an element in the beginning

```javascript
const array = [1, 2, 3, 4];
array.unshift(9, 10); // 6 (unshift returns the length of new array)
// array = [9, 10, 1, 2, 3, 4]
```

### shift() // Remove first element

```javascript
const array = [1, 2, 3, 4];
array.shift(); // 1(shift returns the removed element)
// array = [2, 3, 4]
```

## Iterating

iterating through an array

### forEach() // Iterates an array

```javascript
const array = [1, 2, 3, 4]
array.forEach((elemnt, index) => {
console.log(`Element ${element} at index ${index}`)
}
```

### filter() // Iterates an array and result is filtered array

```javascript
const array = [1, 2, 3, 4];
const filteredArray = array.filter(element => element % 2);
// array = [1, 2, 3, 4]
// filteredArray = [1, 3]
```

### map() // Iterates an array and result is new array

```javascript
const array = [1, 2, 3, 4]
const mapArray = array.map(element => element \* 2)
// array = [1, 2, 3, 4]
// mapArray = [2, 4, 6, 8]
```

### reduce() // "Reduces" the array into single value (accumulator)

```javascript
const array = [1, 2, 3, 4];
const result = array.reduce(
  (accumulator, current) => accumulator + current,
  10,
);
// array = [1, 2, 3, 4]
// result = 20
```

## Others

### slice() // Returns desired elements in a new array

slice method will create a new array with elements from the index range passed in. In the example above, we specify the start index (0) and the end index (2) which gives us a new array [1, 2]. Also, notice that the original array isn’t mutated.
Note: End index is exclusive which means that the element at that end index isn’t included in the new array.

```javascript
const array = [1, 2, 3, 4];
const slicedArray = array.slice(0, 2);
// array = [1, 2, 3, 4]
// slicedArray = [1, 2]
```

### concat() // Append one or more arrays with given array

concat method will create a new array containing all the elements in the original array followed by the each of the arrays that are passed in. This method will not mutate the original array.
Note: You can pass in more than one array as arguments.

```javascript
const array = [1, 2, 3, 4];
const concatArray = array.concat([5, 6, 7, 8]);
// array = [1, 2, 3, 4]
// concatArray = [1, 2, 3, 4, 5, 6, 7, 8]
```

[Credit](https://medium.com/@timhancodes/javascript-array-methods-cheatsheet-633f761ac250)
