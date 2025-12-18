# Node.js Lesson 25 - Express with Handlebars

A simple user management application built with Express.js and Handlebars template engine.

## Overview

This project demonstrates basic Express.js routing, form handling, and template rendering using Handlebars.

## Key Features

- Add users via form submission
- Display list of users
- Shared layout across pages
- In-memory user storage

## Routes

| Route | Method | Description |
|-------|--------|-------------|
| `/` | GET | Display add user form |
| `/users` | GET | Display users list |
| `/add-user` | POST | Add new user and redirect |

## What I Learned

### 1. Setting up Handlebars with Express

```javascript
const expressHbs = require('express-handlebars');

app.engine('hbs', expressHbs({defaultLayout: 'main-layout', extname: 'hbs'}));
app.set('view engine', 'hbs');
```

### 2. Using body-parser correctly

```javascript
// Correct way
app.use(bodyParser.urlencoded({ extended: false }));

// Wrong: bodyParser({ extended: false })
```

### 3. Handling form data

```javascript
app.post('/add-user', (req, res, next) => {
    users.push({ name: req.body.username });
    res.redirect('/users');
});
```

### 4. Handlebars conditionals and loops

```handlebars
{{#if hasUser}}
    <ul>
        {{#each users}}
            <li>{{ name }}</li>
        {{/each}}
    </ul>
{{else}}
    <h1>No Users Found!!</h1>
{{/if}}
```

## What Was Difficult (Q&A)

**Q: Why does `bodyParser({ extended: false })` not work?**

A: `body-parser` doesn't have a direct function call. You need to specify the parser type:
- Use `bodyParser.urlencoded({ extended: false })` for form data
- Use `bodyParser.json()` for JSON data

**Q: What does `extended: false` mean?**

A: It determines which library to use for parsing:
- `false` = use `querystring` library (simpler)
- `true` = use `qs` library (supports nested objects)

**Q: How do layouts work in Handlebars?**

A: The `{{{ body }}}` placeholder in the layout file is replaced with the content from individual view files. Triple braces prevent HTML escaping.

**Q: Why use redirect after POST?**

A: This follows the Post/Redirect/Get (PRG) pattern to prevent duplicate form submissions when users refresh the page.

## Memo

### Recent Updates

Migrated the project from Handlebars to EJS template engine for simpler syntax and better compatibility. Fixed broken template structure in users.ejs where the forEach loop was incomplete and conditional rendering was malformed. Enhanced the form in index.ejs by adding proper labels, accessibility attributes, and improved structure. Removed express-handlebars dependencies and installed ejs package to resolve module errors.
