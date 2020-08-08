## Numbers
### Points to remember. Basics

- They are float implicitly.
`
console.log(3 / 2); // will give 1.5
`
- Numbers are integers or to be specific 32 bit ints and are stored in the 32 bit format. So sometimes it will perform operations that are valid on 32 bit ints but not in real life integers/floats.
`0.1 + 0.2 == 0.30000000000000004; // Valid on 32 bit int, but in real life it should just give 0.3`
- `parseInt()` function is used to convert string to int. Similarly `parseFloat()` is used to convert string to float.
- If a non-number string is passed in `parseInt('Hello')` function this will return as special type `NaN`.
- `NaN` is short for Not a Number. We can check the result of any operation where we are not sure if the output will be a number or something else by using function `isNaN()`
- The `parseInt()` and `parseFloat()` functions parse a string until they reach a character that isn't valid for the specified number format, then return the number parsed up to that point. However the "+" operator simply converts the string to `NaN` if there is an invalid character contained within it. 