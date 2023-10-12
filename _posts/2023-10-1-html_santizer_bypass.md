## html santizer bypass by liveoverflow
```
https://www.youtube.com/watch?v=HUtkW2gjC8Q
<html>
<body>
<11 a="b<img src=x onerror=alert(1)>">test</11>
</body>
</html>
document.body.innerHTML
HTML encoding vs sanitizing
for the above if we submit to server( basic santizer on server side) it will see l1 as no harm and let the attribute stay
but browser tries to render it  and alert will be popped
vs code as well parses html differentyly
```
## dom purify
```
it works on dom
https://github.com/cure53/DOMPurify
browser and dom purify understand interpret the html in same manner and hence dom purify works pefectly

```
