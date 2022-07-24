# 이미지 순차 다운로딩하기

- 이미지 목록을 배열로 미리 뽑아둔다
- 아래와 같이 응답값을 `stream`으로 받아오도록 설정하고, 스트림 파이핑을 해준다

```ts
import * as fs from 'fs'

const outputPath = 'path/to/location'
const format = 'specific_format'
let urls = []

urls.reduce(async (prevPromise, i: string, idx: number) => {
 await prevPromise

 const { data } = await axios.get(i, { responseType: 'stream' })
 data.pipe(fs.createWriteStream(path.join(__dirname, outputPath, `/${String(idx + 1)}.${format}`)))
  }, Promise.resolve())
```
