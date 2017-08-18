# gowebgo

A Golang Wiki Page Tutorial Web Application


## Overview

This Application takes a Go leaner through the process of building a web application using package `net/http` and `html/template` from Go standard library.

This is a stepping coding instructor to a [tutorial article][go-article] by golang.org. Each tagged commit is a separate teaching towards a very simple web app.

### Covered in this tutorial:

- Creating a data structure with load and save methods
- Using the `net/http` package to build web applications
- Using the `html/template` package to process HTML templates
- Using the `regexp` package to validate user input
- Using closures


## Prerequisites

### Git

- A good place to learn about setting up git is [here][git-setup].
- You can find documentation and download git [here][git-home].

### Go

- Get [Go][go-install].
- Learn [how to set up Go development][go-workspace].

### Assumed knowledge

- Understanding of basic web technologies (HTTP, HTML)
- Basic UNIX/DOS command-line knowledge


## Commits / Tutorial Outline

You can check out any point of the tutorial using:
```
$ git checkout step-?
```

To see the changes made between any two lessons use the git diff command:
```
$ git diff step-?..step-?
```

### Step-0 _Bootstrapping_

- Create a gowiki.go file.
- Add the `Page struct`.
- Add the `save` and `loadPage` function.
- Write the `main` function to test what we've written.

### Step-1 _Error Handling_

- Modify the `loadPage` to let it return an error if `ReadFile` encounters one.

You can compile and run the program like this:
```
$ go build gowiki.go
$ ./gowiki
This is a sample page.
```

### Step-2 _Serve Pages_

- Use `net/http` package to serve our wiki pages.
- Add the `viewHandler` to handle URLs.
- create some page data like test.txt

Let's compile, run our code and visit [http://localhost:8080/view/test](http://localhost:8080/view/test) to see what we have by far.

### Step-3 _Editing Pages_

- Add the `editHandler`.

Now we have an editing page [http://localhost:8080/edit/test](http://localhost:8080/edit/test).

As you might have noticed, we comment out the registration of `saveHandler` in `main`. We will come back on that later.

### Step-4 _Better HTML_

- Use `html/template` to keep the HTML in a separate file.
- Keep hard-coded HTMLs in separate files.

### Step-5 _Refactor_

In this step, we will not be adding any new functionality to our application. Instead, we are going to take a step back, refactor our codebase and fix a potential issue.

- Move all templating code to its own function.
- Handle non-existent pages in `viewHandler`.

Recompile the code, run and visit [http://localhost:8080/view/APageThatDoesntExist](http://localhost:8080/view/APageThatDoesntExist)

### Step-6 _Saving Pages_

- Implement the `saveHandler` and uncommenting the related line in `main`.

### Step-7 _More Error Handling_

- Handle errors in `renderTemplate`.
- Handle errors in `saveTemplate`.

### Step-8 _Template Caching_

- Refactor to call `ParseFiles` once at program initialization, parsing all templates into a single `*Template`.
- Create the global variable named `templates`, and initialize it with `ParseFiles`.
- Modify the `renderTemplate` function to call the `templates.ExecuteTemplate` method with the name of the appropriate template.

### Step-9 _Validation_

- Use `regexp` package and create the global variable `validPath` to store our validation expression.
- Add the function `getTitle ` that uses the `validPath` expression to validate path and extract the page title.
- Put a call to `getTitle` in each of the handlers.

### Step-10 _Using Function Literals and Closures_

- Re-write the function definition of each of the handlers to accept a title string.
- Define the wrapper function that takes a function of the above type, and returns a function of type `http.HandlerFunc`.
- Wrap the handler functions with `makeHandler` in `main`.
- Remove the calls to `getTitle` from the handler functions, making them much simpler.


## Try it out!

Now we have finished our little wiki page application. Recompile the code, and run the app:
```
$ go build gowiki.go
$ ./gowiki
```

Visiting [http://localhost:8080/view/ANewPage](http://localhost:8080/view/ANewPage) should present you with the page edit form. You should then be able to enter some text, click 'Save', and be redirected to the newly created page.


[go-article]: https://golang.org/doc/articles/wiki/
[git-setup]: https://help.github.com/articles/set-up-git
[git-home]: https://git-scm.com/
[go-install]: https://golang.org/doc/install
[go-workspace]: https://golang.org/doc/code.html
