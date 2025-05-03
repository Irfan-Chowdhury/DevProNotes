<div align='center'>

# <span style="color: red;">TypeScript Tutorial</span>
</div>


## <span style="color: blue;">1.4 : Basic Data Types </span>
 
**Primitive & Non-Primitive Types**

**Primitive :**  number | string | boolean | null | undefined | symbol

**Non-Primitive :**  array | touple | object


**Code :**

```ts
// string 
let firstName : string = "Irfan";

//number
let rollNo : number = 123;

// boolean
let isAdmin : boolean = true;

//undefined
let x: undefined = undefined

//null
let y: null = null

//any
let z: any = 123;

//void
let a: void = undefined;

//object
let obj: object = {
    name: "Irfan",
    rollNo: 123,
    isStudent: true
};

//array
let hobbies : string[] = ["Reading", "Writing", "Coding"];
let numbers : number[] = [1, 2, 3, 4, 5];

//tuple --> array --> order --> types of values
let tuple : [string, number] = ["Irfan", 123];
let coordinates : [number, number] = [10.5, 20.5];
let ageName : [number, string, boolean] = [25, "Irfan", true]; 
ageName[0] = 30; // number

//enum
enum Color {
    Red,
    Green,
    Blue
}

let address : { street: string, city: string, zip: number } = {
    street: "123 Main St",
    city: "New York",
    zip: 10001
};
let student : { name: string, rollNo: number, isStudent: boolean } = {
    name: "Irfan",
    rollNo: 123,
    isStudent: true
};
```


## <span style="color: blue;">1-5 : Object, Optional and Literal Types</span>

```ts
// Reference Type --> Object 

const user: {
    company: string;
    firstName: string;
    lastName?: string; //optional Type
    isMarried: boolean;
    brand:'Pacific Knitex'; //literal type
} = {
    company: "Google Bangladesh",
    firstName: "Irfan",
    lastName: "Chowdhury",
    isMarried: false,
    brand: 'Pacific Knitex'
};
```

## <span style="color: blue;">1-6 : Function in typescript</span>


**Normal Function**

```ts
function add(num1:number, num2:number):number {
    return num1 + num2;
}

add(10, 20); // 30 

```

**Arrow Function**

```ts
const addArrow = (num1:number, num2:number):number => num1 + num2;
addArrow(10, 20); // 30
```

**Object-->Method**
```ts
// object --> function --> method 
const poorUser = {
    name: "Irfan",
    balance:0,
    addBalance(balance:number):string {
        return `Your balance is ${this.balance + balance}`;
    }
}
```

**Callback function**
```ts
const arr:number[] = [1, 2, 3, 4, 5];
const newArray:number[] = arr.map((elem:number): number => elem * elem);
```

## <span style="color: blue;">1-7 : Spread and Rest Operator</span>

**Spread Operator :**

```ts
// Example-1
const bros1: string[] = ['John', 'Jane', 'Jack'];
const bros2: string[] = ['Jill', 'Joe', 'Jim'];

bros1.push(...bros2); // ['John', 'Jane', 'Jack', 'Jill', 'Joe', 'Jim']

// Example-2
const mentors1= {
    typescript: 'Irfan',
    javascript: 'Ali',
    python: 'Ahmed'
}

const mentors2= {
    csharp: 'Sara',
    java: 'Sana',
    php: 'Sadiq'
}

const mentorList = {
    ...mentors1,
    ...mentors2
}
console.log(mentorList); // { typescript: 'Irfan', javascript: 'Ali', python: 'Ahmed', csharp: 'Sara', java: 'Sana', php: 'Sadiq' }
```


**Rest Operator :**
```ts
// Example-1
const greedFriends = (friend1:string, friend2:string, friend3:string):string => {
    console.log(`Hi ${friend1} and ${friend2}, and also hello to ${friend3}`);
};

greedFriends('John', 'Jane', 'Jack'); // Hi John and Jane, and also hello to Jack

// Example-2
const badFriends = (...friends:string[]) => {
    friends.forEach((friend:string) => console.log(`Hi ${friend}`))
};  

badFriends('John', 'Jane', 'Jack', 'Abul', 'kabul'); // Hi John and Jane, and also hello to Jack
```


## <span style="color: blue;">1-8 : Destructuring</span>


**code** 

```ts
const user = {
    id:345,
    name: {
        firstName: "Irfan",
        middleName: "Chowdhury",
        lastName: "Fahim"
    },
    contactNo: "01700000000",
    address: 'Dhaka Bangladesh'
};

const { 
    contactNo, 
    name: { middleName }, 
} = user;
console.log(contactNo); // 01700000000
console.log(middleName); // Chowdhury
```

**Array Destructuring**

```ts
const myFriends = ['Irfan', 'Shakib', 'Sabbir', 'Rafiq'];

// Option 1
const [a, b, bestFriendA] = myFriends;

// Option 2
const [, , bestFriendB, ...rest] = myFriends;
console.log(a); // Irfan
console.log(b); // Shakib
console.log(bestFriendB); // Sabbir
```


## <span style="color: blue;">1-9 : Type alias in typescript</span>

**Old Way**

***Example : 1***

```ts
    const student1 : {
        name:string,
        age:number,
        gender:string,
        contactNo:string,
        address:string,
    } = {
        name: "Irfan",
        age:50,
        gender:'male',
        contactNo: "01700000000",
        address: 'Dhaka Bangladesh'    
    }

    const student2 : {
        name:string,
        age:number,
        gender:string,
        address:string,
    } = {
        name: "Fahim",
        age:80,
        gender:'female',
        address: 'Chittagong Bangladesh'    
    }
```

**New Way**

***Example : 2***

```ts
    type Student = {
        name:string;
        age:number;
        contactNo?:string;
        gender:string;
        address:string;
    }

    const student3 : Student = {
        name: "Irfan",
        age:50,
        gender:"male",
        contactNo: "01700000000",
        address: 'Dhaka Bangladesh'
    }
```

***Example-3***
```ts
    type UserName = string;
    type IsAdmin = boolean;
    const UserName : UserName = "Irfan";
    const isAdmin : IsAdmin = true;
    console.log(UserName); // Irfan
    console.log(isAdmin); // true
```

**Function Alias**

***Example-4***

```ts
    type Add = (num1: number, num2:number) => number;
    const add: Add = (num1, num2) => num1 + num2;

    const result = add(10, 20);
    console.log(result); // 30
```


## <span style="color: blue;">1-10 : Union and Intersection types</span>


**Union types (OR), Symbol '|'**

***Example-1 :*** 
```ts
    type FrontendDeveloper = "fakibazDeveloper" | "juniorDeveloper";
    type FullstackDeveloper = "frontendDeveloper" | "expertDeveloper";

    type Developer = FrontendDeveloper | FullstackDeveloper;

    const newDeveloper : FrontendDeveloper = "juniorDeveloper";
```

***Example-2 :*** 
```ts
    type User = {
        name: string;
        email?: string;
        gender: "male" | "female";
        bloodGroup: "A+" | "B" | "AB+" | "O";
    }

    const user1: User = {
        name: "Fakibaz",
        gender:'male',
        bloodGroup: "A+"
    }
```

**Intersection types (AND), Symbol '&'**

***Example-3 :***
```ts
    type FrontendDeveloper = {
        skills: string[];
        designation1: "Frontend Developer";
    }

    type BackendDeveloper = {
        skills: string[];
        designation2: "Backend Developer";
    }

    type FullstackDeveloper = FrontendDeveloper & BackendDeveloper;

    const fullstackDeveloper : FullstackDeveloper = {
        skills: ["HTML", "CSS", "JavaScript", "Node.js"],
        designation1: "Frontend Developer",
        designation2: "Backend Developer",
    }
```
