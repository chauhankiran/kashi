# Kashi

I've created a static site generator called bajana in Node.js and to make it look little good and different, I'm planning to create a small specific styles for generator called Kashi.

I do not have plan to do any competition with big player and this framework will be small with few configuration. This will contain only few items including typography, nav, helper, grid and form elements.

Let's start by creating blueprint for this project.

## Blueprint

This micro framework contains following components.

1. reboot : a cross-browser support.
2. configuration : a set of variables.
3. typography : cleaning up some default look.
4. grid : Your responsive friend.
5. tables : Aha! The old friend responsible for layout!
6. List: Your needed listing buddy.
7. Button: Clicked!
8. Form: Tribe of inputs!
9. Nav: Your guide on website.
10. Helper: How can I help you?
11. Example - 1
12. Example - 2
13. Example - 3

I'm going to use `css` for implementation for now.

_Framework or Library?_ Hmmm…. It’s tricky question. But, if ask me, then I will say it’s framework. I know frameworks are evil or not good. But, still it’s framework. Why? Because, when you use Kashi, it will effect your webpage's styles even though, you have not use a single class from it. That is not true for libraries such as jQuery. If you include jQuery in your webpage, it will not effect your webpage until you use one of its method. So, yes Kashi is framework but a micro one!

## Reboot the default behavior

Create a new file inside of `src` folder with name `_reboot.css`.

As name suggest, this file contains code for reboot or reset. I have two options in my plate for reset – Eric Mayer's reset.css and Nicolas Gallagher's Normalize.css.Both have their advantages. But, I really don’t want to go with any of these. Because first, I don't need that level of sophisticated reset and second I have different requirements with reset. Also, I don’t want reset over those field which I am not going to use.

Following are the browsers I am planning to target –

1. Mozilla Firefox
2. Google Chrome
3. Edge
4. Apple Safari

No plan for Opera and IE!

So, let's starts with math. I am not good at math and I don't want to do any calculation. So,

```css
*::before,
*::after {
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
}
```

Although, all browsers has same default margin ( `8px` ). But, I really don't want to go with that amount. So,

```css
body {
    margin: 0;
    padding: 0;
}
```

Yes, I also want total control over padding as well.

Sometimes, that dot decoration around links make me crazy. So,

```css
a:hover,
a:active {
    outline: 0;
}
```

Webkit and Mozilla still haven't agree on `b` and `strong` values. So,

```css
b,
strong {
    font-weight: bold;
}
```

Also, there is a lot inconsistency in `font-family` for code related tags. So,

```css
code,
kbd,
pre,
samp {
    font-family: monospace, monospace;
}
```

Sometimes `pre` spoil the view of page by introducing a long scroll over horizontal space. So,

```css
pre {
    margin-bottom: 0;
    margin-top: 0;
    overflow: auto;
}
```

Also has removed some margin from `pre`!

Form components still not agree with common `font-family` and have different margins across the browsers. So,

```css
button,
input,
select,
textarea {
    font-family: inherit;
    font-size: 100%;
    margin: 0;
}
```

Also, in Edge, textarea introducing default vertical scrollbar, which is not needed. So,

```css
textarea {
    overflow: auto;
    resize: vertical;
}
```

I personally thing, all `img` should be vertically aligned. So,

```css
img {
    vertical-align: middle;
}
```

That's it. This is my `_reboot.css`. `_` in name is just styling purpose you can make it as `_reboot.css` or `reboot.css`. Doesn't make any difference. But, as part of naming convention this means this file is not going to be used as stylesheet with link.

I have taken following references while creating this `_reboot.css`.

1. [Firefox Default Style](https://dxr.mozilla.org/mozilla-central/source/layout/style/res/html.css)
2. [Webkit Default Style](https://trac.webkit.org/browser/trunk/Source/WebCore/css/html.css)
3. [Normalize.css](https://necolas.github.io/normalize.css/8.0.0/normalize.css)
4. [Bootstrap's Reboot](https://github.com/twbs/bootstrap/blob/v4-dev/scss/_reboot.scss)
5. [UIKit's Base](https://github.com/uikit/uikit/blob/develop/src/scss/components/base.scss)

## Configuration

The next file we need for our Kashi is `_config.css` file. This file will contains set of variables and some configurations for Kashi framework. Using this file we can customize the look-n-feel of our framework. We will edit this file in future again if we need to configuration something as part of global configuration.

Let’s start with _colors_. We need one color palette to give a mining of information. But, As I mentioned earlier that I'm not creating a fully feature framework so the colors will be limited to -

* brand color
* background color
* text color
* gray color for displaying less important information
* link color

We also need light/dark color of above color to display some effect such as link hover, focus or button click or something.

You can use any color you would like but I am currently using elementary‘s color palette for following colors. You are free to use any colors you would like –

* brand-color: #3689e6      ( shade of blue )
* background-color: #fff    ( white as background )
* text-color: #333333       ( shade of black )
* gray-color: #abacae       ( shade of gray )
* link-color: #c6262e       ( shade of red! )

Here, I have used these colors. There is no special choice or consideration I have used to use these color to inviting hacking the Kashi.

Also, I'm going to use dark shade of these colors to go with effect. I'm choosing `700` of color given colors so it will become ( except white ),

* brand-color: #3689e6, #0d52bf      ( shade of blue )
* background-color: #fff            ( white as background )
* text-color: #333333, #1a1a1a       ( shade of black )
* gray-color: #abacae, #7e8087       ( shade of gray )
* link-color: #c6262e, #a10705       ( shade of red! )

CSS support the variable declaration. I need these variables throughout the framework. So first I'm going to define,

```css
:root {

}
```

Now inside of `:root` I'm going to define these colors.

```css
:root {
    --brand-color: #3689e6;
    --brand-color-dark: 0d52bf;
    --background-color: #fff;
    --text-color: #333333;
    --text-color-dark: #1a1a1a;
    --secondary-color: #abacae;
    --secondary-color-dark: #7e8087;
    --link-color: #c6262e;
    --link-color-dark: #a10705;
}
```

I've used name `secondary-color` instead of `gray-color` to just make name less dependable on color. These are the colors we are going to use at different places.

Looks like we are done with colors! It is time to define default for fonts.

Let’s first starts with font-family and we can have three types of font-familys, So –

```css
--font-serif: 'Merriweather', serif;
--font-sans-serif: 'Merriweather Sans', sans-serif;
--font-monospace: 'Inconsolata', monospace;
```

( I will use Google’s fonts URL to include this fonts in Kashi. But, that part comes later. )

While working with fonts, let’s define a default font-size as well.

```css
--default-font-size: 1rem;
--default-line-height: 1.5
```

I thought it is good to define a line-height with this single line!

We have default font-size. Now, We can also have large font size and small font size as well. I with go with +/- 0.3rem. So –

```css
--large-default-font-size: 1.3rem;
--small-default-font-size: 0.7rem;
```

Defining few font styles wouldn’t hurt. So, –

```css
--font-italic: italic;
--font-bold: bold;
--font-normal: normal;
--font-thin: thin;
```

Looks like we done with default colors, fonts and text.

Let me complete this config file with default font-size for headers. You are welcome to use any font-size you like.

My calculation is – starts from `h4` with the same size as default font have and then continue increase the size with .5. Last two `h5` and `h6` will be decrease by `.1`.

```css
--default-header-one-font-size: 2.5rem;
--default-header-two-font-size: 2rem;
--default-header-three-font-size: 1.5rem;
--default-header-four-font-size: 1rem;
--default-header-five-font-size: 0.9rem;
--default-header-six-font-size: 0.8rem;
```

That’s it. This was our `_config.scss`. But, remember we will touch this file again future if we thing something need to be hackable!

## Testing

Before I go further and develop another Kashi component, let me pause for a moment and do some arrangement for testing because I yet do not know how all these looks except theoretically. So, I'm going to create a `test` folder and inside of it, I'm going to create a `_module.html` file that will going to be used as development testing.

```bash
$ mdkir test
$ cd test
$ touch _module.html
```

Inside of this, `_module.html` file, I've written following content -

```html
<!doctype html>
<html lang="en" dir="ltr">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Kashi: Modules Testing</title>

        <!-- Development testing... -->
        <link href="../src/kashi.css" rel="stylesheet">
    </head>
    <body>
        <header>
            <h1>Kashi</h1>
            <p>A minimal CSS framework for bajana!</p>
        </header>
    </body>
</html>
```

Here, I've used `kashi.css` file from `src` folder. But, I don't have that file. So, let me first create one -

```bash
$ cd ../src
$ touch kashi.css
```

And inside of this file I'm going to write following code -

```css
@import "_reboot.css";
@import "_config.css";
```

This will include both created file inside of `kashi.css` that ultimately make my style working. Running this `_module.html` in Firefox looks working for me.

Onward now, to test new component, I'll going to create another file and going to include in this `kashi.css` file.