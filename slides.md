---
class: 'text-center'
transition: slide-left
highlighter: 'prism'
lineNumbers: true
colorSchema: 'dark'
defaults:
  layout: 'center'
  class: 'text-center'
---

# Clean Code

Mehmet Pekcan <span class='text-blue-500'>@atlassian</span>





---​
class: 'bg-white'
---

<img src='/assets/clean-code-meme.jpg' />






---
class: 'text-center'
---

<div class='grid grid-cols-2 gap-16'>
  <div>
    <h4 class='font-bold'>Maintenable</h4>
    <span class='text-xs'>Easy to read, understand and modify.</span>
  </div>
  <div>
    <h4 class='font-bold'>Scalable</h4>
    <span class='text-xs'>Easy to extend it by adding new features.</span>
  </div>
  <div>
    <h4 class='font-bold'>Debugging</h4>
    <span class='text-xs'>Easy to find bugs and fix them.</span>
  </div>
  <div>
    <h4 class='font-bold'>Collaboration</h4>
    <span class='text-xs'>Easy to understand by others.</span>
  </div>
</div>





---
class: 'text-center'
---

# Variables

Variable names should tell what its for in glance.






---
class: 'text-center'
---

# Use meaningful names

Be explanatory on your naming

```javascript {1|3}
const button = document.querySelector(...);

const registerButton = document.querySelector(...);
```







---
class: 'text-center'
---

# Use consistent names

Don't have more than one reference for similar things, instead have them one

```javascript {1-3|5|7-9|11-13}
getClientData();
getUserInfo();
getCustomerDetails();

getClient();

const some_constant = 5;
const ANOTHER_CONSTANT = '....';
const someOther = '...';

const SOME_CONSTANT = 5;
const ANOTHER_CONSTANT = '....';
const SOME_OTHER = '....';
```






---
class: 'text-center'
---

# Use searcahble names

Have names that can easy to search/predict

```javascript {1|3-4}
setTimeout(fetchUsers, 86400000);

const MILLISECONDS_PER_DAY = 60 * 60 * 24 * 1000;
setTimeout(refreshDashboard, MILLISECONDS_PER_DAY);
```






---
class: 'text-center'
---

# Use constants

Have constant variables for static things.

```javascript {1-7|9-17}
const checkUserIsInLegitAge = (user) => {
  if(user.age >= 18) {
    return true;
  }

  return false;
};

const LEGIT_AGE_LIMIT = 18;

const checkUserIsInLegitAge = (user) => {
  if(user.age >= LEGIT_AGE_LIMIT) {
    return true;
  }

  return false;
};
```





---
class: 'text-center'
---

# Use constants

Have constant variables for static things.

```javascript{1-5|7-15}
let sum = 0;

for (let i = 0; i <= 5; i++) {
  s += 8 * 5 * 1.2;
}

const WORK_HOURS_PER_DAY = 8;
const WORK_DAYS_PER_WEEK = 5;
const BONUS_MULTIPLIER = 1.2;

let totalSalary = 0;

for (let index = 0; index <= WORK_DAYS_PER_WEEK; index++) {
  totalSalary += WORK_HOURS_PER_DAY * WORK_DAYS_PER_WEEK * BONUS_MULTIPLIER;
}
```





---
class: 'text-center'
---


# Avoid misleading

Don't use misleading abbrevations

```javascript {1|3}
const orgPath = '../path/to/folder';

const originPath = '../path/to/folder';
```




---
class: 'text-center'
---


# Avoid mental mapping

Always be explicit rather than implict

```javascript {1-10|12-21}
managers.forEach(m => {
  doSomething();
  doAnotherThing();

  m.directReporters.forEach(w => {
    doSomeHotStuff();
    // ...
    doLastThing(m); // ??? What was `m`?
  })
})

managers.forEach(manager => {
  doSomething();
  doAnotherThing();

manager.directReporters.forEach(reporter => {
    doSomeHotStuff();
    // ...
    doLastThing(manager);
  })
})
```





---
class: 'text-center'
---

# Don't repeat the same thing

```javascript {1-9|11-19}
const user = {
  userAge: 23,
  userName: 'Name',
  userSurname: 'Surname',
  // ..
}

user.userName
user.userSurname

const user = {
  age: 23,
  name: 'Name',
  surname: 'Surname',
  // ..
}

user.name
user.surname
```






---
class: 'text-center'
---

# Functions

A function name should tell what it does for in glance.








---
class: 'text-center'
---

# Have descriptive name

Start with always verb, and be descriptive what that function do

```javascript {1-3|5-7}
function sum(x, y) {
  return x + y;
}

function addNumbers(firstNumber, secondNumber) {
  return firstNumber + secondNumber;
}
```










---
class: 'text-center'
---

# Do one thing

One of the most important ones. Easy to test, compose, refactor.

```javascript {1-9|11-21}
function processUser(accountId, newName, newEmail) {
    const user = database.fetchUser(accountId);
    user.name = newName;
    user.email = newEmail;
    database.saveUser(user);

    const updateMessage = `Updated: ${newName}!`;
    emailService.sendEmail(newEmail, updateMessage);
}

function updateUser(accountId, newName, newEmail) {
    const user = database.fetchUser(accountId);
    user.name = newName;
    user.email = newEmail;
    database.saveUser(user);
}

function sendUpdateNotification(newName, newEmail) {
    const updateMessage = `Updated: ${newName}!`;
    emailService.sendEmail(newEmail, updateMessage);
}
```



---
class: 'text-center'
---

# Have 2 or less parameter

Limiting the parameter is extremely important to test, and maintain the function

```javascript {1-3|5-7}
function createEmployee(name, age, address, position, department) {
  // ..
}

function createEmployee(employeeInfo) {
  // ..
}
```




---
class: 'text-center'
---

# Remove duplicate code

```javascript {1-11|13-20}
function discountForStudent(price) {
    return price - price * 0.2;
}

function discountForSenior(price) {
    return price - price * 0.1;
}

function discountForVeteran(price) {
    return price - price * 0.3;
}

function applyDiscount(price, discountRate) {
    return price - price * discountRate;
}

// Somewhere in the code
const studentPrice = applyDiscount(price, 0.2);
const seniorPrice = applyDiscount(price, 0.1);
const veteranPrice = applyDiscount(price, 0.3);
```





---
class: 'text-center'
---

# Avoid passing flags

```javascript{1-10|12-22}
function createReport(data, isDetailed) {
    let report;
    // some common report creation code...

    if (isDetailed) {
      // code to create a detailed report...
    }

    return report;
}

function createSummaryReport(data) {
    let report;
    // code to create a summary report...
    return report;
}

function createDetailedReport(data) {
    let report;
    // code to create a detailed report...
    return report;
}
```






---
class: 'text-center'
---

# Avoid side effects

```javascript {1-9|11-19}
let name = 'Mehmet';

function greet() {
  name = 'Ahmet';
  return `Hello, ${name}!`;
}

console.log(greet()); // "Hello, Ahmet!"
console.log(name); // "Ahmet"

let name = 'Ahmet';

function greet(name) {
  let newName = 'Mehmet';
  return `Hello, ${newName}!`;
}

console.log(greet(name)); // "Hello, Mehmet!"
console.log(name); // "Ahmet"
```





---
class: 'text-center'
---

# Avoid side effects

```javascript {1-3|5-7}
const addItemToCart = (cart, item) => {
  cart.push({ item, date: Date.now() });
};

const addItemToCart = (cart, item) => {
  return [...cart, { item, date: Date.now() }];
};
```



---
class: 'text-center'
---

# Encapsulate conditions 

```javascript {1-3|5-11}
if (basketStore.state === "fetching" && isEmpty(listNode)) {
  // ...
}

function shouldShowSpinner(basketStore, listNode) {
  return basketStore.state === "fetching" && isEmpty(listNode);
}

if (shouldShowSpinner(basketStore, listNodeInstance)) {
  // ...
}
```



---
class: 'text-center'
---

# Avoid negative conditionals

```javascript {1-5|7-11}
if (!isNotLoggedIn) {
    // ...
} else {
    // ...
}

if (isLoggedIn) {
    //  ...
} else {
    //  ...
}
```



---
class: 'text-center'
---

# Comments

Comment only when your code can <span class='underline'>not</span> explain itself.





---
class: 'text-center'
---


# Comment business logics & clarifications

```javascript {1-5|7-10}
// Setting variable x to 10
let productStock = 10;

// Adding 5 to x
productStock = productStock + 5;

let productStock = 10;

// Adding 5 to stock to account for the 5-unit buffer in warehouse stock
productStock = productStock + 5;
```




---
class: 'text-center'
---


# Don't leave any commented out codes



---
class: 'text-center'
---


# Avoid positional markers

```javascript {1-16|18-24}
// ---------
// Variables
// ---------
let x = 10;
let y = 20;

// ------------
// Calculations
// ------------
let sum = x + y;
let product = x * y;

// -----
// Output
// -----
console.log(sum, product);

let x = 10;
let y = 20;

let sum = x + y;
let product = x * y;

console.log(sum, product);
```




---
class: 'text-center'
---


# Thank you!

Any questions?
