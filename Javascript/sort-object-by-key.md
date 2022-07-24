# key 순서로 객체 정렬시키기

```ts
function sortObject(obj) {
 Object
  .keys(obj)
  .sort()
  .reduce((o, k) => {
   o[k] = obj[k]
   return o
  }, {})
}
```
