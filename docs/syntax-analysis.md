## Intro

**turn the tokens into an intermediate representation or abstract syntax tree**

### how to to it

- iterate through the array of tokens
- for each number, string, etc. add the toke to same level of the tree
- for each callExpression (e.g. function) collect the parameters and then recurse down into the function body

(only identifiers and values matters)
