+++
title = 'Making browser extensions'
date = 2024-05-05T00:03:55-07:00
lastmod = 2024-05-09T12:19:53-07:00
+++

Creating browser extensions is easier than I expected, but still has some challenging parts. A great way to start learning how to make extensions is [the Chrome dev docs](https://developer.chrome.com/docs/extensions).

Creating your first extension requires a lot of trial and error. It gets easier as you learn how extensions work and how to use the browser APIs. On sites like Stack Overflow, many discussions have answers that make assumptions, such as that you're creating a content script and so have access to the `document` variable (which is not accessible in background scripts). The assumptions in some answers are confusing at first, but this problem also gradually fades as you learn more.

## browsers

An extension made for one browser might need few or no changes to also work in other browsers.

Releasing an extension on [the Chrome Web Store](https://chromewebstore.google.com/) makes it available not only to Chrome, but also to other Chromium-based browsers such as Edge, Brave, Vivaldi, and Opera. Firefox and Safari each have their own extension stores.

* [Chrome Web Store](https://chromewebstore.google.com/)
* [Add-ons for Firefox](https://addons.mozilla.org/en-US/firefox/)
* [Safari Extensions Apps](https://apps.apple.com/us/story/id1377753262)

Publishing extensions on the Chrome Web Store requires a small one-time fee. If I remember correctly, it was $5 USD. Creating extensions for Safari appears to require using a Mac and being in [the Apple Developer Program](https://developer.apple.com/programs/), which normally costs $99 USD per year in the United States. The Firefox extension store is completely free to publish to.

Some of the Chromium browsers also have their own extension stores despite allowing installing extensions from the Chrome Web Store, including [Edge](https://microsoftedge.microsoft.com/addons/Microsoft-Edge-Extensions-Home) and [Opera](https://addons.opera.com/en/extensions/).

## web-ext

[web-ext](https://extensionworkshop.com/documentation/develop/getting-started-with-web-ext/) is a command line tool created by Mozilla that helps with making extensions in various ways. For example, using `web-ext run` in an extension's code directory will open Firefox with your extension already loaded, and `web-ext run -t chromium` does the same but with Chrome.

web-ext is also helpful for:

* automatically detecting problems in some of the extension's files with `web-ext lint`
* packaging the extension into a `.zip` file without unnecessary files using `web-ext build`
* signing an extension with `web-ext sign` if you want to self-host it

See [web-ext command reference](https://extensionworkshop.com/documentation/develop/web-ext-command-reference) for more details.

## examples

Besides the example extensions in [the Chrome dev docs](https://developer.chrome.com/docs/extensions), here are a few more:

* [Stardown](https://github.com/wheelercj/Stardown) (which I created)
* [Zotero](/how-zotero-gets-reference-data-from-sites)
* [search for more on GitHub](https://github.com/topics/browser-extension).

Also, reading the reviews of related extensions can be very helpful when deciding what features to create in your extension.

## security

Successful extensions with many users are sometimes sold to data brokers who then change the extension to gather massive amounts of private data. This change is often impossible for the average user to detect since extensions usually update automatically and extension developers sometimes sell not just their extensions, but also their online accounts. Be careful about what extensions you install, and periodically make sure you don't have any installed you don't use anymore.

In [Temptations of an open-source browser extension developer](https://github.com/extesy/hoverzoom/discussions/670), Oleg Anashkin shares dozens of offers he has received (and declined) to monetize his extension, Hover Zoom+.

## other important links

Here are a bunch of links to documentation, guides, etc. that I found helpful.

* Chrome
	* [dev docs](https://developer.chrome.com/docs/extensions)
	* [developer dashboard](https://chrome.google.com/webstore/devconsole)
	* [permissions](https://developer.chrome.com/docs/extensions/reference/permissions-list)
	* [user interface components](https://developer.chrome.com/docs/extensions/develop/ui)
	* [message passing](https://developer.chrome.com/docs/extensions/develop/concepts/messaging)
	* [Give users options](https://developer.chrome.com/docs/extensions/develop/ui/options-page)
	* [chrome.contextMenus](https://developer.chrome.com/docs/extensions/reference/api/contextMenus#type-ContextType)
	* [chrome.i18n](https://developer.chrome.com/docs/extensions/reference/api/i18n)
	* [chrome.tabs](https://developer.chrome.com/docs/extensions/reference/api/tabs)
	* [chrome.tabs.sendMessage()](https://developer.chrome.com/docs/extensions/reference/api/tabs)
	* [chrome.notifications](https://developer.chrome.com/docs/extensions/reference/api/notifications)
* Firefox
	* [dev docs](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions)
	* [developer hub](https://addons.mozilla.org/en-US/developers/addons)
	* [Extension Workshop](https://extensionworkshop.com/)
	* [manifest.json](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json)
	* [Request the right permissions](https://extensionworkshop.com/documentation/develop/request-the-right-permissions/)
	* [Porting a Google Chrome extension](https://extensionworkshop.com/documentation/develop/porting-a-google-chrome-extension/)
	* [Chrome incompatibilities](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Chrome_incompatibilities)
	* [building a cross-browser extension](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Build_a_cross_browser_extension)
	* [Test permission requests](https://extensionworkshop.com/documentation/develop/test-permission-requests/)
	* [Implement a settings page](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Implement_a_settings_page)
	* [menus.ContextType](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/menus/ContextType#page_action)
	* [Internationalization](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Internationalization#internationalizing_manifest.json)
	* [Browser Extension Development Tools](https://extensionworkshop.com/documentation/develop/browser-extension-development-tools/)
