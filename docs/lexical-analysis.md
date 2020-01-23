## Intro

**Take the big string of code and trun it into tokens**

### tokenize

#### token

下面代码中所有非空格的部分都是 token

```
(add 1 2 (substract 6 3))
```

#### how it works

- accept an input string of code
- create a variable for tracking our position, like a cursor
- make an array of tokens
- write a while lopp that iterate through the source code input
- check each token to see if it matches one of your types
- add it to the list of tokens

```js
const tokenize = input => {
  let cursor = 0;
  const tokens = [];
  while (cursor < input.length) {
    // here comes the tokenizing
  }
  return tokens;
};
```
