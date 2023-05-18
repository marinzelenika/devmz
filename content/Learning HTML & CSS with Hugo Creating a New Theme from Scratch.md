---
title: "Learning HTML & CSS with Hugo: Creating a New Theme from Scratch"
description: "Learn or upgrade your skills in HTML and CSS by using them in the fastest framework out there."
categories: "web"
image: "studio-fast.jpg"
datee: "May 18th, 2023"
---
## Introduction
Hugo is an extremely powerful static site generator. It's easy to use, flexible, and it's built with speed in mind. One of its key features is the ability to create unique and custom themes for your website. This article will guide you through the process of learning HTML and CSS using Hugo to create a new theme from scratch.  

## HTML and CSS: The Basics  
Before delving into Hugo, it's crucial to have a basic understanding of HTML (HyperText Markup Language) and CSS (Cascading Style Sheets). HTML is the standard markup language for creating web pages and web applications. CSS, on the other hand, is used for styling the HTML elements. Knowing these two languages will make your journey with Hugo much easier.  

### HTML
HTML is used to structure a web page and its content. An HTML document is made up of various tags, each serving a specific purpose. Some common HTML tags include <h1> for the main headings, <p> for paragraphs, and <img> for images.  

### CSS
CSS is used to control the layout of a webpage. It can alter the colors, fonts, line heights, widths, heights, margins, and many other visual aspects of the page. A basic CSS syntax includes a selector and a declaration block. For instance:  

```css
    p {
        color: green;
        font-size: 16px;
    }
```  

## Getting Started with Hugo
Hugo is a static site generator that takes markdown files (or other content files), applies them to templates, and generates a full HTML website. The first step in using Hugo is installing it, which can be done by following the instructions on the [official Hugo website](https://gohugo.io).  

## Creating a New Hugo Theme
Hugo's power comes from its flexibility and customizability, and one of the best ways to harness this is by creating your own theme. Let's break down the process of creating a Hugo theme.  

### 1. Create a New Theme Directory
The first step in creating a theme is to create a new directory for the theme inside the themes directory in your Hugo project. You can do this using the command:  

```bash
$ hugo new theme mytheme
```

This will create a new directory called mytheme with all the necessary files and directories.  

### 2. Understand the Directory Structure  
Inside your new theme directory, you'll see several different directories. Here's a quick rundown:

* archetypes: Defines the default content for your new posts.
* assets: Holds files that will be processed by Hugo Pipes.
* layouts: Contains HTML templates.
* static: Stores static files like images, CSS, or JavaScript.  

### 3. Create a Base Template
The base template is the most crucial part of your theme. It's the main layout for your pages. You can create a base template by creating a new file called baseof.html inside the layouts directory.

In this file, you can define the basic structure of your pages. A simple base template might look something like this:

```html
        <!DOCTYPE html>
        <html>
        <head>
            <title>{{ .Title }}</title>
            {{ block "styles" . }}{{ end }}
        </head>
        <body>
            {{ block "main" . }}{{ end }}
            {{ block "scripts" . }}{{ end }}
        </body>
        </html>
```

### 4. Define Blocks
In your base template, you've defined several blocks using the {{ block "blockname" . }} syntax. These blocks can be overridden in other templates. For instance, you might create a `home.html file inside the layouts directory to create a custom layout for the homepage.

```html
    {{ define "main" }}
        <h1>Welcome to my website!</h1>
        {{ range .Pages }}
            <h2>{{ .Title }}</h2>
            <p>{{ .Summary }}</p>
        {{ end }}
    {{ end }}
```

This overrides the "main" block from the baseof.html for the homepage, displaying a welcome message and a list of pages.  

### 5. Adding Styles
Now it's time to add styles to your website. Create a new CSS file inside the static directory. Let's call it styles.css.

```css
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 0;
        background-color: #f4f4f4;
    }

    h1 {
        color: #333;
    }
```

To link this stylesheet with your HTML, add a link element inside the "styles" block in your baseof.html:

```html
    {{ block "styles" . }}
        <link rel="stylesheet" href="/styles.css">
    {{ end }}
```

### 6. Understanding Partials
Partials are smaller, reusable pieces of HTML that can be included in your templates. They're useful for elements that appear on multiple pages, like headers and footers.

To create a partial, create a new HTML file inside the layouts/partials directory. Let's create a header.html:

```html
    <header>
        <h1>{{ .Site.Title }}</h1>
        <nav>
            {{ range .Site.Menus.main }}
                <a href="{{ .URL }}">{{ .Name }}</a>
            {{ end }}
        </nav>
    </header>
```

You can include this partial in your baseof.html by using the {{ partial "header.html" . }} function.  

### 7. Finalizing the Theme
Once you've set up all your templates and partials, and styled your site, your theme is ready. To use it, simply specify the theme in your Hugo config file or run Hugo with the --theme flag, like so: hugo server --theme=mytheme.

**Conclusion**
Learning HTML and CSS with Hugo is an engaging way to understand these fundamental web technologies, all while creating your unique website. This step-by-step guide should have equipped you with the knowledge to create a basic Hugo theme. However, remember that this is just the beginning. Hugo offers many more advanced features and functionalities that you can explore as you get more comfortable.