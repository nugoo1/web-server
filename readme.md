# Installing Express

`npm install express`

This would serve up your markup as a string. Obviously not the preferred method, but it works. 
You can repeat for each URL.

```

    app.get('/URL', (req, res) => {
        // res.send('<h1>Hello Express!</h1>');
        res.send({
            name: 'Nuwan',
            likes: [
                'Swimming',
                'Sleeping'
            ]
        });
    });

```


The following 4 lines of code is all you need to make a static web server using Express.js!
const express = require('express');

const app = express();

app.use(express.static(__dirname + '/public'));

app.listen(3000);

## Templating Engine

Handlebars View Engine for Express => a view engine for Express (also see ejs or pug).

Render HTML in a dynamic way, injecting values like a username or date. 
Let's you create reusable templates like a header and footer.

### Installing hbs 

`npm install hbs`

in your application: `app.set('view engine', 'hbs');`

### Files

Create a folder called views.

Inside of views, create a file with a .hbs suffix. eg;

`about.hbs`

This is like your standard html page.

In your application, you can inject data inside of your templates, eg. pageTitle and currentYear.

'app.get('/about', (req, res) => {
    res.render('about.hbs', {
        pageTitle: 'About Page',
        currentYear: new Date().getFullYear()
    });
});'

### Partials
Moving footer and header to its own files.

'hbs.registerPartials(__dirname + '/views/partials')'

In your .hbs file, you can import your partials using the following syntax:

{{> footer}}

This lets you reuse your code throught your website.

When running nodemon, make sure it tracks changes in your hbs files.

`nodemon server.js -e js,hbs`

### Handlebars helpers
Way to register functions to run to dynamically create output.
This lets you pass unique data to templates using a single function.

For example, printing the current year in the footer of every page.

'hbs.registerHelper('getCurrentYear', () => {
    return new Date().getFullYear()
});'

change footer.hbs markup to:

    <footer>
        <p>Created By Nuwan Goonewardena - Copyright {{getCurrentYear}}</p>
    </footer>

You can pass arguments to the Handlebard Helpers with a space separating the data.

    <p>{{screamIt welcomeMessage}}</p>

hbs.registerHelper('screamIt', (text) => {
    return text.toUpperCase();
});
