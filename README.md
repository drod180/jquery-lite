# DOMinion

DOMinion is a lightweight DOM manipulation library that provides easy to use methods for working with the DOM with minimal overhead. DOMinion provides methods that allows adding or removing classes from HTML elements as well as methods to add event listeners and even a method for creating XML requests.

Proof of concept: [snake](http://www.drodriguez.io/snake/) | [github](https://github.com/drod180/snake)

###Technical Details:
* DOMinion is a lightweight library that uses instance variable htmlElements which is coerced to behave like an array. htmlElements are kept in an object called DOMNodeCollection which has multiple public API which can be used to manipulate the DOM.
* $d can be used with selectors of either strings, HTMLElement objects or functions to create a new DOMNodeCollection. Functions will be registered and called as soon as the document is ready, or immediately if document is already ready.

ex.

```
root.$d = function (selector) {
	var returnVal;

	switch (typeof(selector)) {
		case "string":
			returnVal = _getSelectorsFromDom(selector);
			break;
		case "object":
			if (selector instanceof HTMLElement) {
				returnVal = new DOMNodeCollection(selectors);
			}
			break;
		case "function":
				_registerCallback(selector);
			break;
	}

	return returnVal;
};

var _registerCallback = function (callback) {
  if(_docReady){
    callback();
  } else {
		_docReadyCallbacks.push(callback);
  }
};
```


###Public API
```
* $d(selector) - Create new DOMNodeCollection or add callback to be called on DOM ready.
	* $d.extend(target[,object]...[,object]) - Merge one ore more objects into target object.
	* $d.ajax([options]) - Asynchronous XMLHttpRequest.
* DOMNodeCollection.prototype
	* addClass(className) - Add class to DOM elements.
	* append(children) - Add children elements to DOM elements.
	* attr(attrName, value) - Set attribute to value for DOM elements.
	* children() - Get children of DOM elements, returns new DOMNodeCollection.
	* each() - Iterate through each DOM element.
	* empty() - Set DOM elements to empty strings.
	* equal(index) - Find DOM element by index in DOMNodeCollection, returns new DOMNodeCollection.
	* filter(selector) - Find DOM elements that match on string selector, returns new DOMNodeCollection.
	* find(selector) - Find DOM elements by selector, returns new DOMNodeCollection.
	* on(eventName, callback) - Add event listener to DOM elements for particular event.
	* off(eventName, callback) - Remove event listener from DOM elements for particular event.
	* parent() - Get parent of DOM elements, returns new DOMNodeCollection.
	* remove() - Remove DOM elements from DOM.
	* removeClass(className) - Remove class to DOM elements
```