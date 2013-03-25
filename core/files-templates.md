---

layout: ots
title: Files & Templates

---

## Files

So you've seen how to send out some basic text with a simple flask application, and the languages that are used to build the web: HTML, CSS and Javascript. Serving text isn't enough though - what if we want to serve some actual files?

Luckily, Flask comes prepared. All you have to do is create a folder in the same directory as `hello.py` with the special name of `static`. Any file you put in that folder will be served by flask automatically!

You can do this with your computer's file browser, or on the command line by typing `mkdir static`.

So, if you made a file in the `static` folder called `cats.gif`, and you'd normally access your application by visiting the url [`http://127.0.0.1:5000`](http://127.0.0.1:5000), then you can view that file by going to [`http://127.0.0.1:5000/static/cats.gif`](http://127.0.0.1:5000/static/cats.gif).

Check this works by downloading a funny image from the internet (there are plenty at [imgur](http://imgur.com)), putting it in the `static` folder, running your flask application (`python hello.py`), and browsing to your image by the right url.

The `static` folder is a great place to put CSS stylesheets, Javascript script files, and images. Those files don't usually change much when a website is running, hence the folder name. A common practice is that web developers will organise these files in sub-directories called, for instance, `css`, `js`, and `img` respectively. 

## HTML Templates

None of that explains where to put the *content* of our application - the HTML. Flask makes use of HTML templating - this allows it to put dynamic application data (like a list of email addresses that changes over time) into HTML easily, so that any web browser can view it easily, and it looks good as well.

Flask uses another special directory to store templates, called `templates` (crazy, huh?), so go ahead and create it, like you did for `static`.

In it, create a file called `index.html` and chuck some in some HTML -

    <!DOCTYPE html>
    <html>
    <head>
        <title>{{ author }}' app</title>
    </head>
    <body>
        <p>Hello {{ name }}!</p>
    </body>
    </html>


This is a pretty simple HTML page, but it includes two simple bits of Flask's templating language. When Flask shows this template to your browser, it will replace `{{ author }}` and `{{ name }}` with what you assign those two variables in your application.

In this way a template separates what the content of the page should be, from the actual actual `data` that will be used as that content. This makes things a lot easier if you have to write a lot of dynamic web pages!

Let's modify our flask app to serve this template:

    from flask import Flask, render_template
    app = Flask(__name__)

    @app.route("/")
    def hello():
        author = "Me"
        name = "You"
        return render_template('index.html', author=author, name=name)

    if __name__ == "__main__":
        app.run()

You can see we imported a function from `flask`, called `render_template`.

Then in `hello()`, we added two variables called `author` and `name`. Please change their values from `"Me"` and `"You"` in your file, those are boring!

Then instead of returning some text, we returned the result of calling `render_template`. First, we give it the file name of the template we wish to return. Then, we give it a list of variable names that the template should know about (`author` and `name`) and what their values should be (...coincidentally, `author` and `name`!).

Now try running and viewing your app, in all its HTML glory.