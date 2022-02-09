# SASS Architecture

There are four folders that hold the .scss files for this project:
1. utilities
2. base
3. components
4. pages

Each folder serves a purpose, which helps organize the project. 

<!-- > It is important to know that all files are imported into the main.scss file at the root of the scss folder.   -->

## Utilities Folder

The utilities folder includes files that are used throughout the project. In this project, there are three files in the utilities folder.

- _functions.scss
- _mixins.scss
- _variables.scss

**Variables** are convient ways to store information that you want to reuse later. With Sass, they are declared with a dollar sign symbol `$` followed by the variable name. To define it, use a colon `:` and set the variable equal to a value.

```css
$main-font-color: #fff;
```

Then, you can use this value in your Sass with the variable name rather than its value. 

```css
body {
    color: $main-font-color;
}
```
These variables can be used throughout your project, so it rightly  belongs in the Utilities folder. The variables file needs to be imported with `@use` in order for this to work, however. This applies to all files in the Utilities folder.

***

**Functions** allow you to write an operation once, and reuse it as many times as you like. It has a name, it can have arguments, and it will return a value. 

This is what it looks like.

```css
@function mult($num1, $num2) {
    $result: $num1 * $num2;
    @return $result;
}
```
We declare a function with an at-sign `@` and the word `function`, followed by the function name. In this case, the function is called `mult`. Then, it accepts two arguments, `$num1` and `$num2`, representing two numbers. Within the function block, we create a variable called `result` and multiply the two arguments together. Finally, we return the result with an at-sign `@` and `return`, followed by the return value. 

This is a very simple function that might not even be used since it is shorter to write num1 * num2 within the style block. Anyway, this is how to call the function anywhere in your stylesheet.

```css
.card {
    padding: 2rem;
    margin-left: mult(3, 8) * 1px;
}
```
Functions allow you to abstract some logic so that your Sass can be more readable and easy to understand. It is clear what the function is doing due to its name, and we don't even have to go back and look at the function itself to know what it does. Functions can be separated into one file and placed in the Utilities folder since these will be used anywhere in your Sass. 

***

**Mixins**, like functions and variables, are a way to abstract some css and represent it in a shorter, readable way. This makes it very easy to be reused throughout your stylesheet. 

A mixin represents a block of css declarations. It has a name and can take arguments.

Here is what a mixin declaration looks like.

```css
@mixin center-div($width: 50%) {
    display: block;
    width: $width;
    margin: auto;
}
```
As shown above, a mixin is declared with an at-sign `@` and the word `mixin`, followed by its name. In this case, it is called `center-div` which describes what it is doing very well. This mixin also has a parameter called `$width` representing a width measurement. If this mixin is called without an argument, then it will use a default `$width` of 50%. In the block of declarations, the width property is set to the value of the `$width` parameter. 

Mixins are incredibly convenient when you want the same css applied to multiple elements. This is how it looks to use a mixin.

```css
.card {
    @include center-div;
}
```

It results in a single declaration rather than a block of code. All it needs is the at-sign `@` with `include`, followed by the name of the mixin. 

## Base Folder

The Base folder includes files that are supposed to load before any other styles in your stylesheet. This includes any style resets (to deal with browser differences) and typography that you want to include in your project. 

**Resets** include any styles that you want to apply before anything else. Maybe you want to adjust the box-sizing, set the margin/padding for the body element, or you want to apply an exisiting CSS reset stylesheet like [normalize.css](https://necolas.github.io/normalize.css/), or [reset.css](https://meyerweb.com/eric/tools/css/reset/) by Eric Meyers. 

**Typography** includes any imported fonts you want to include on your website. Here will be any @font-face declarations or @import declarations based on where your fonts come from. In this file can also be variables set that relate to font use in your project. This feels organizationally correct. 

## Components Folder
The Components folder has seperate files for css styles applied to certain elements. It is your discretion as to what elements you want to have their own stylesheet. Some example components are buttons, headers, footers, and cards. 

## Pages Folder
The Pages folder includes stylesheets for each page on the site. Some examples are home, about, and contact pages. Component files from the Components folder will be imported into these files at the top of each using `@use`. 

***

This file structure nicely organizes our Sass and makes logical sense. The cascade won't be an issue because this architecture makes it so every file has an understandable relationship to other files. 

In addition to these folders, there is usually a `main.scss` file that includes imports from the Page files and Base files. This makes sense because the developer wants to apply the base styles first and then the rest, which was funnelled down into only the Page files. 

In the end, everything is abstracted into that one main.scss file, which is what the compiler reads when creating a single css stylesheet for the whole project. 