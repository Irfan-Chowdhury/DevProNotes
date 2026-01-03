Problems are given by Programming Hero.

<br>

## 1. Task: Array Filtering and Mapping

#### Create an array of objects, each representing a person with properties like name, age, and gender. Write a function to filter out all females and then map the remaining people to an array of names. Print the final result.

```js
const people = [
  { name: "Asha", age: 22, gender: "female" },
  { name: "Rafi", age: 25, gender: "male" },
  { name: "Nabil", age: 19, gender: "male" },
  { name: "Mitu", age: 21, gender: "female" },
];

function maleNames(arr) {
  return arr
    .filter(person => person.gender !== "female")
    .map(person => person.name);
}

console.log(maleNames(people)); // ["Rafi", "Nabil"]

```

---


## 2. Task: Object Manipulation

#### Create an array of objects representing books with properties like title, author, and year. Write a function that takes the array and returns a new array with only the book titles. Print the result.



```js
const books = [
  { title: "Clean Code", author: "Robert C. Martin", year: 2008 },
  { title: "The Pragmatic Programmer", author: "Andrew Hunt", year: 1999 },
  { title: "You Don't Know JS", author: "Kyle Simpson", year: 2015 },
];

function getBookTitles(arr) {
  return arr.map(book => book.title);
}

console.log(getBookTitles(books));
```

---

## 3. Task: Function Composition

#### Write three functions: one to square a number, one to double a number, and one to add 5 to a number. Compose these functions to create a new function that squares a number, doubles the result, and then adds 5.

```js
const square = (n) => n * n;
const double = (n) => n * 2;
const add5 = (n) => n + 5;

// manual composition:
const composed = (n) => add5(double(square(n)));

console.log(composed(3)); // square(3)=9, double=18, add5=23
```

Bonus (generic compose helper):

```js
const compose = (...fns) => (x) => fns.reduceRight((v, fn) => fn(v), x);
const composed2 = compose(add5, double, square);
console.log(composed2(3)); // 23
```

---

## 4. Task: Sorting Objects

#### Create an array of objects representing cars with properties like make, model, and year. Write a function to sort the array of cars by the year of manufacture in ascending order. Print the sorted array.



```js
const cars = [
  { make: "Toyota", model: "Corolla", year: 2015 },
  { make: "Honda", model: "Civic", year: 2012 },
  { make: "Tesla", model: "Model 3", year: 2020 },
];

function sortCarsByYear(arr) {
  // copy first so original is not changed
  return [...arr].sort((a, b) => a.year - b.year);
}

console.log(sortCarsByYear(cars));
```

---

## 5. Task: Find and Modify

#### Write a function that searches an array of objects for a specific person by name. If found, modify their age property. Print the updated array.

```js
const persons = [
  { name: "Rafi", age: 25 },
  { name: "Asha", age: 22 },
];

function updateAgeByName(arr, targetName, newAge) {
  return arr.map(p =>
    p.name === targetName ? { ...p, age: newAge } : p
  );
}

const updated = updateAgeByName(persons, "Asha", 30);
console.log(updated);
```

(Above way is best in interviews because it doesn’t mutate original array.)

---

## 6. Task: Array Reduction

#### Create an array of numbers. Write a function that uses the reduce method to calculate the sum of all even numbers in the array.

```js
const nums = [1, 2, 3, 4, 5, 6, 10];

function sumEven(arr) {
  return arr.reduce((sum, n) => {
    if (n % 2 === 0) return sum + n;
    return sum;
  }, 0);
}

console.log(sumEven(nums)); // 22 (2+4+6+10)
```

---

## 7. Task: Leap Year Checker

#### Write a function that determines whether a given year is a leap year.

Rules:

* divisible by 400 ✅ leap
* divisible by 100 ❌ not leap
* divisible by 4 ✅ leap

```js
function isLeapYear(year) {
  if (year % 400 === 0) return true;
  if (year % 100 === 0) return false;
  return year % 4 === 0;
}

console.log(isLeapYear(2024)); // true
console.log(isLeapYear(2100)); // false
```

---

## 8. Task: Unique Values

#### Create an array of numbers with some duplicate values. Write a function to filter out the duplicate values and return a new array with only unique numbers. Print the result.

```js
const numbers = [1, 2, 2, 3, 4, 4, 5];

function uniqueNumbers(arr) {
  return [...new Set(arr)];
}

console.log(uniqueNumbers(numbers)); // [1,2,3,4,5]
```

---

## 9. Task: Advanced Sorting

#### Create an array of objects representing students with 'name' and 'grades' properties. Write a function to sort the students by average grade in descending order.



```js
const students = [
  { name: "Rafi", grades: [80, 90, 85] },
  { name: "Asha", grades: [95, 92, 96] },
  { name: "Nabil", grades: [70, 75, 72] },
];

function avg(grades) {
  return grades.reduce((sum, g) => sum + g, 0) / grades.length;
}

function sortByAvgDesc(arr) {
  return [...arr].sort((a, b) => avg(b.grades) - avg(a.grades));
}

console.log(sortByAvgDesc(students));
```

---

## 10. Task: Functional Programming - Reduce

#### Write a function that uses the reduce function to calculate the total value of an array of objects with a 'quantity' and 'price' property

```js
const items = [
  { quantity: 2, price: 50 },
  { quantity: 1, price: 120 },
  { quantity: 3, price: 10 },
];

function totalValue(arr) {
  return arr.reduce((total, item) => total + item.quantity * item.price, 0);
}

console.log(totalValue(items)); // 2*50 + 1*120 + 3*10 = 250
```

---