<div align='center'>

# TypeScript With Laravel
</div>


### What is TypeScript
- Superset of JavaScript created by Microsoft
- Allows static strict typing
- Extra features - interfaces, enums, tuples, generics
- Supports modern features (arrow functions, let, const)
- Based on the .NET harmony specification


### What's wrong with JavaScript
- Not suitable for large application
- Lacks strong typing
- Weired inheritance, unfamiliar syntax
- Only errors during runtime
- Suffers type coercion


### Install TypeScript
Install TypeScript globally or locally in your project. It's recommended to install it locally within your project to avoid version conflicts. Run

```bash
npm install typescript --save-dev
```


### Create a tsconfig.json file: 
TypeScript requires a configuration file to specify compiler options. In your project's root directory, create a `tsconfig.json` file and copy-paste this full code.Or copy any `tsconfig.json` from typescript environment. 

```json
{
  "compilerOptions": {
    "target": "es2016",                                  
    /* Modules */
    "module": "commonjs",                               /* Specify what module code is generated. */
    "rootDir": "./resources/assets/ts",                 /* Specify the root folder within your source files. */
    "outDir": "./public/js/compiled_from_ts",           /* Specify an output folder for all emitted files. */
    "esModuleInterop": true,                             /* Emit additional JavaScript to ease support for importing CommonJS modules. This enables 'allowSyntheticDefaultImports' for type compatibility. */
    "forceConsistentCasingInFileNames": true,            /* Ensure that casing is correct in imports. */
    /* Type Checking */
    "strict": true,                                      /* Enable all strict type-checking options. */
    "skipLibCheck": true                                 /* Skip type checking all .d.ts files. */
  }
}

```

### Write TypeScript code : 
Create your TypeScript files in the specified directory (e.g., resources/assets). You can organize your files as needed and write your frontend logic in TypeScript.

file `invoice.ts`
```ts
let countryName:string = "Bangladesh";
console.log(countryName);
```

### Command : 
```bash
tsc <your_file.ts>
```

or compiled all .ts files automatically (recommended)
```bash
tsc -w
```
after command this, then goto `public/js/compiled_from_ts`. You'll see a `invoice.js` file created automatically.

### Include compiled JavaScript in your Blade views: 
Once you have the compiled JavaScript files, you can include them in your Blade views like any other JavaScript file:

```bash
@push('scripts')

<script src="{{ asset('js/compiled_from_ts/invoice.js') }}"></script>

// ... your other js code or file.

@endpush
```

Just include this in your expected file.

### jQuery (Optional): 
if you need jQuery then run the command - 

```bash
npm install @types/jquery --save-dev
```

import jquery in the .ts file
```bash
import * as $ from 'jquery';
```

#### Use $(document).ready(): 

You can then use $(document).ready() or its shorthand form $(function() { ... }) to run code when the DOM is ready:

```bash
$(function() {
    console.log(12);
}); 
```

<i><b>But if you've already imported jquery file in your layout, then you can ignore this jQuery import part</b></i>