# Spec

Using Vue, display all numbers from 1 to 100 in a random order on the screen. This number should be configurable via a provided input box.
If the user places their pointer over a given number, highlight that numbers' divisors.
For example, if the user hovers over 21, the numbers 1, 3, 7 would be highlighted. 22 would highlight 1, 2 and 11.

# Interview Task

The provided code is functional, but it's got some issues that need to be resolved. These issues may or may not be logical in nature - just because the code is working doesn't necessarily mean it is the best way of doing something.

Improve the code how you see fit - please leave comments to justify your decisions.

# GitHub Pull Requests

This is an interview task sent to prospective candidates to work at Aluminati. As such, all pull requests will be rejected. This code is, by its very nature, purposely designed with issues that candiates are asked to review!

If you have been invited to perform this test your submission should be through your point of contact with us, e.g. your recruitment agency.

---

# > Changes & Fixes

--> _Additional comments within the source code as comments_ <--

---

#### 1. Created a new function for shuffling the array based on **Fisher-Yates algorithm**.

This algorithm provides a better, more randomized and faster shuffle than sort()

```js
shuffleArray(array) {
    let receivedArray = array;
    for (let i = receivedArray.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * (i + 1));
        [receivedArray[i], receivedArray[j]] = [receivedArray[j], receivedArray[i]];
    }
    return receivedArray;
},
```

#### 2. Change the first `for loop` from `i = 0` to `i = 1` and changed the condition from `<` to `<=`.

The requirements of the application is to show all values from 1 to 100 (where 100 is the value on the input and can be changed). Without these changes the application displayed numbers from 0 to 99 while the input was 100.

#### 3. Changed the method for appending items to the array of `numbers`.

Based on preference, since `numbers = [...numbers, i]` is exactly the same as `numbers.push()`, I decided to change it as it takes less code.

#### 4. Renamed two function names to a more convenient name

• Renamed the method `n()` to `numbersList()`

• Renamed the method `hov()` to `numbersHover()`

#### 5. Created a variable that can be used by multiple methods called `allNumbers`

This variable was previously named `nums` and was created two times in two different methods.

`allNumbers` is now returned in the `data()` method and it is used as `this.allNumbers`. Only set in the first method (called) and then used on the second one without re-setting the same value.

#### 6. Converted the text of all the elements with `class=“number”` created from the array `numbers` to a valid Number.

Using either `textContents` or `innerHTML` for an element will simply return a string, if the string happens to be a number, it will work on a calculation without issue, however, this is not considered a good practice and can cause massive issues.

Therefore, by using `parseInt()` this has been fixed and now it is recognized as a proper Number.

> **EXTRA**: The same can be done with the "+" symbol (e.g. `+myValue.trim()`) or the `Number()` method, as well as other methods too.
