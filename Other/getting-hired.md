# Getting Hired

* Show ability to solve problems
* Solve problems vocally and use pseudocode
* Show and explain past projects how they were done
* Communicate what you know clearly and with confidence. It's not about knowing a lot but make the best with what you know.

## LI

* Update headline to Front End Developer or React Developer
* Have a summary that shows passion and list keywords in it that are present in relevant job postings. List projects, talk about accomplishments, write about what I love doing and what I find exciting.
* Have a call to action for recruiters without a LI premium account
* Have a cover image with name, headline, and contact details
* Set open to new job and add job titles you're interested in
* Add location, remote, and immediate start date
* Under data privacy set sharing profile when you click apply to jobs
* Highlight transferable skills
* Describe specific accomplishments and go into detail, don't write generic responsibilities. Discuss results and showcase my extra miles, not the basics. Must look active, not passive.
* Add accomplishments (there's a category for it)
* Add certificates
* Add keywords from job postings everywhere on the profile, especially in the headline
* Have at least 5 skills listed
* Network on discord if no meetups, add new people

## FE

**Falsy values** are a set of unique values that evaluate to false, and there are six of them. Avoid using falsey values when writing code.

**Const, let and var** are all ways to declare variables. Const and let use block-scope and were introduced in ES6. This means the variables they create can only be used within their scope. Var is deprecated, and it uses lexical scope instead. With lexical scope, JS will create the variable as undefined, and only assign the value within its actual scope.

== compares value, === compares both type and value. 5 == '5' would be true, but 5 === '5' would be false. It's best to use strict equality **===** at all times.

**map(), filter() and reduce()** are very common methods and they all take functions as parameters. Map creates a new array and calls a function for each array element. Filter creates a new array and returns only the elements that pass the function. Reduce executes a reducer function for each array element, and only returns a single value at the end.

**Undefined** means a variable does not have a value, such as `let x`. **Null** can be used to assign an empty value and indicate it will have a value in the future.

Data types are divided in primitive (strings, numbers, booleans, BigInt, Symbol) and non-primitive (arrays, objects, map, set)

The **spread** can be used to copy an entire array or an object. The **rest** operator is used inside the parameter of a function to allow the passing of an array. The advantage to this is that you can pass an unlimited number of array elements.

Destructuring objects and arrays can make code more readable and provide intent. You can pull out values and reassign them to a new variable.

Git is the most popular form of version control. **Agile** is a process for how a sdev team is run, and it includes processes and procedures. The most common version of that is **Scrum**. Everything is based on team agreement, to decide whether something is finished, or anything else. Every organization is different on this.

Explain different types of **CSS selectors**: class, element, id, pseudo class `:hover`, pseudo element `::after`, compound selectors. Remember specificity.

**Responsive design** is essential to ensure a website is functional on multiple screen sizes. The best practice is developing mobile-first and using media queries combined with flex and grid. Also, use rem and em units.

Managing large numbers can be tricky in JS, it is recommended to use BigInt() or toFixed(2) to fix decimals.

Passing by **value** occurs whenever you're passing the value of a variables to anything, without changing the variable. Passing by **reference** will actually modify the initial variable.

Promises are used with any async action, most commonly used when working with APIs calls.

```js
function getPost() {
    console.log(1);
    
    fetch('https://jsonplaceholder.typicode.com/posts/1')
    .then((data) => data.json())
    .then((json) => console.log(2))
    .catch((error) =>  console.log(e));

    console.log(3);
} 
```

Equivalent to the below.

```js
async function getPost() {
    console.log(1);

    try {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts/1');
    const json = await response.json();
    console.log(json);
        
    } catch(e) {
        console.log(e)
    }
    
    console.log(3);
}
```

## Generic Questions and Tips

* How do you stay up to date?
* Why you?
* Why us?
* Biggest professional achievement?

~

* Make eye contact and be human
* Apply daily
* Meetups and network

~

* What's the project?
* What's the team like?
* What code quality standards do you follow, i.e. testing?
* What's the best part of working here?
* Why are you interest in hiring me?
* Finish with a statement of some achievement. Make sure to leave the interview with a positive note.

## Github

* Pin important repos, customize pins
* Have a repo with all certificate images and a readme
* Fill out the profile
* Refactor old projects and update constantly, even for small things

## CV

* Contact details
* Clear summary, brag and stand out
* Tech skills, break it down by section and make it easy to understand: FE, BE, Principles and Methodologies, anything
* Personal projects with the actual URL, not links
* Work experience with information about the companies
* References on cv directly?
* Bold keywords so they stand out
* Add certificates with descriptions and dates
* Maybe two columns
* novoresume.com

## React

The Virtual DOM acts as a copy of the real DOM, and it can be updated without refreshing the entire page. It's a pattern, not a specific technology. `react-dom` syncs it with the real DOM, which directly manipulates the HTML. In short, the key is **diffing**: the virtual DOM updates the state of the DOM based on only what has changed in state.

JSX is short for JavaScript XML and it allows to write JS with an HTML-like syntax, and it produces elements that represent objects. JSX produces elements, and componenents are functions that return an element.

Values are passed from parent to child with props. Children can't pass props, but if they are receiving a function prop from the parent, they can return values when calling it. Props are read-only.

Props and state are both JS objects, but only props can be passed. State can only be accessed within a given component.

UseEffect is used to update lifecycle components in function components. It runs on mount, and updates on what is given in the dependencies array. The return value of UseEffect is a cleanup function, and it should remove things like event listeners.

The Context API implicitly states what values a given child component can have, without having to pass them down several branches with prop drilling.

Fragments are empty elements, essentially containers to hold other elements in.

Uncontrolled components are controlled by the user, not by React, for example forms and inputs. Controlled components are the solution to that: React controls the state changes happening in an input.
