# HTML Notes

`<head>` contains the **metadata** of a page.

Most HTML elements are **block** elements, and will stack on top of each other. **Inline** elements do not stack, they wrap around other elements.

Strong `<strong>` and emphasis `<em>` are used to add importance and emphasis to text, not in place of `<b>` and `<i>`.

**Attributes** are given to tags like arguments to functions.

`<img/>` written with the slash or without does the same thing, because it's a **self-closing tag**.

`<ul>` is bullet points and `<ol>` is numbered points.

## Forms

The basic structure of a form is the below.

```html
<form action="#" method="POST">
    <label>First name:
        <input type="text" required value="Enter your first name">
    </label>
    <br>
    <label for="lname">Last name:</label>
    <input id="lname" type="text" required placeholder="Enter your last name">
    <br>
    <label for="email">Email:</label>
        <input id="email" type="email" required>
    <button type="submit">Send away!</button>
</form>
```

The form tag wraps the entire form. `Action` is the page that shows up once the form is submitted. `Method="post"` sends the data to the server.

There are different kinds of inputs:

* Text, email and password for writing.
* Checkbox and radio for buttons.
* Color, date and file to interact with.

Labels are inline elements that are placed before each input or form element to attach some text to them. **`<br>` can be used to break the inline elements apart!**

Using `for` and `id` on both, will link the elements together, so clicking on the same will allow to type inside the input box. Alternatively, place the input before closing the label tag.

Buttons submit the data in the form and activate the action on the form tag.

Form attributes can be placed in the forms.

* `Required` will make the input mandatory according to the input type.
* `Value` will prefill the form value.
* `Placeholder` will have a greyed out hint that disappears.

Another option you can place in a form is the `<textarea>`. This will create a larger text area that is resizable, see below to style it

```html
<label for="message">Message</label>
<textarea id="message"></textarea>
```

```css
textarea {
    resize: none;
    height: 100px;
}
```

## Semantic HTML tags

* heading
* nav
* main
* section
* article
* footer
* aside (class sidebar)

`<div>` serve the purpose of grouping content, and have no semantic meaning. They are usually placed inside something like `<section>`.

`<header>` and `<footer>` are good to use with a `<div>` container inside them.

`<main>` and `<aside>` on the other hand should be inside a `<div>` container if they are part of the same block structure.

Note the class names. Long example of a page structure:

```html
<html>
    <head>
        <link href="https://fonts.googleapis.com/css?family=Lora|Ubuntu:400,700&display=swap" rel="stylesheet">
        <link rel="stylesheet" href="css/styles.css">
    </head>
    <body> 
        <header>
            <div class="container container-nav">
                <div class="site-title">
                    <h1>Living the social life</h1>
                    <p class="subtitle">A blog exploring minimalism in life</p>
                </div>
                <nav>
                    <ul>
                        <li><a href="#">Home</a></li>
                        <li><a href="#">About me</a></li>
                        <li><a href="#">Recent posts</a></li>
                    </ul>
                </nav>
            </div> <!-- / .container -->
        </header>
        
        <div class="container">
            <main role="main">
                
                <article class="article-featured">
                    <h2 class="article-title"></h2>
                    <img src="" alt="" class="article-image">
                    <p class="article-info"></p>
                    <p class="article-body"></p>
                    <a href="#" class="article-read-more"></a>
                </article>
                
                <article class="article-recent">
                    <div class="article-recent-main">
                        <h2 class="article-title"></h2>
                        <p class="article-body"></p>
                        <a href="#" class="article-read-more"></a>
                    </div>
                    <div class="article-recent-secondary">
                        <img src="" alt="" class="article-image">
                        <p class="article-info"></p>
                    </div>
                </article>
                
                <article class="article-recent">
                    <div class="article-recent-main">
                        <h2 class="article-title"></h2>
                        <p class="article-body"></p>
                        <a href="#" class="article-read-more"></a>
                    </div>
                    <div class="article-recent-secondary">
                        <img src="" alt="" class="article-image">
                        <p class="article-info"></p>
                    </div>
                </article>
                
                <article class="article-recent">
                    <div class="article-recent-main">
                        <h2 class="article-title"></h2>
                        <p class="article-body"></p>
                        <a href="#" class="article-read-more"></a>
                    </div>
                    <div class="article-recent-secondary">
                        <img src="" alt="" class="article-image">
                        <p class="article-info"></p>
                    </div>
                </article>
            </main>
            
            <aside class="sidebar">
                
                <div class="sidebar-widget">
                    <h2 class="widget-title"></h2>
                    <img src="#" alt="" class="widget-image">
                    <p class="widget-body"></p>
                </div>
                
                <div class="sidebar-widget">
                    <h2 class="widget-title"></h2>
                    <div class="widget-recent-post">
                        <h3 class="widget-recent-post-title"></div>
                        <img src="" alt="" class="widget-image">
                    </div>
                    <div class="widget-recent-post">
                        <h3 class="widget-recent-post-title"></div>
                        <img src="" alt="" class="widget-image">
                    </div>
                    <div class="widget-recent-post">
                        <h3 class="widget-recent-post-title"></div>
                        <img src="" alt="" class="widget-image">
                    </div>
                </div>
                
            </aside>
            
        </div>
        
        
        <footer>
            <p></p>
            <p></p>
        </footer>
        
        
    </body>
</html>
```
