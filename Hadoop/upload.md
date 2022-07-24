# WebHDFS 업로드 API 사용

- 공식문서에는 `curl` 호출방법이 다음과 같이 나와있다

```bash
# from namenode
curl -i -X PUT "http://<HOST>:<PORT>/webhdfs/v1/<PATH>?op=CREATE"

# from datanode
curl -i -X PUT -T <LOCAL_FILE> "http://<DATANODE>:<PORT>/webhdfs/v1/<PATH>?op=CREATE"
```

- 위처럼 로컬에서 도커 컨테이너에 `curl`을 날리면 500이 날아온다
- `namenode`에서 `datanode`로 리디렉션을 시키는데 도커 컨테이너에서는 서로 격리된 환경이라 `localhost:<PORT>`식의 호출로는 서로의 호스트를 찾지 못한다
- `datanode`에 직접 호출을 다음과 같이 날릴 수 있다

```bash
curl -i -X PUT -T <LOCAL_FILE> "http://<DATANODE>:<PORT>/webhdfs/v1/<PATH>/<LOCAL_FILE>?op=CREATE&namenoderpcaddress=namenode:9000&createflat=&createparent=true&overwrite=false"
```

- javascript에서 `axios`로 `put` 호출을 할 떄는 다음과 같이 해야한다

```tsx
import FormData from 'form-data'

const params = new URLSearchParams()
params.append('op', 'CREATE')
params.append('namenoderpcaddress', 'namenode:9000')
params.append('createflag', '')
params.append('createparent', 'true')
params.append('overwrite', 'false')

const fileData = new FormData()
fileData.append('filename', fs.readFilySync(file))

await axios.put(`${url}/${path}/${filename}?${params.toString()}`, fileData, {
 headers: {
  'Content-Type': 'multipart/form-data'
 }
})
```
