+++
title = 'Customizing a Hugo theme'
date = 2024-01-15T15:47:01-08:00
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