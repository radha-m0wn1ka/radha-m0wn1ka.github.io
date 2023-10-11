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

```
