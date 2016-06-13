---
layout: default
---

# Test one thing at a time

If you want to see if your function is doing what you think it's doing, you should be careful that you're not getting other functions up in the mix. Your test should say: I expect my function to give me **that specific output** when I give it **this specific input**.

Here's a function:

```javascript
var myFunkyAdd = function(numbersArray) {
  var addedNumbers = 0;
  numbersArray.forEach(function(arrayItem) {
    addedNumbers += arrayItem;
  })
  return addedNumbers;
}
```

Here's a mocha test for it:

```javascript
describe('myFunkyAdd', function() {
  it('should return the sum of the numbers in the array', function () {
    var expectedResult = 7;
    var inputNumbers = [3, 4];
    assert.equal(expectedResult, myFunkyAdd(inputNumbers));
  });
});
```

I expect my function to give me that specific output (`expectedResult`, which is `7`) when I give it this specific input (`inputNumbers`, which is `[3, 4]`). Notice how no other functions are used: just `myFunkyAdd`.

## Test it more

You can do more than one `assert` in a test to make it a bit stronger. This means testing that your function is re-usable: it works with lots of different inputs.

```javascript
describe('myFunkyAdd', function() {
  it('should return the sum of the numbers in the array', function () {
    assert.equal(7, myFunkyAdd([3, 4]));
    assert.equal(-9, myFunkyAdd([-1, -5, -3]]));
    assert.equal(91, myFunkyAdd([-67, 42, 15, 101]]));
  });
});
```

You should use enough tests to feel confident that your function will work for every use case. `myFunkyAdd` should work for any two numbers, but we can't test every single pair!

## It's complicated

Here's another function:

```javascript
var myFunkyPush = function(x, y) {
  var numbersArray = [];
  numbersArray.push(x, y);
  return numbersArray;
}
```

`myFunkyAdd` takes an array as an input. We could use `myFunkyPush` to generate that array. We might be tempted to write a test like this:

```javascript
describe('myFunkyAdd', function() {
  it('should return the sum of the numbers in the array', function () {
    var expectedResult = 7;
    var inputNumbers = myFunkyPush(3, 4);
    assert.equal(expectedResult, myFunkyAdd(inputNumbers));
  });
});
```

Now our `it` isn't quite right, though. We're testing that `myFunkyAdd` works correctly **when we use it with `myFunkyPush`**. In this test we can't be sure what happens when we use it without `myFunkyPush`. We shouldn't change our `myFunkyAdd` (but we should add a new test that only looks at `myFunkyPush).
