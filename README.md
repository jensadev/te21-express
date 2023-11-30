# Node webbserver

https://expressjs.com/

Bygga en monolit.

## Hello world

- Start terminal, wsl
- Make sure nvm is installed
- mkdir te21-webbserver
- npm init -y
- npm i express
- touch index.js
- edit package.json
    
    ```
    "scripts": {
        "dev": "node index.js"
      },
    ```
    
- edit index.js

```
const express = require("express")
const app = express()

const port = process.env.PORT || 3000

app.get("/", (req, res) => {
  res.send("Hello World!")
})

app.listen(port, () => {
  console.log(`Server running on port ${port}`)
})
```

- mkdir public
- touch public/index.html

```jsx
const express = require("express")
const app = express()

const port = process.env.PORT || 3000

app.use(express.static("public"))

app.get("/hello", (req, res) => {
  res.send("Hello World!")
})

app.listen(port, () => {
  console.log(`Server running on port ${port}`)
})
```

## Express generator

Go to code directory.

- npx express-generator --no-view --git te21-express
    - Vi vill inte ha en view för vi ska byta view motor till nunjucks
- Follow instructions
- npm i nunjucks
- mkdir views
- rm public/index.html
- Open app.js

```jsx
const nunjucks = require('nunjucks');
...
const app = express();

nunjucks.configure('views', {
    autoescape: true,
    express: app
});
...
```

- routes/index.js

```jsx
router.get("/", function (req, res, next) {
  res.render("index.njk", { title: "Express" })
})
```

- touch views/layout.njk

```html
<!DOCTYPE html>
<html lang="sv">

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>{{ title }}</title>
    <link rel="stylesheet" href="/stylesheets/style.css">
</head>

<body>
    {% block content %}
    {% endblock %}
</body>

</html>
```

- touch views/index.njk

```html
{% extends "layout.njk" %}
{% block content %}
<ma>
    <h1>{{ title }}</h1>
</main>
{% endblock %}
```

- npm start
- nodemon för att orka
- npm i -D nodemon
- edit package.json
- "dev": "nodemon -e js,html,njk ./bin/www”
