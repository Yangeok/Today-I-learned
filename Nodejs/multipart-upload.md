# 멀티파트 업로드

- `express`에서 `multiparty`를 미들웨어로 사용하기 위해 `multiparty-express`를 사용했다
- `post` 메서드로 `body`의 `form-data`에 파일을 업로드하면 `req.files`에서 받아볼 수 있다
- `form-data`에 `file`이란 이름으로 파일을 업로드하면 다음과 같이 `req.files`를 찍어볼 수 있다

```tsx
{
  file: [
    {
      fieldName: 'file',
      originalFilename: '전남도청 API.postman_collection.json',
      path: '/var/folders/rd/3chs9m2n68q_4lnf9cmmrky00000gn/T/DfD9IAb6sfPuZX9h0xj8FsJu.json',
      headers: [Object],
      size: 2199
    }
  ]
}
```

- `post` 요청시 같이 보낸 파일은 `req.files.file[i].path`에 저장이 된다
- `multiparty-express`에서 `cleanup` 함수를 꺼내서 사용하면 임시 폴더에 저장된 파일을 지울 수 있다는데 정상동작하지 않는 것 같다
- `multiparty`를 사용하면서 콜백이 보기싫을때는 wrapper를 하나 만들어 다음과 같이 사용할 수 있다

```tsx
const promiseMultiparty = (req: Request): any =>
   new Promise((resolve, reject) => {
     const form = new multiparty.Form()

     form.parse(req, (err, fields, files) => {
       if (err) return reject(err)

       return resolve([fields, files])
     })
   })

await promiseMultiparty()
```