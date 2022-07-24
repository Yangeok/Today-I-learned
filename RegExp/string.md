# 정규식 문자열 취급

```js
function escapeRegExp(string){
  return string.replace(/[.*+?^${}()|[\]\\]/g, "\\$&")
}
```

- `$&`는 일치한 전체 문자열을 의미함
