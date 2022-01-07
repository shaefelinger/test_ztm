# Max JS

##### vs code

- material icons
- prettier
- 

settings user/workspace



##### dev tools

uncheck preserve log

------

![image-20211227204915593](../../../../../Library/Application Support/typora-user-images/image-20211227204915593.png)



> convention: never assign `undefined`

typeof



------

## defer

much better to load the scripts as early as possible -› faster



```html
<head>
  ...
	<script src="assets/scripts/app.js" defer></script>
  ...
```



using `async`  executes as soon as possible



![image-20211227210630283](../../../../../Library/Application Support/typora-user-images/image-20211227210630283.png)

------

- MDN => JavaScript Basics: https://developer.mozilla.org/en-US/docs/Web/JavaScript
- MDN => Variables: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Variables
- MDN => Operators: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Math
- MDN => Functions: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Functions
- MDN => Arrays: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Arrays
- MDN => Objects: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Basics

------

# Dev-Workflow & Debugging

Write Code Efficently

Find Help

Debug

# IDE



ECMA Standard

https://www.ecma-international.org/publications-and-standards/standards/ecma-262/

### Debugging

set breakpoint in dev-tools -> stops BEFORE the selected line



vscode: chrome debug

- VS Code Docs: https://code.visualstudio.com/docs
- VS Code Keybindings: https://code.visualstudio.com/docs/getstarted/keybindings
- VS Code Extensions Docs: https://code.visualstudio.com/docs/editor/extension-gallery
- Google Chrome DevTools Docs: https://developers.google.com/web/tools/chrome-devtools/

------

## Conventions

- GLOBAL_CONSTANTS in uppercase
- functions that are attaced to an evenlistener:
  - `attackHandler`
  - `onAttack`

------

##### Statement vs Expression: 

- Expression returns a value, eg. can be on the riht side of a `=`

- an `if-`statement can NOT be on the right side of a `=`

https://stackoverflow.com/questions/12703214/javascript-difference-between-a-statement-and-an-expression

------

#### break

#### continue

------

#### labled statements

rarely needed

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/label



eg. to stop the outer loop of nested loops

give the loop a name

```js
let j = 0;
outerWhile: do {
  console.log('Outer', j);
  innerFor: for (let k = 0; k < 5; k++) {
      if (k === 3) {
        break outerWhile;
        // continue outerWhile; // dangerous! => Infinite loop!
      }
      console.log('Inner', k);
    }
    j++;
  } while (j < 3);
```

------

# Error Handling Try - catch

some errors can't be avoided

![image-20220104184632837](../../../../../Library/Application Support/typora-user-images/image-20220104184632837.png)



`try` a code, if an error occurs, use `catch`

throwig



convention: most errors have an object with a message property

```js
 if (isNaN(chosenMaxLife) || chosenMaxLife <= 0) {
    throw { message: 'invalid user input. enter a number' };
  }
```

throwing an error stops the execution of the code

## Try/Catch

```js
try {
  chosenMaxLife = getMaxLifeValues();
} catch (error) {
  console.log(error);
} finally {
// this will always be executed
}
```



##### `finally `

after `try`/`catch` (or just `try`) 



re-throwing an error: sometimes useful

```js
try {
  chosenMaxLife = getMaxLifeValues();
} catch (error) {
  console.log(error);
  throw error
} finally {
// this will always be executed
}
```

- often it is not needed
- code inside `finally` will also execute if an error occures. the rest of the code will not

------

#### Links

- Control Structures (MDN): https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling
- JavaScript Loops (MDN): https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration

------

# Behind the Scenes

the (weird) past

## ES5 vs ES6

Ecma-Script

![image-20220105122834425](../../../../../Library/Application Support/typora-user-images/image-20220105122834425.png)

ES5 first big Standardisation

ES6 (2015)

## var, let & const

![image-20220105123444094](../../../../../Library/Application Support/typora-user-images/image-20220105123444094.png)

#### Block Scope

`let` and `const` only care about curly braces `{}` 

you can create a scope: (not needed often)

```js
{
  let test = 5;
  console.log(test);
}
console.log(test); // -> error - not defined
```



#### Var

this does not throw an error:

```js
var name = 'Max';
var name = 'Anne';
```

this creates a global variable:

```js
if (name === 'Max') {
  var hobbies = ['Sport', 'Cooking'];
}
```

this can create nasty behaviour!

-› dont use `var`

------

## Hoisting

```js
console.log(userName);
var userName = 'Max';
// undefined
```

```js
console.log(userName);
let userName = 'Max';
// error
```

Hoisting: JS engine goes over the whole code and registers vars and functions

-› it is good to get an error

also

------

## Strict Mode

JS is a forgiving language wich can lead to messy code

with `var` this is possible:

```js
var userName = 'Max';
var userName = 'Moritz';
console.log(userName); // Moritz
```

also possible: (`var` is added automatically)

```js
userName = 'Max';
console.log(userName);
```

to avoid this, add `'use strict';`:

```js
'use strict';

userName = 'Max';
console.log(userName);
```

only for the scipt where this is placed in

Changes:

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode#changes_in_strict_mode

- no undeclared vars
- no reserved words `var undefined = 'Max';`

JavaScript modules are automatically in strict mode
