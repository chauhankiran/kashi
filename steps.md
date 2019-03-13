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

That's it. This is my `_reboot.css`. `_` in name is just styling purpose you can make it as `_reboot.css` or `reboot.css`. Doesn't make any difference.

I have taken following references while creating this `_reboot.css`.

1. [Firefox Default Style](https://dxr.mozilla.org/mozilla-central/source/layout/style/res/html.css)
2. [Webkit Default Style](https://trac.webkit.org/browser/trunk/Source/WebCore/css/html.css)
3. [Normalize.css](https://necolas.github.io/normalize.css/8.0.0/normalize.css)
4. [Bootstrap's Reboot](https://github.com/twbs/bootstrap/blob/v4-dev/scss/_reboot.scss)
5. [UIKit's Base](https://github.com/uikit/uikit/blob/develop/src/scss/components/base.scss)
