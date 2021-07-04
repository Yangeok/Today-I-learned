# 디렉토리 내 파일 압축하기

- 폴더 다운로드 플러그인이 설치되지 않은 경우에 아래와 같이 스크립트를 짤 수 있다

```python
import os
import tarfile

def recursive_files(dir_name='.', ignore=None):
    for dir_name,subdirs,files in os.walk(dir_name):
        if ignore and os.path.basename(dir_name) in ignore: 
            continue

        for file_name in files:
            if ignore and file_name in ignore:
                continue

            yield os.path.join(dir_name, file_name)

def make_tar_file(dir_name='.', tar_file_name='tarfile.tar', ignore=None):
    tar = tarfile.open(tar_file_name, 'w')

    for file_name in recursive_files(dir_name, ignore):
        tar.add(file_name)

    tar.close()

output_path = 'path/to/location'
output_filename = 'filename'

ignore = {'.ipynb_checkpoints', '__pycache__', output_filename}
make_tar_file(output_path, output_filename, ignore)
```