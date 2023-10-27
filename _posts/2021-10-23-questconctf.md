## questcon
## web web explorer
```
Web Explorer's Journey
483
Ahoy, matey! a bottle of code! Captain Jack Sparrow has hidden his secret pirate flag using
the ancient JavaScript Cipher. It's your duty to decipher the code and uncover the hidden treasure, savvy?

https://web-explorer.netlify.app
```
### script
```
let flag = "flag{Test_Flag}";
let encryptedFlag = "";
function encodeFlag() {
  for (let i = 0; i < flag.length; i++) {
    encryptedFlag += flag.charCodeAt(i);
  }
}

encodeFlag();
document.getElementById("flag").innerHTML = encryptedFlag;
```
### hint
```
<div class="displaynone">
        NOTE: Flag contains only capial letters, numbers and curly brackets.
      </div>
Your flag is:
81856983846779781238751669551888076488251829549839552875183487751125
```
### solving
```
https://asecuritysite.com/coding/asc2
capital letters 65-90
numbers         48-57
parenthesi 123{,125}

 Flag format: QUESTCON{C2s3_s3ns1T1v3_F1Ag} (Not a real one though :( )
8185698384677978    123 87 51 66 95 51 88 80 76 48 82 51 82 95 49839552875183487751 125
len(QUESTCON)=8
hence 16 numbers from the flag are questcont
```
### python script
```
a={1:2,3:4}
a[1]=2
```
#### map
```
def myfunc(a):
  return len(a)

x = map(myfunc, ('apple', 'banana', 'cherry'))
#function and iteratble 
print(x)

#convert the map into a list, for readability:
print(list(x))
```
#### example
```
print("Hello world")
a=lambda p,q :(p,q)
print(type(a(2,3)))
# ans tuple
print(dict([(2,3)]))
ans{2:3}
```
### python code
```

print("Hello world")
keys=[]
values=[]
letters=[]
flag=[]
for i in range(48,58):
    keys.append(i)
    values.append(chr(i))
for i in range(65,91):
    keys.append(i)
    values.append(chr(i))
string="8751669551888076488251829549839552875183487751"
keys.append(95)
values.append('_')
res = dict(map(lambda i,j : (i,j) , keys,values))
print(res)
i=0
while(i<46):
    pos=string[i]+''+string[i+1]
    i=i+2
    letters.append(int(pos))
for i in letters:
    print((res[i]))
    
    
    
```
### flag
QUESTCON{W3B_3XPL0R3R_1S_4W3S0M3}
