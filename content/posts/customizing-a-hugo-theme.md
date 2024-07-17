+++
title = 'Customizing a Hugo theme'
date = 2024-01-15T15:47:01-08:00
lastmod = 2024-07-16T23:18:58-07:00
+++

The [Etch](https://themes.gohugo.io/themes/etch/) theme is great, but I found a few ways to customize it so that it better meets my needs.

Rather than editing the theme's files directly, it's important to [override them](https://gohugobrasil.netlify.app/themes/customizing/). I copied `<project root>/themes/etch/assets/css/dark.css` to `<project root>/assets/css/dark.css` and edited the new file.

## embedded gists

Etch's dark mode doesn't do anything for embedded gists, making them blindingly bright when [Dark Reader](https://github.com/darkreader/darkreader) is disabled.

![blinding gist embed](/blinding-gist-demo.png)

Eventually I found [Customizing GitHub Gists](https://codersblock.com/blog/customizing-github-gists/). After some experimentation, I was satisfied with this result:

![custom gist CSS demo](/custom-gist-css-demo.png)

Here's the CSS:

```css
body .gist .gist-file,
body .gist .gist-data,
body .gist .highlight {
    background: #2e2e2e;
    border: none;
}

body .gist .blob-num {
    color: #f5f5f5;
    background-color: #3e3e3e;
    pointer-events: none;
}

body .gist .gist-meta {
    display: none;
}

body .gist .blob-code {
    font-size: 14px;
    filter: contrast(5%) brightness(140%) saturate(5000%);
}
```

## background color

Dark Reader was putting a box around each page's content. This change made the box mostly invisible.

```diff
body {
    color: #ebebeb;
-    background: #121212;
+    background: #1e1e1e;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
```

## text color

The bright text on the dark background was a little painful to read, so I made the text a little darker. The left half of the image below is the original color, and the right half is the new color.

![text-color-change.png](/text-color-change.png)

I also made links slightly darker.

Here are the changes:

```diff
body {
-    color: #ebebeb;
+    color: #c4c9ce;
    background: #1e1e1e;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

header#banner a {
-    color: #e0e0e0;
+    color: #c4c9ce;
    text-decoration: none;
}

header#banner nav ul li a {
-    color: #cccccc;
+    color: #c4c9ce;
}

main#content a {
-    color: #00b1ed;
+    color: #20acdb;
}

main#content p {
-    color: #f5f5f5;
+    color: #c4c9ce;
}
```

## code block background color and border radius

The default appearance of multiline code blocks looked good, but inline code blocks had the same background color as the rest of the site; sometimes it was difficult to tell where inline code blocks started and ended. I made the background color of both types of code blocks brighter to fix this.

```css
div.highlight pre,
code {
    background-color: #38383d;
    border-radius: 6px;
}
```

I also added a tiny border radius to images.

```css
img {
    border-radius: 6px;
}
```

## latest edit date

I thought I was going to have to customize the template to show the latest edit dates of pages, but it already supports this with a `lastmod` variable in the frontmatter. If the values of date and lastmod are the same, lastmod is ignored.

```toml
title = 'Customizing a Hugo theme'
date = 2024-01-15T15:47:01-08:00
lastmod = 2024-01-16T15:47:01-08:00
```

## tables

By default, tables in Etch have no borders. That can make tables hard to read, so I added some simple borders that aren't too distracting.

```css
table,
th,
td {
    border: 1px solid #424141;
    width: 100%;
    border-collapse: collapse;
    padding: 0.5rem;
    text-align: left;
}
```

## redirecting

Some of my notes here have improved enough over time that they feel blog-worthy, so I would like to move them to [my blog](https://chriswheeler.dev/). I don't want to break links to pages here though, so I looked into how to redirect to other pages.

Hugo has something called [aliases](https://gohugo.io/methods/page/aliases/) for redirecting, but it only works between pages on the same domain. I want to redirect from a subdomain to a root domain, so I can't use aliases for this.

HTML allows a few ways to redirect to a new page. Here's the way recommended on [Meta refresh - Wikipedia](https://en.wikipedia.org/wiki/Meta_refresh):

```html
<body onload="window.location = 'http://example.com/'">
</body>
```

There's also this way that can apparently make the browser's back button get messed up:

```html
<head>
	<meta http-equiv="refresh" content="0; URL='http://example.com/'" />
</head>
```

Neither of these can be put directly into a post on a Hugo site since the `<head>` and `<body>` elements are outside of the post's scope.

To solve this, I found the file in my theme with the `<body>` tag and changed it to this:

```html
<body {{- with .Params.redirect }} onload="window.location = '{{ . }}'"{{ end }}>
```

Now, I can make a post redirect anywhere by just adding a line like this to the post's front matter:

```toml
redirect = 'http://example.com/'
```

For those with JavaScript disabled, I also added a redirect link a few lines below the `body` tag:

```html
{{- with .Params.redirect -}}<br><a href="{{ . }}">Click here to redirect.</a>{{- end -}}
```
