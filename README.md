## Deploy Next.JS App in Firebase using Firebase Cloud Functions

Resource:

- [Cloud Function](https://firebase.google.com/docs/functions)
- [Custom Server](https://nextjs.org/docs/advanced-features/custom-server)

### Start Application

Use `npm run deploy` to build files and upload Cloud functions & hosting to Firebase.

### Setup

1. Create server.js file to handle page request

```
exports.nextServer = functions.https.onRequest((req, res) => {
  return app.prepare().then(() => handle(req, res));
});
```

2. Update firebase.json using below codebase. Function name should be the same as your function in server.js

```
{
  "hosting": {
    "public": "public",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ],
    "rewrites": [
      {
        "source": "**",
        "function": "nextServer"
      }
    ]
  },
  "functions": [
    {
      "source": ".",
      "runtime": "nodejs16"
    }
  ]
}
```
