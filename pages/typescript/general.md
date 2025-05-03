<div align='center'>

# TypeScript 
</div>

## How to install TypeScript

### Download Node.js

```bash
# Download and install nvm:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

# in lieu of restarting the shell
\. "$HOME/.nvm/nvm.sh"

# Download and install Node.js:
nvm install 22

# Verify the Node.js version:
node -v # Should print "v22.15.0".
nvm current # Should print "v22.15.0".

# Verify npm version:
npm -v # Should print "10.9.2".
```


### Install TypeScript

```bash
npm install -g typescript
```

Check Version 

```bash
tsc -v
```


### Configure `tsconfig.json`

1. First install `tsc` for typescript : 

  ```bash
    sudo apt install node-typescript
  ```

2. Generate New `tsconfig.json` file : 

```bash
    tsc --init
```

3. Configure the file : 

Search and Comment out 

```bash
    "rootDir": "./module1/src/", 
```
Example : if your path `root_directory/module1/src/index.ts`


```bash
    "outDir": "./module1/dist",
```
Example : if your path `root_directory/module1/dist/index.js`


4. After setup all config then open terminal on root directory and just type `tsc` and enter. It will generate or updated the `js` of `ts`


## ts-node-dev install

visit : https://www.npmjs.com/package/ts-node-dev

To see instant changes data in terminal by typescript.

**Install Globally**

 ```bash
 sudo npm i -g ts-node-dev
 ```

**Run the specific file**

```bash
ts-node-dev --respawn --transpile-only module1/src/1.11-Ternary-optiona.ts
```

here my file path loaction is : /var/www/html/typescript-technocrat/module1/src/1.11-Ternary-optiona.ts