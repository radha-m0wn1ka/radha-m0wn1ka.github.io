### 14-10-23
### escape html
```
->look and understand source code
this is part of script
'''
function escapeHTML(input){
		return input.replace(/</g,'&lt;').replace(/>/g,'&gt;')
	}
'''
input which is being sent to this fucntion will be santized by replacing < ,> with lt,gt
```
#### url search params
```
https://developer.chrome.com/blog/urlsearchparams/
the code
'''
var params = new URLSearchParams(window.location.search);
	var name = params.get('name');
'''
now
// URL: https://example.com?version=1.0
const params = new URLSearchParams(location.search);
params.set('version', 2.0);
so we can see the website is taking the serach parameter name and storing it in name variable
so our payload must follow the inclusion of ?name=xxx
the url searach parameter api:::::
The URLSearchParams API provides a consistent interface to the bits and pieces of the URL and allows
 trivial manipulation of the query string (that stuff after ?)
another example
'''
// Can also constructor from another URLSearchParams
const params = new URLSearchParams('q=search+string&version=1&person=Eric');

params.get('q') === "search string"
params.get('version') === "1"
Array.from(params).length === 3
'''
```
### json parse
```
JSON.parse() parses a string, written in JSON format, and returns a JavaScript object
var obj = JSON.parse('{"firstName":"John", "lastName":"Doe"}');
document.getElementById("demo").innerHTML = obj.firstName;

http://example.com?name={"age":30,"city":"New York"}

```
### jquery extends
```
'''
	var paramsJson = $.extend(true, HoF, JSON.parse(name));
'''
The jQuery.extend() method is used to merge contents of two or more objects together. The object is merged into the first object.
https://www.tutorialspoint.com/Where-do-we-use-extend-method-in-jQuery
https://api.jquery.com/jquery.extend/
by this line of code all properties are recursivly merged into hof

```
### $.each in jquery
```
'''
$.each(paramsJson,function(key,value){
		$(`<li id='name'>${escapeHTML(value)}</li>`).appendTo('#HoF')
	});
'''
each key value pair in parms json will be written in list format with id as name and list element as the value
so we can see the key does not have any effect only the value
```
### how to add our name into the hof
```
url/?name={"key_random":"m0wn1ka"}
we can see it does work
https://msrkp.github.io/?name={"key_random":"m0wn1ka"}
will show our name appended to the hof
```
### later 
```
now we can see how to write to the page
so let us see how can we get xss
1:try to use xss cheetsheets
2:may be somekind of pollution works ,as the jquery library some version are prone to it ((https://api.jquery.com/jquery.extend/))
3:we can see there are exploits in <script src="https://code.jquery.com/jquery-1.12.4.js"></script>(as per google search)

```

### going with xss cheetsheets
```

```
### html 
```
we can observe that it uses replace function
</li><img src=x onerror=alert(1337)><li> this is my payload
as , and > are not allowed lets us html encode
this is my another test page
'''
<html>
<body>
test
<ol>
<li>first elem</li>
<li>

("</li><img src=x onerror=alert(1337)><li>").replace(/</g,'&lt;').replace(/>/g,'&gt;')

</li>
</ol>
</body>
</html>
'''
it pops xss
hence may be '</li><img src=x onerror=alert(1337)><li>' will give alert
not working ,may be it is not just replacing
let us create same env as of the website in local as well like same kind of fucntions
so we can find which part is preventing us
```
### try debugging the site by debugger in developer console
```
by placing brakpoints we can see for query /?name={"key_random":"m0wn1ka"}
key is key_random  and value is m0wn1ka
now let us see how key ,value pair changes when used with < and >
by this /?name={"key_random":"m0wn1ka>"}
in output we can see mown1ka> but > is not treated as symbol
let us go with pollution
as of jquery library in script
<script src="https://code.jquery.com/jquery-1.12.4.js"></scrip
```
## wired behaviour
```
1::::when this is the query
'''
?name="hi"
'''
the first 2 members in hof are replaced by h,i
2::::local working
in original site if we try /?name={"mouni":"radha"} it appends the name
but if i copy same on local and try it says cant access
t>

```
### jquery library
```
<script src="https://code.jquery.com/jquery-1.12.4.js"></script>
site to refer
https://github.com/advisories/GHSA-gxr4-xjj5-5px2
https://github.com/advisories/GHSA-6c3j-c64m-qhgq
want to try this https://msrkp.github.io/?name={__proto__:{"protokey":"protovalue"}}
```
### getting prototype of inner html
```
var element = document.getElementById('HoF');
var prototype = Object.getPrototypeOf(element);

console.log(prototype);
```

