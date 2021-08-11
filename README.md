# lexicographical-radix64
Snippet to convert integers to radix64 strings in lexicographical order

```javascript
const digit = "-0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ_abcdefghijklmnopqrstuvwxyz";
toB64 = x=>x.toString(2).split(/(?=(?:.{6})+(?!.))/g).map(v=>digit[parseInt(v,2)]).join("")
fromB64 = x=>x.split("").reduce((s,v,i)=>s=s*64+digit.indexOf(v),0)

//let ini = Date.now()
let ini = 1628698411335

// Tests:

for (var i = 0; i < 100000; i++) {
  let nowB64 = toB64(ini+i)
  let nextB64 = toB64(ini+i+1)
  
  if (ini+i !== fromB64(nowB64)) {
    console.log('error fromB64')
  }
  
  if (nowB64 >= nextB64) {
    console.log('error: not lexicographical')
  }
}
```
