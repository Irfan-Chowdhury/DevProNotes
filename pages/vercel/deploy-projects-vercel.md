<div align='center'>

# How to deploy projects in Vercel
</div>


## For Frontend

### ✅ Create `vercel.json` file and paste the code 

```json
{
  "rewrites": [
    {
      "source": "/(.*)",
      "destination": "/index.html"
    }
  ]
}
```

### ✅ After finishing your project then build the project

```bash
npm run build
```

### ✅ Then run this command to deploy in vercel

```bash
vercel
```

### ✅ In command section, they will ask you some question. Answer this.

**? Set up and deploy “/var/www/html/Programming-Hero/Level-2 (Next Web Devleopment)/Mission-4/Module-24 (Assignment)/library-management-frontend”?**  *`yes`*

**? Which scope should contain your project?** *`irfanchowdhury's projects`*

**? Link to existing project?** *`no`*

**? What’s your project’s name?** *`library-management-frontend`*

**? In which directory is your code located?** *`./`*

**? Want to modify these settings?** *`no`*

<br>

### ✅ To modify and then have to upload the updated file, 

before build the project ad then just follow the command

```bash
vercel --prod
```

<br>

## For Backend

### ✅ Create `vercel.json` file and paste the code 

```json
{
    "version": 2,
    "builds": [
        {
            "src": "dist/server.js",
            "use": "@vercel/node"
        }
    ],
    "routes": [
        {
            "src": "/(.*)",
            "dest": "dist/server.js"
        }
    ]
}
```

### ✅ Then follow Frontend part same as it is.


## Common Error : 
## Problem-1 :
 Access to fetch at 'https://library-management-backend-node-iuiaxte0p.vercel.app/api/books' from origin 'http://localhost:3000' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource. If an opaque response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disabled.

### Solution: Cors Setup

i) Install cors
```bash
npm i cors
```

ii) import & write code in server part `src/app.ts`
```bash 
import cors from 'cors'; 

const allowedOrigins = [
  "http://localhost:3000",
  "https://library-management-frontend-eta-umber.vercel.app"
];

app.use(cors({
  // origin: "*",
  origin: (origin, callback) => {
    if (!origin || allowedOrigins.includes(origin)) {
      callback(null, true);
    } else {
      callback(new Error("Not allowed by CORS"));
    }
  },
  methods: ["GET", "POST", "PUT", "PATCH", "DELETE", "OPTIONS"],
}));
```

iii) in Frontend Part, open `.env` file and add the server deploy link

```bash
VITE_BASE_URL="https://library-management-server-tau.vercel.app/api/"
```