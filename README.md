ng-twitter [![NPM version](https://badge.fury.io/js/ng-twitter.png)](http://badge.fury.io/js/ng-twitter) [![Build Status](https://travis-ci.org/darul75/ng-twitter.png?branch=master)](https://travis-ci.org/darul75/ng-twitter)
=====================

Angular directive tweets display.

Idea is to provide a tweet listing for you website.

I have made some tests using angular `http` service to query Twitter API (authentication, query) and it works. But at the end
, I have faced CORS issues, and it was just working on localhost.

So one thing you need to do on your own is the server side.

Demo
-------------

http://darul75.github.io/ng-twitter/

Installation
------------

Using npm:

```
npm install ng-twitter
```

How to use it
-------------

You should already have script required for Angular, note `sanitize` module use.

```html
<script type="text/javascript" src="angular.min.js"></script>
<script type="text/javascript" src="angular-sanitize.min.js"></script>
```

to the list above, you should add:

```html
<link rel="stylesheet" type="text/css" href="ng-twitter.min.css">
```

```html
<script type="text/javascript" src="ng-twitter.min.js"></script>
```

Then, inject `ngTwitter` in your application module:

```javascript
angular.module('myApp', ['ngTwitter']);
```

and then just add an `div` with `tweets` directive name attribute, `hashtag` scope variable attribute.

```html
<div tweets hashtag="hashtag" button="true" count="15" refresh="60"/>
```

'hashtag' is your default hashtag search value.

```javascript
$scope.hashtag = 'football';
```

### Attribute

* `hashtag`: scope hashtag string variable object, default 'football'
* `button`: show refresh button, default true
* `hash`: show hash input field, default true
* `count`: number of tweets to show, default 15
* `refresh`: refresh time in seconds

Example with all above features:

```html
<div ng-app="myApp" ng-controller="ctrl">
	<div tweets hashtag="hashtag" hash="true" button="true" count="5" refresh="10"/>
</div>
```

### Customization

If you look at the code, module provide one angular service, here is the service side call with `$http`. So, for your needs, just play with it.
```javascript
// TWEETER PROXY SERVICE
.service('twitter', ['$http', function (http) {                        
	return {
	        asyncSearch: function(hashtag, since) {
	                var cfg = {        };
	                var paramSince = since ? '&since_id='+ since : '';
	                // should add 'since' but not there because of mock
	                //var queryUrl = '/search?hashtag='+hashtag+paramSince;
	                
	                // YOUR SERVICE CALL : manage auth and search on server side
	                var queryUrl = '/search?hashtag='+hashtag;
	                var promise = http.get(queryUrl, cfg).then(function (response) {
	                        return response;
	                });
	                return promise;
	        }
	};
}])
```

### Build

You can run the tests by running

```
npm install
```
or
```
npm test
```

assuming you already have `grunt` installed, otherwise you also need to do:

```
npm install -g grunt-cli
```

## License

The MIT License (MIT)

Copyright (c) 2013 Julien Valéry

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.




