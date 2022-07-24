# 데이터프레임 리스트 펼치기

- 다음과 같은 데이터프레임에서 구분자(,)가 있는 문자열이 있는 열을 아래로 펼치려면 다음과 같이 할 수 있다

name | list
--- | ---
1 | ,a,b,c
2 | b,e,f
3 | ,b,c,d

- 우선 문자열을 split할 수 있다

```python
df = pd.DataFrame({ 'name': [1, 2, 3],
          'list': [',a,b,c', 'b,e,f', ',b,c,d']
         })

df['list'] = df['list'].str.split(',', expand=False)
```

name | list
--- | ---
1 | [, a, b, c]
2 | [b, e, f]
3 | [, b, c, d]

- `list`에 배열로 들어있는 아이템을 펼쳐준다

```python
df = df.explode('list')
```

name | list
--- | ---
1 |
1 | a
1 | b
1 | c
2 | b
2 | e
2 | f
3 |
3 | b
3 | c
3| d

- 배열에 빈 문자열로 들어간 문자열까지 같이 펼쳐져서 빈 문자열이 있는 열을 없애줘야 한다

```python
nan_value = float('NaN')
df.replace('', nan_value, inplace=True)

df = df.dropna()
```

name | list
--- | ---
1 | a
1 | b
1 | c
2 | b
2 | e
2 | f
3 | b
3 | c
3| d
