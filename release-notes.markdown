Release Notes
-------------

* 2.1.0 2015-08-27:
    * Ability to convert response bodies to JavaScript objects at the end of the traversal is now also available for `post()/put()/patch()/delete()` via configuration method `convertResponseToObject()`, not only for `get()`. ([#44](https://github.com/basti1302/traverson/issues/44), thanks to @jinder for the suggestion).
    * Improved error message when a JSONPath expression denotes a property that does not have type string; for example, if the property has type object. ([#43](https://github.com/basti1302/traverson/issues/43), thanks to @Baiteman for reporting).
* 2.0.1 2015-05-04:
    * Fixes a [bug](https://github.com/basti1302/traverson-angular/issues/11) when cloning a continued traversal (via `continue`) with `newRequest`.
* 2.0.0 2015-04-07:
    * Continue link traversals with `continue` (see [API docs](https://github.com/basti1302/traverson/blob/master/api.markdown#traversal-continue), also see GitHub issues [#7](https://github.com/basti1302/traverson/issues/7), [#24](https://github.com/basti1302/traverson/issues/24), [#40](https://github.com/basti1302/traverson/issues/40) and [traverson-hal/#4](https://github.com/basti1302/traverson-hal/issues/4)).
    * Fix for wrong resolution of URLs for HAL and root URLs with path ([#38](https://github.com/basti1302/traverson/issues/38), thanks to @xogeny)
    * Breaking changes (_probably_ irrelevant for most users):
        * The methods callback passed to `post`, `put`, `patch` and `delete` no longer receive the URL that had been visited last as their third parameter. The callback signature is now `callback(err, response, traversal)` for these methods.
* 1.2.1 2015-03-15:
    * Include browser build in npm release (for users using npm for client side packages but not using Browserify but script tags or RequireJS).
* 1.2.0 2015-03-15:
    * Huge refactoring of Traverson's internals. To the best of my knowledge, this did not break anything (the test coverage on Traverson is pretty good). You probably should take this version for a test ride before pushing it to production, though.
    * The method `getUri` has been renamed to `getUrl`. `getUri` is now deprecated, but is kept as an alias for `getUrl`.
    * The API for media type plug-ins has changed. The property `uri` in the step object that media type plug-ins return has been renamed to `url`. Media type plug-ins that return a step object with an `uri` attribute still work, but this attribute is considered to be deprecated. Support for it will be removed in version 2.0.0.
    * An undocumented behaviour has been removed: In case of an error, the callback has sometimes been called with more than one argument (the error), namely with the last response and the last URL that had been accessed before the error occured. If you relied on this behaviour, then this is a breaking change for you.
    * Added `preferEmbeddedResources()`.
* 1.1.0 2015-03-02:
    * Abort link traversals (and HTTP requests) ([#27](https://github.com/basti1302/traverson/issues/27)). This feature is to be considered experimental in this version.
    * Specify request options per step by passing in an array to `withRequestOptions` or `addRequestOptions` ([#25](https://github.com/basti1302/traverson/issues/25)).
    * Fix for subsequent error that ate the original error if a problem occured before or during the first HTTP request ([#23](https://github.com/basti1302/traverson/issues/23)).
    * Fix: Copy contentNegotiation flag correctly to cloned request builder (`newRequest()`).
    * Add methods to request builder to query the current configuration.
    * Posting with content type application/x-www-form-urlencoded works now ([#31](https://github.com/basti1302/traverson/issues/31)).
* 1.0.0 2015-02-27:
    * Media Type Plug-ins. You can now register your own media types and plug-ins to process them.
    * HAL is no longer supported by Traverson out of the box. If you want to use HAL, you now have to use the [traverson-hal](https://github.com/basti1302/traverson-hal) plug-in.
    * Traverson uses content type detection by default now. You can still force media types by calling `setMediaType` or shortcuts like `json()`/`jsonHal()` on the request builder.
    * New method `setMediaType` to force arbitrary media types (as long as a matching media type plug-in is registered).
    * New methods `json()`/`jsonHal()` as shortcuts for `setMediaType('application/json')`/`setMediaType('application/hal+json')`.
    * The properties `traverson.json` and `traverson.jsonHal` (that is, using *properties* `json`/`jsonHal` on the `traverson` object) are deprecated as of 1.0.0 (but they still work). Instead, use the methods `json()`/`jsonHal()` on the request builder object. Thus, `traverson.json.from(url)` becomes `traverson.from(url).json()` and `traverson.jsonHal.from(url)` becomes `traverson.from(url).jsonHal()`. You can also omit `json()`/`jsonHal()` completely and use content negotiation.
    * Entry points (methods on the traverson object) have been restructured (see api.markdown for details).
    * Cloning a request builder (to share configuration between link traversals) is now more explicit (method `newRequest()` on a request builder instance).
    * `del()` has been renamed to `delete()`. `del()` is kept as an alias for backward compatibility.
    * New method `addRequestOptions` to add request options (HTTP headers etc.) without resetting the ones that have been set already ([#33](https://github.com/basti1302/traverson/issues/33)) (thanks to @xogeny)
    * Lots of documenation updates. Also new [API reference documentation](https://github.com/basti1302/traverson/blob/master/api.markdown).
* 0.15.0 2014-12-06:
    * Content type detection ([#6](https://github.com/basti1302/traverson/issues/6))
* 0.14.0 2014-12-05:
    * `'link[$all]'` to retrieve the complete array of `_embedded` HAL resources instead of an individual resource ([#14](https://github.com/basti1302/traverson/issues/14))
    * Add ability to use a custom JSON parsing method ([#13](https://github.com/basti1302/traverson/issues/13))
* 0.13.0 2014-12-01:
    * Reduce size of browser build by 33%. The minified version now has 37k instead of 55k (still too much, but also much better than before)
* 0.12.0 2014-11-29:
    * Deal with cases where body comes as arg but not in response ([#19](https://github.com/basti1302/traverson/issues/19)) (thanks to @subvertnormality/@bbc-contentdiscovery)
* 0.11.0 2014-11-14:
    * Add ability to set a custom request library ([#18](https://github.com/basti1302/traverson/issues/18)) (thanks to @subvertnormality/@bbc-contentdiscovery)
* 0.10.0 2014-10-01:
    * Add query string handling for client side ([#16](https://github.com/basti1302/traverson/issues/16)) (thanks to @craigspaeth)
* 0.9.0 2014-06-27:
    *  Add HAL curie resolution ([#12](https://github.com/basti1302/traverson/issues/12))
* 0.8.3 2014-06-19:
    * Fix bower release ([#11](https://github.com/basti1302/traverson/issues/11))
* 0.8.2 2014-06-12:
    * Fix corrupted browser build ([#10](https://github.com/basti1302/traverson/issues/10))
    * Can now be installed via bower (thanks to @chadly)
* 0.8.0 2014-04-30:
    * Support absolute URLs, absolute URL paths and relative URLs ([#3](https://github.com/basti1302/traverson/issues/3))
    * Fix: Also resolve URI templates when no template params are given (makes sense for templates with optional components)
    * Fix: Now works for cases where the entry point has a pathname other than `/`. (thanks to @eins78)
* 0.7.0 2013-12-05:
    * Select HAL links by secondary key
* 0.6.0 2013-11-25:
    * Further reduce browserified size
* 0.5.0 2013-11-23:
    * Make individual elements of HAL link arrays and embedded arrays available by using array indexing notation
* 0.4.0 2013-11-21:
    * Use Halfred instead of Halbert to parse HAL to reduce size of browser build.
* 0.3.0 2013-11-17:
    * Browser build in addition to Node.js module (by browserify)
* 0.2.1 2013-10-25:
    * Documentation fixes
* 0.2.0 2013-10-25:
    * Support for hypertext application language (HAL)
    * Add `getUri`
    * Add `withRequestOptions`
* 0.1.0 2013-10-11:
    * New fluent API
    * Add `get`, `post`, `put`, `patch` and `delete`
* 0.0.1 2013-10-02: Initial release