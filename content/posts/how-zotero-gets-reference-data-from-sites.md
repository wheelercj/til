+++
title = 'How Zotero gets reference data from sites'
date = 2024-04-06T00:54:59-07:00
+++

> Clicking [the Zotero] icon saves reference information to the Zotero library. Such functionality is made possible by 'translators' – short pieces of computer code, or scripts[9] to understand the structure of web pages and to parse them into citations using its internal formats
> 
> -- [Wikipedia](https://en.wikipedia.org/wiki/Zotero#mw-content-text:~:text=clicking%20this%20icon%20saves%20reference%20information%20to%20the%20zotero%20library.%20such%20functionality%20is%20made%20possible%20by%20'translators'%20%E2%80%93%20short%20pieces%20of%20computer%20code%2C%20or%20scripts%5B9%5D%20to%20understand%20the%20structure%20of%20web%20pages%20and%20to%20parse%20them%20into%20citations%20using%20its%20internal%20formats)

Zotero's translators are each a JavaScript file in [github.com/zotero/translators](https://github.com/zotero/translators). There are over 700 translators. Each one is for a different site. For example, [here is the translator for Wikipedia](https://github.com/zotero/translators/blob/5af5f73c11baf3bef7789b0e142e047b0e6de7e4/Wikipedia.js).

[dev:translators [Zotero Documentation]](https://www.zotero.org/support/dev/translators)

Zotero often refers to their browser extension as "the Connector".

> The Connector runs a [background process](https://github.com/zotero/zotero-connectors/blob/e1a16c8ad2e17c6893554c3f376384e18182202d/gulpfile.js#L95-L125) ([Chrome](https://developer.chrome.com/extensions/event_pages)/[Firefox](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Anatomy_of_a_WebExtension#Background_scripts)/[Safari](https://developer.apple.com/library/content/documentation/Tools/Conceptual/SafariExtensionGuide/AddingaGlobalHTMLPage/AddingaGlobalHTMLPage.html)) which works as a middle-layer between the translation framework running in inject scripts (a) and Zotero (c) or zotero.org (d).
> 
> The background process maintains a cache of translators and performs the initial [translator detection using URL matching](https://github.com/zotero/zotero-connectors/blob/e1a16c8ad2e17c6893554c3f376384e18182202d/src/common/translators.js#L140-L196). Translators whose target regexp matches the URL of a given webpage are then further tested by running `detectWeb()` in injected scripts. A list of translators and their code is fetched either from [Zotero (c) or zotero.org (d)](https://github.com/zotero/zotero-connectors/blob/e1a16c8ad2e17c6893554c3f376384e18182202d/src/common/repo.js#L140-L155).
> 
> The background process is also responsible for updating the extension UI, kicking off translations, storing and retrieving connector preferences and sending translated items to Zotero or zotero.org. Browser specific scripts are available for [BrowserExt](https://github.com/zotero/zotero-connectors/blob/master/src/browserExt/background.js) and [Safari](https://github.com/zotero/zotero-connectors/blob/master/src/safari/global.html).
> 
> -- [zotero-connectors/README.md](https://github.com/zotero/zotero-connectors/blob/9675587fb3ae91d904c3a3578166b75da3db8e5c/README.md?plain=1#L141)

```js
// Enumeration of types of translators
var TRANSLATOR_TYPES = {"import":1, "export":2, "web":4, "search":8};

// Properties required for every translator
var TRANSLATOR_REQUIRED_PROPERTIES = ["translatorID", "translatorType", "label", "creator", "target", "priority", "lastUpdated"];
// Properties that are preserved if present
var TRANSLATOR_OPTIONAL_PROPERTIES = ["targetAll", "browserSupport", "minVersion", "maxVersion", "inRepository", "configOptions", "displayOptions", "hiddenPrefs", "itemType"];
// Properties that are passed from background to inject page in connector
var TRANSLATOR_PASSING_PROPERTIES = TRANSLATOR_REQUIRED_PROPERTIES
	.concat(["targetAll", "browserSupport", "code", "runMode", "itemType", "inRepository"]);

var TRANSLATOR_CACHING_PROPERTIES = TRANSLATOR_REQUIRED_PROPERTIES
	.concat(["browserSupport", "targetAll"]);
```
-- [translate/src/translator.js](https://github.com/zotero/translate/blob/c9bbad0e68d8bb157101743455565cf43264144f/src/translator.js#L26)

## types

* [CSL properties in zotero/utilities/utilities_item.js](https://github.com/zotero/utilities/blob/cccf1235a318c259345fc623d5e9d6770ba19df7/utilities_item.js#L609)
* [CLS properties in zotero/zotero-schema/schema.json](https://github.com/zotero/zotero-schema/blob/1b12272d44134a652519e9192e5a936ac9fcd707/schema.json#L2734)
* [aurimasv.github.io/z2csl/typeMap.xml](https://aurimasv.github.io/z2csl/typeMap.xml)
* [item types, fields, and creator types in zotero/zotero-schema/schema.json](https://github.com/zotero/zotero-schema/blob/1b12272d44134a652519e9192e5a936ac9fcd707/schema.json)

## further reading

* [github.com/zotero](https://github.com/zotero)
* [dev:client_coding [Zotero Documentation]](https://www.zotero.org/support/dev/client_coding)
* [zotero-connectors/src/browserExt/manifest.json](https://github.com/zotero/zotero-connectors/blob/master/src/browserExt/manifest.json)
* [zotero-connectors/src/browserExt/background.js](https://github.com/zotero/zotero-connectors/blob/master/src/browserExt/background.js#L936)
