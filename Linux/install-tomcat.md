# Tomcat 8.5 설치

```bash
tar -xvfz apache-tomcat-8.5.66.tar.gz
```

- 압축이 풀려 나온 폴더를 해당 폴더로 옮긴다

```bash
cd /usr/local/lib
mv /home/opc/tomcat/apache-tomcat-8.5.66 .
```

- 방화벽을 열어준다

```bash
firewall-cmd --permanent --zone=public --add-port=8080/tcp
firewall-cmd --reload
```

- 아래 스크립트 파일로 실행하고 중지할 수 있다

```bash
# /usr/local/lib/apache-tomcat-8.5.66/bin
./startup.sh # 실행
./shutdown.sh # 중지
```
