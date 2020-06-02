# NPR IT Devs Typescript Style Guide


<a name="table-of-contents"></a>

# TypeScript Style Guide

This is the TypeScript style guide that we aim to use for NPR IT DevTeam codebases.

## Table of Contents

  1. [Formatting](#Formatting)
  0. [Files](#files)
  0. [Quotes](#quotes)
  0. [Commas](#commas)
  0. [Comments](#comments)
  0. [Variable Declarations](#variable-declarations)
  0. [Function Declarations](#function-declarations)
  0. [Anonymous Functions](#anonymous-functions)
  0. [Names](#names)
      - [Variables, Modules, and Functions](#variables-modules-and-functions)
      - [Use of var, let, and const](#use-of-var-let-and-const)
      - [Types](#types)
      - [Classes](#classes)
      - [Interfaces](#interfaces)
      - [Constants](#constants)
  0. [Statements](#statements)
  0. [Object and Array Literals](#object-and-array-literals)
  0. [Assignment Expressions](#assignment-expressions)
  0. [=== and !== Operators](#-and--operators)
  0. [Promises and Async/Await](#promises-and-async-await)
  0. [Typings](#assignment-expressions)
      - [External](#external)
      - [Internal](#internal)
  0. [Eval](#eval)
  0. [Other Sources/Guides](#Other-Sources/Guides)


**[top](#table-of-contents)**

## Formatting

  - Use <https://prettier.io/> for formatting
  - Devs should use this VS Code plugin: <https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode>
  - It is highly recommended to auto-format on save (this will be the default project settings for for vscode)
  - The unit of indentation is two spaces.

## Files
  - All TypeScript files must have a ".ts" or ".tsx" extension.
  - It is OK to separate words with periods or dashes (e.g. `my.view.html`).
  - Angular usually should end the respective class type ie `.component` or `.service` and so on
  - **All files should end in a new line.** This is necessary for some Unix systems.


**[top](#table-of-contents)**


## Quotes
  - Use single-quotes `''` for all strings, and use double-quotes `""` for strings within strings.
  - When you need to use an apostrophe inside a string it is recommended to use double-quotes.

  ```typescript
  // bad
  let greeting = "Hello World!";

  // good
  let greeting = 'Hello World!';

  // bad
  let phrase = 'It\'s Friday!';

  // good
  let phrase = "It's Friday!";

  // bad
  let html = "<div class='bold'>Hello World</div>";

  // bad
  let html = '<div class=\'bold\'>Hello World</div>';

  // good
  let html = '<div class="bold">Hello World</div>';

  // bad
  let template = `string text string text`;

  // good
  let template = `string text ${expression} string text`;
  ```

**[top](#table-of-contents)**

## Commas
  - Use trailing commas always. DO NOT USE leading commas.
  - Always use an additional trailing comma for cleaner git diffs and merges

  ```typescript
  // bad
  const person = {
      firstName: 'Jane'
    , lastname: 'Smith'
    , email: 'jane.smith@npr.org'
  };

  // good
  const person = {
      firstName: 'Jane',
      lastname: 'Smith',
      email: 'jane.smith@npr.org',
  };
  ```

**[top](#table-of-contents)**

## Comments

  - Comments are strongly encouraged. It is very useful to be able to read comments and understand the intentions of a given block of code.
  - Try to include meaningful and comments that show your intention. 
  - If the code is tricky explain why and how it works
  - If you use `setTimeout` you should explain why

  - All public functions should have a comment block `/**...*/` using [JSDoc](http://usejsdoc.org/) style comments.

JSDocs can be interpreted by IDEs for better intellisense. Below is an example of a JSDoc comment block for a function.

  ```typescript
  /**
   * Takes in a name and returns a greeting string.
   *
   * @param name The name of the greeted person.
   */
  function getGreeting(name: string): string {
      return 'Hello ' + name + '!';
  }
  ```

**[top](#table-of-contents)**

### Comments: Todo and Code Review

`TODO` and `code-review` annotations help you quickly find things that need to be fixed/implemented.

  - Use `// TODO:` or `// todo` to annotate solutions that need to be implemented.
  - Use `// code-review:` to annotate problems the need to be fixed or questions for code review meetings.

**[top](#table-of-contents)**

## Variable Declarations

  - All variables must be declared prior to using them. 
  - Use `const` for vars that will never change
  - Use `let` or `const`
  - You should not use `var`
  - Avoid global variables

## Function Declarations

  - All functions must be declared before they are used.
  - You should explicitly declare the return type
  - You should try to return early to avoid a lot of nesting

  ```typescript
  // good
  function foo(): string {
      return 'foo';
  }
  ```

**[top](#table-of-contents)**

## Anonymous Functions

  - All anonymous functions should be defined as fat-arrow/lambda `() => { }` functions unless it is absolutely necessary to preserve the context in the function body.
  - All fat-arrow/lambda functions should have parenthesis `()` around the function parameters.

  ```typescript
  // bad
  clickAlert() {
      let element = document.querySelector('div');

      this.foo = 'foo';

      element.addEventListener('click', function(ev: Event) {
          // this.foo does not exist!
          alert(this.foo);
      });
  }

  // good
  clickAlert() {
      let element = document.querySelector('div');

      this.foo = 'foo';

      element.addEventListener('click', (ev: Event) => {
          // TypeScript allows this.foo to exist!
          alert(this.foo);
      });
  }
  ```

  - Always surround the function block with braces `{}`

**[top](#table-of-contents)**

## Names

  - All variable and function names should be formed with alphanumeric `A-Z, a-z, 0-9` and underscore `_` charcters.

### Variables, Modules, and Functions

  - Variable, module, and function names should use lowerCamelCase.

### Use of var, let, and const

  - Use `const` where appropriate, for values that never change
  - Use `let` everywhere else
  - Avoid using `var`

**[top](#table-of-contents)**

### Types

  - Always favor type inference over explicit type declaration except for function return types
  - Always define the return type of functions. This can help catch errors as the functions evolve.
  - Types should be used whenever necessary (no implicit `any`).
  - Arrays should be defined as `type[]` instead of `Array<type>` .
  - Use the `any` type sparingly, it is always better to define an interface.

  ```typescript
  // bad
  let numbers = [];

  // bad
  let numbers: Array<number> = [];

  // good
  let numbers: number[] = [];
  ```

**[top](#table-of-contents)**

### Classes

  - Classes/Constructors should use UpperCamelCase (PascalCase).
  - `Private` and `private static` members in classes should be denoted with the `private` keyword.
  - `Protected` members in classes do not use the `private` keyword.
  - Default to using `protected` for all instance members
  - Use `private` instance members sparingly
  - Use `public` instance members only when they are used by other parts of the application.

  ```typescript
  class Person {
      protected fullName: string;

      constructor(public firstName: string, public lastName: string) {
          this.fullName = firstName + ' ' + lastName;
      }

      public toString() {
          return this.fullName;
      }

      protected walkFor(millis: number) {
          console.log(this.fullName + ' is now walking.');

          // Wait for millis milliseconds to stop walking
          setTimeout(() => {
              console.log(this.fullName + ' has stopped walking.');
          }, millis);
      }
  }
  ```

**[top](#table-of-contents)**

### Interfaces

  - Interfaces should use UpperCamelCase.
  - Interfaces should be prefaced with the capital letter I.
  - Only `public` members should be in an interface, leave out `protected` and `private` members.

  ```typescript
  interface IPerson {
      firstName: string;
      lastName: string;
      toString(): string;
  }
  ```

**[top](#table-of-contents)**


## Statements

### Simple

  - Each line should contain at most one statement
  - A semicolon should be placed at the end lines

**[top](#table-of-contents)**

### Compound

Compound statements are statements containing lists of statements enclosed in curly braces `{}`.

  - The enclosed statements should start on a newline.
  - The enclosed statements should be indented

  ```typescript
  // bad
  if (condition === true) { alert('Passed!'); }

  // good
  if (condition === true) {
      alert('Passed!');
  }
  ```
  - The left curly brace `{` should be at the end of the line that begins the compound statement.
  - The right curly brace `}` should begin a line and be indented to align with the line containing the left curly brace `{`.

  ```typescript
  // bad
  if (condition === true)
  {
      alert('Passed!');
  }

  // good
  if (condition === true) {
      alert('Passed!');
  }
  ```

  - **Braces `{}` must be used around all compound statements** even if they are only single-line statements.

  ```typescript
  // bad
  if (condition === true) alert('Passed!');

  // bad
  if (condition === true)
      alert('Passed!');

  // good
  if (condition === true) {
      alert('Passed!');
  }
  ```

If you do not add braces `{}` around compound statements, it makes it very easy to accidentally introduce bugs.

  ```typescript
  if (condition === true)
      alert('Passed!');
      return condition;
  ```

It appears the intention of the above code is to return if `condition === true`, but without braces `{}` the return statement will be executed regardless of the condition.

  - Compount statements do not need to end in a semicolon `;` with the exception of a `do { } while();` statement.

**[top](#table-of-contents)**

### Return

  - If a `return` statement has a value you should not use parenthesis `()` around the value.
  - The return value expression must start on the same line as the `return` keyword.

  ```typescript
  // bad
  return
      'Hello World!';

  // bad
  return ('Hello World!');

  // good
  return 'Hello World!';
  ```

  - It is recommended to take a return-first approach whenever possible.

  ```typescript
  // bad
  function getHighestNumber(a: number, b: number): number {
      let out = b;

      if(a >= b) {
          out = a;
      }

      return out;
  }

  // good
  function getHighestNumber(a: number, b: number): number {
      if(a >= b) {
          return a;
      }

      return b;
  }
  ```

  - Always **explicitly define a return type**. This can help TypeScript validate that you are always returning something that matches the correct type.

  ```typescript
  // bad
  function getPerson(name: string) {
      return new Person(name);
  }

  // good
  function getPerson(name: string): Person {
      return new Person(name);
  }
  ```

**[top](#table-of-contents)**

### If

  - Alway be explicit in your `if` statement conditions.

  ```typescript
  // bad
  function isString(str: any) {
      return !!str;
  }

  // good
  function isString(str: any): str is string {
      return typeof str === 'string';
  }
  ```

Sometimes simply checking falsy/truthy values is fine, but the general approach is to be explicit with what you are looking for. This can prevent a lot of unncessary bugs.


**[top](#table-of-contents)**

### For

For statements should have the following form:

  ```typescript
  for(/* initialization */; /* condition */; /* update */) {
      // ...
  }

  let keys = Object.keys(/* object */);
  let length = keys.length;

  for(let i = 0; i < length; i += 1) {
      // ...
  }
  ```

Object.prototype.keys is supported in `ie >= 9`.

  - Use Object.prototype.keys in lieu of a `for...in` statement.

With TypeScript you can use `for...of` statements:

  ```typescript
  let arr = [2, 3, 4];

  for (const value of arr) {
      // ...
  }
  ```

**[top](#table-of-contents)**

### Switch

Switch statements should have the following form:

  ```typescript
  switch (/* expression */) {
      case /* expression */:
          // ...
          /* termination */
      default:
          // ...
  }
  ```

  - Each switch group except default should end with `break`, `return`, or `throw`.

**[top](#table-of-contents)**

### Try

  - Try statements should be avoided whenever possible. They are not a good way of providing flow control.
  - Try statements should be used when using `async/await` syntax.

Try statements should have the following form:

  ```typescript
  try {
      // ...
  } catch (error: Error) {
      // ...
  }

  try {
      // ...
  } catch (error: Error) {
      // ...
  } finally {
      // ...
  }
  ```

**[top](#table-of-contents)**

### Continue

  - It is recommended to take a continue-first approach in all loops.

**[top](#table-of-contents)**

### Throw

  - Avoid the use of the throw statement unless absolutely necessary.
  - Flow control through try/catch exception handling is not recommended.

**[top](#table-of-contents)**


## Object and Array Literals

  - Use curly braces `{}` instead of `new Object()`.
  - Use brackets `[]` instead of `new Array()`.

**[top](#table-of-contents)**

## === and !== Operators

  - It is better to use `===` and `!==` operators whenever possible.
  - `==` and `!=` operators do type coercion, which can lead to headaches when debugging code.

**[top](#table-of-contents)**

## Promises and Async/Await

  - Always use `async/await` wherever possible. Avoid using `Promise.then` and `Promise.catch`.

  ```typescript
  // bad
  function reddits(): Promise<reddit.IListing> {
      return fetch('https://www.reddit.com/r/all.json')
          .then((response) => {
              return response.json();
          })
          .then((result) => {
              return result.data;
          })
          .catch((error) => {
              console.log(error);

              return {
                  kind: 'Listing',
                  data: {
                      children: [],
                  },
              };
          });
  }

  // good
  async function reddits(): Promise<reddit.IListing> {
      try {
          const response = await fetch('https://www.reddit.com/r/all.json');

          return response.json();
      } catch(error) {
          console.log(error);

          return {
              kind: 'Listing',
              data: {
                  children: [],
              },
          };
      }
  }
  ```

**[top](#table-of-contents)**

## Typings

### External

  - Typings are sometimes packaged with node modules, in this case you don't need to do anything
  - Use `@types` for all external library declarations not included in `node_modules`
  - Actively add/update/contribute typings when they are missing

## Eval

  - **Never use eval**
  - **Never use the Function constructor**
  - **Never pass strings to `setTimeout` or `setInterval`**

**[top](#table-of-contents)**

## Lint

  - Always use a Linter. TSLint for now but ESLint is the future.


**[top](#table-of-contents)**


## Other Sources/Guides

Original source/Adopted from: https://github.com/Platypi/style_typescript

Other guides:

- <https://github.com/Microsoft/TypeScript/wiki/Coding-guidelines>
- <https://github.com/Platypi/style_typescript>
- <https://basarat.gitbook.io/typescript/styleguide>
- <https://github.com/airbnb/javascript> (js)

**[top](#table-of-contents)**