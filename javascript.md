# JavaScript

## Compare two objects

```javascript
// Simple compare objects in JavaScript. This method works in moste cases
function compareObjs(a, b) {
	var equal = true;
	for(var key in a) {
		if(a.hasOwnProperty(key) && b.hasOwnProperty(key)) {
			if(typeof a[key] === 'function' && typeof b[key] === 'function') {
				continue;
			}
			else if(typeof a[key] === 'object' && typeof b[key] === 'object') {
				if(!compareObjs(a[key], b[key])) {
					equal = false;
					break;
				}
			}
			else if(a[key] !== b[key]) {
				equal = false;
				break;
			}
		}
		else {
			equal = false;
			break;
		}
	}

	return equal;
}

// Usage
var obj1 = { a: 3, b: 'x' };
var obj2 = { a: 3, c: 'y' };
compareObjs(obj1, obj2); // => false

var obj3 = { x: 1, y: 2 };
var obj4 = { x: 1, y: 2 };
compareObjs(obj3, obj4); // => true

var obj5 = { p: { x: 1, y: 1 }, b: 1 }
var obj6 = { p: { x: 1, y: 1 }, b: 1 }

compareObjs(obj5, obj6); // => true
```

## Cookie helper

```javascript
// Inspired by Quirksmode http://www.quirksmode.org/js/cookies.html
var CookieHelper = {
	setCookie: function (name, value, days) {
		days = days || 365;
		var expires = '',
			date = new Date();
	
		date.setTime(date.getTime() + (days * 24 * 60 * 60 * 1000));
		expires = '; expires=' + date.toGMTString();
	
		document.cookie = name + '=' + value + expires + '; path=/';
	},
	
	readCookie: function (name) {
		var nameEQ = name + '=',
			ca = document.cookie.split(';');
		for (var i = 0; i < ca.length; i++) {
			var c = ca[i];
			while (c.charAt(0) == ' ') {
				c = c.substring(1, c.length);
			}
			if (c.indexOf(nameEQ) == 0) {
				return c.substring(nameEQ.length, c.length);
			}
		}
		return null;
	},
	
	deleteCookie: function (name) {
		CookieHelper.setCookie(name,'',-1);
	}
};
```

## Replace all occurrences of a string

```javascript
// Replace all occurrences of monkey
'monkeys monkeys monkeys'.replace(/monkey/g, 'sloth');
// => result: 'sloths sloths sloths'

// Replaces . with ,
'1.5 3.4 6.7'.replace(/\./g, ',');
// => result: '1,5 3,4 6,7'
```

## Split a string on multiple characters

```javascript
// Split a string on multiple characters. This will split on minus, periods and spaces.
'this-is a.string'.split(/[-\.\s]/);
```

## Repeat string

```javascript
Array(5).join('x');
// => result: xxxxx
```

## Generate random numbers functions

```javascript
function random(min, max) {
  return min + Math.random() * (max - min); 
}

function randomInt(min, max) {
  return Math.floor(min + Math.random() * (max - min + 1));
}

function randomRange(count, min, max) {
  var range = [];
  for(var i  = count; i > 0; i--) {
  	range.push(random(min, max));
	}
  return range;
}

function randomIntRange(count, min, max) {
  var range = [];
  for(var i  = count; i > 0; i--) {
  	range.push(randomInt(min, max));
	}
  return range;
}

// usage: 
// random(50, 100); // => 50.0 - 100.0
// randomInt(50, 100); // => 50 - 100
// randomRange(10, 50, 100); // => Array with 10 decimal values
// randomIntRange(10, 50, 100); // => Array with 10 int values
```

## Array helper methods

```javascript
Array.prototype.skip = function(count) {
	var val,
		length = this.length;

	if(length > count) {
		val = this.slice(count);
	} else {
		val = [];
	}

	return val;
};

Array.prototype.take = function(count) {
	var val,
	length = this.length;

	if(count > length) {
		count = length;
	}

	return this.slice(0, count);
};

Array.prototype.first = function() {
	var val;

	return this.length ? this[0] : this;
};

Array.prototype.last = function(count) {
	var val,
	length = this.length;

	return length ? this[length - 1] : this;
};

Array.prototype.equals = function (array) {
    // if the other array is a falsy value, return
    if (!array)
        return false;

    // compare lengths - can save a lot of time 
    if (this.length != array.length)
        return false;

    for (var i = 0, l=this.length; i < l; i++) {
        // Check if we have nested arrays
        if (this[i] instanceof Array && array[i] instanceof Array) {
            // recurse into the nested arrays
            if (!this[i].equals(array[i]))
                return false;       
        }           
        else if (this[i] != array[i]) { 
            // Warning - two different object instances will never be equal: {x:20} != {x:20}
            return false;   
        }           
    }       
    return true;
}

var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];

console.log(arr.first());

console.log(arr.last());

console.log(arr.take(3));

console.log(arr.skip(3));

console.log(arr.equals([1, 2, 3])); // => false
console.log(arr.equals(arr)); // => true
```

## Useful regular expressions

```javascript
// Test a swedish zip code
document.write( /\d{5}|\d{3}\s\d{2}/.test('12345') );
document.write( /\d{5}|\d{3}\s\d{2}/.test('123 45') );
 
// Test email simple
document.write( /^\S+@\S+\.\S+$/.test('zaphod@hotmail.com') );
 
// Test numbers and spaces (phone number)
document.write( /^[0-9\s]+$/.test('070 123 456') );
 
// Replace urls with hyperlinks
var exp = /(\b(?:(?:https?|ftp|file):\/\/|www\.|ftp\.)[-A-Z0-9+&@#/%=~_|$?!:,.]*[A-Z0-9+&@#/%=~_|$])/ig;
var text = 'A url http://www.github.com in a text';
text = text.replace(exp, '<a href="$1" target="_blank">$1</a>');
 
// Remove HTML tags
var regex = /(<([^>]+)>)/ig;
var html = '<p>Test</p>';
document.write(html.replace(regex, ''));

// Validate hex color
/^#?([a-f0-9]{6}|[a-f0-9]{3})$/.test('#ccc');
```

## Capitalize first letter in sentance

```javascript
var t='text to capitalize. another sentance.';
t[0].toUpperCase() + t.slice(1).replace(/([.!?]\s*\w)/gi, function(c){ return c.toUpperCase() });
```

## Add remove class from DOM element

```javascript
function addClassToElement(element, className) {
	var classes = element.className.split(' ');
	if(classes.indexOf(className) === -1) {
		classes.push(className);
		element.className = classes.join(' ');
	}
}

function removeClassFromElement(element, className) {
	var classes = element.className.split(' '),
		classNameIndex = classes.indexOf(className);
	
	if(classNameIndex != -1) {
		classes.splice(classNameIndex, 1);
		element.className = classes.join(' ');
	}
}
```

## Create GUID

```javascript
/**
 * Generates a GUID string, according to RFC4122 standards.
 * @returns {String} The generated GUID.
 * @example af8a8416-6e18-a307-bd9c-f2c947bbb3aa
 * @author Slavik Meltser (slavik@meltser.info).
 * @link http://slavik.meltser.info/?p=142
 */
function guid() {
    function _p8(s) {
        var p = (Math.random().toString(16)+"000000000").substr(2,8);
        return s ? "-" + p.substr(0,4) + "-" + p.substr(4,4) : p ;
    }
    return _p8() + _p8(true) + _p8(true) + _p8();
}
```

## Object Store

```javascript
var ObjectStore = {
	values: {},
	length: 0,
	add: function(value) {
		var guid = this.createGuid();
		
		this.values[guid] = value;
		
		this.length++;
		
		return guid;
	},
	remove: function(guid) {
		delete this.values[guid];
		this.length--;
	},
	createGuid: function() {
		function _p8(s) {
			var p = (Math.random().toString(16)+'000000000').substr(2,8);
			return s ? '-' + p.substr(0,4) + '-' + p.substr(4,4) : p ;
		}
		return _p8() + _p8(true) + _p8(true) + _p8();
	}
};
```

## Get number of days in a month
```javascript
var year = 2014,
	month = 1; // jan, start at 1 not 0
new Date(year, month, 0).getDate();
// => 31
```

## Day name helper
```javascript
var weekDay = function() {
  var names = ['Sunday', 'Monday', 'Tuesday', 'Wednesday',
               'Thursday', 'Friday', 'Saturday'];
  return {
    name: function(number) { return names[number]; },
    number: function(name) { return names.indexOf(name); }
  };
}();
```

## Month name helper
```javascript
var month = function(){
  var names = [ 'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
  return {
    name: function(index) {
      return names[index];
    },
    number: function(name) {
      return names.indexOf(name);
    }
  }
}();
```

## Sort array of dates
```javascript
var arr = [ 
	{ date: new Date(2014, 5, 5, 10, 00) },
	{ date: new Date(2014, 5, 5, 5, 00) },
	{ date: new Date(2013, 3, 3, 10, 00) },
	{ date: new Date(2014, 5, 5, 15, 00) },
	{ date: new Date(2014, 10, 10, 10, 00) } 
];

arr.sort(function(a, b) {
	return a.date - b.date;
});
```

## Sort array of strings (with numbers in name)
```javascript
// http://stackoverflow.com/questions/15478954/sort-array-elements-string-with-numbers-natural-sort
function strcmp(a, b) {
    return a > b ? 1 : a < b ? -1 : 0;
}

function natcmp(a, b) {
    var x = [], y = [];

    a.replace(/(\d+)|(\D+)/g, function($0, $1, $2) { x.push([$1 || 0, $2]) })
    b.replace(/(\d+)|(\D+)/g, function($0, $1, $2) { y.push([$1 || 0, $2]) })

    while(x.length && y.length) {
        var xx = x.shift();
        var yy = y.shift();
        var nn = (xx[0] - yy[0]) || strcmp(xx[1], yy[1]);
        if(nn) return nn;
    }

    if(x.length) return -1;
    if(y.length) return +1;

    return 0;
}

ary = ["IL0 Foo", "PI0 Bar", "IL10 Baz", "IL3 Bob says hello"]
ary.sort(natcmp)
```

## Get the first N values from an array
```
var arr = [1, 2, 3, 4, 5];
arr.slice(0,2)
// => [1, 2]
```

## Get the last N values from an array
```
var arr = [1, 2, 3, 4, 5];
arr.slice(arr.length - 2)
// => [4, 5]
```

## Get every even value from an array
```
var arr = [1, 2, 3, 4, 5];
arr.filter(function(value, index) {
    return index % 2 === 0;
});
// => [ 1, 3, 5 ];
```

## Get every odd value from an array
```
var arr = [1, 2, 3, 4, 5];
arr.filter(function(value, index) {
    return (index + 1) % 2 === 0;
});
// => [ 2, 4 ];
```

## Parse and build querystring
```javascript
var QueryString = {
    parse: function (url) {
        var qo = {};

        if (url.indexOf('?') >= 0) {
            url.replace(
                new RegExp("([^?=&]+)(=([^&]*))?", "g"),
                function ($0, $1, $2, $3) {
                    if ($3) { qo[$1] = $3; }
                }
            );
        }

        return qo;

    },
    build: function (query, startSeparator) {
        var queryString = '',
        	separator = typeof startSeparator === 'undefined' ? '?' : startSeparator;

        for (var key in query) {
            var value = query[key];

            if (value) {
                queryString += separator + key + '=' + value;

                if(separator !== '&') {
                    separator = '&';
                }
            }
        }

        return queryString;
    }
};

QueryString.parse('http://www.domain.com?a=1&b=2&c=3'); // => {a: '1', b: '2', c: '3'}
QueryString.build({a: '1', b: '2', c: '3'}) // => '?a=1&b=2&c=3'
QueryString.build({a: '1', b: '2', c: '3', '&'}) // => '&a=1&b=2&c=3'
QueryString.build({a: '1', b: '2', c: '3', ''}) // => 'a=1&b=2&c=3'
```

## Simple string templating
```javascript
function simpleTemplate(template, data) {
	var output = template,
		l = '{{',
		r = '}}',
		find,
		regexp;

	for(var key in data) {
		if(data.hasOwnProperty(key)) {
			find = l + key + r;
			regexp = new RegExp(find, 'g');
			output = output.replace(regexp, data[key]);
		}
	}

	return output;
}
	
var template = '<b>Number of {{animal}} are {{count}}</b>';
simpleTemplate(template, { animal: 'cats', count: 3 }); // => "<b>Number of cats are 3</b>"
simpleTemplate(template, { animal: 'dogs', count: 5 }); // => "<b>Number of dogs are 5</b>"
```

## Math, Trigonometry, circles, etc
```javascript
// Convert degrees to radians
function degreesToRadians(degrees) {
    return (degrees * Math.PI) / 180;
}

// Convert radians to degrees
function radiansToDegrees(radians) {
    return (radians * 180) / Math.PI;
}

// Get scale based on width or height
function getScale(width, height, maxWidth, maxHeight) {
	return Math.min(maxWidth / width, maxHeight / height);
}
```
## Copy to clipboard
```javascript
function copyToClipboard(text) {
  var textarea = document.createElement('textarea'),
      successful = false;
  
  textarea.value = text;
  textarea.style.position = 'absolute';
  textarea.style.opacity = 0;
  document.body.appendChild(textarea);
  textarea.select();

  try {
    successful = document.execCommand('copy');
    var msg = successful ? 'successful' : 'unsuccessful';
  } catch (err) {
    successful = false;
  }
  
  document.body.removeChild(textarea);
  
  return successful;
}
```

## Format number
```javascript
function formatNumber(num, n, x, s, c) {
	if(typeof num !== "number") {
		num = Number(num);
	}

    var re = '\\d(?=(\\d{' + (x || 3) + '})+' + (n > 0 ? '\\D' : '$') + ')',
	    num = num.toFixed(Math.max(0, ~~n));

	return (c ? num.replace('.', c) : num).replace(new RegExp(re, 'g'), '$&' + (s || ','));
}

formatNumber(12345.56789, 2, 3, ',', '.')
```

## Round decimals
```javascript
function roundDecimals(value, places) {
    var multiplier = Math.pow(10, places);
    return (Math.round(value * multiplier) / multiplier);
}
// roundDecimals(100, 2) => 100
// roundDecimals(100.1234, 2) => 100.12
```

## WaitForIt
```javascript
function waitForIt(fn, condition, interval, maxCalls, context) {
  
  interval = interval || 1000;
  context = context || this;
  maxCalls = maxCalls || Infinity;
  
  var calls = 0;
  
  function testCondition(){
    if(calls < maxCalls && condition()) {
      fn.call(context)
    }
    else if(calls < maxCalls) {
      setTimeout(testCondition, interval);
    }
    calls++;
  }
  
  testCondition();
  
};
```
