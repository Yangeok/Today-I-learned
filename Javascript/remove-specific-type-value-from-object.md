# 객체에서 어떤 타입의 값 제거하기

- 어떤 객체에서 제네릭하게 배열을 지우고 싶다고 가정하고, 아래의 객체를 예로 들어본다.

```jsx
const obj = {
	a: 1,
	b: 2,
	c: 3,
	d: [1, 2, 3, 4, 5]
}
```

- 이 객체 뿐만 아니라 다른 여러 형태의 객체에도 범용적으로 적용할 수 있는 함수를 작성해본다

```jsx
const removeSpecificTypeKeyFromObject = type => obj => {
	const entries = Object.entries(obj)
	const removeType = i => typeof i[1] !== type
	return Object.fromEntries(entries.filter(removeType))
}
```

- 한 줄씩 이해하면서 넘어가보자
    - `const removeSpecificTypeKeyFromObject = type => obj => {`(line 1)은 고차 함수다. 이유는 `Array` 메서드 안에 고차 함수로 사용하기 위함이다.
    - `const ent ries = Object.entries(obj)`(line2)는 객체를 배열로 바꾸기 위해 사용했다. `Object.entries()`는 인자로 객체를 넣으면 `[key, value]` 형태의 배열로 반환한다.
    - `const removeType = i => typeof i[1] !== type`(line 3)는 첫번째 파라미터였던 `type`과 `value`의 타입이 같으면 `true`를 반환하는 함수이다. `Array.filter()`에 고차 함수로 사용하기 위해 선언했다.
    - `return Object.fromEntries(entries.filter(removeType))`(line 4)에서 `entries` 배열 중 삭제할 타입만 지운 다음 다시 객체로 되돌리기 위해 `Object.fromEntries()`를 사용한다. `Object.fromEntries()`의 인자는 iterable한 배열이나 `Map`, `Set` 타입을을 집어넣을 수 있다.
- 호출해서 받은 응답의 인터페이스가 상이한 어떤 API 2개가 있다고 가정하자. 응답값은 각각 아래와 같다.

```jsx
const result1 = {
	list: [
	  {
			id: 1,
			name: 'foo'
		},
		{
			id: 2,
			name: 'bar'
		}
	],
	desc: 'baz'
}
```

- `result1`은 객체다. 이 객체를 `removeSpecificTypeKeyFromObject` 함수를 사용해 가공해서 아래와 같은 결과를 얻을 수 있다. 값이 배열인 프로퍼티 `list`는 javascript 원시타입이 `object`라 첫 번째 인자로 `object`가 들어간다. 두 번째 인자로 API 호출결과인 객체가 들어간다.

```jsx
const concatable1 = removeSpecificTypeKeyFromObject('object', result1)
```

- 함수 실행결과는 아래와 같다.

```jsx
{
	desc: 'baz'
}
```

- `result1.list`에 `concatable1`을 합쳐주면 원하는 형태의 결과물을 아래와 같이 얻을 수 있다.

```jsx
const data1 = reuslt1.map(i => ({ ...i, ...concatable1 }))
```

```jsx
[
  {
		id: 1,
		name: 'foo',
		desc: 'baz'
	},
	{
		id: 2,
		name: 'bar',
		desc: 'baz'
	}
],
```

- `result2`는 배열이다. 배열은 `removeSpecificTypeKeyFromObject`  함수를 사용하기 위해 `Array.map(****)` 안에서 고차 함수를 한 겹 벗겨서 집어넣어준다.

```jsx
const result2 = [
	{
		list: [
			{
				id: 1,
				name: 'foo'
			},
			{
				id: 2,
				name: 'bar'
			},
		],
		common: 'baz'
	},
	{
		list: [
			{
				id: 3,
				name: 'faz'
			},
			{
				id: 4,
				name: ****'far'
			},
		],
		common: 'qux'
	}
]
```

```jsx
const concatable2 = result.map(removeSpecificTypeValueFromObject('object'))
```

- `i ⇒ removeSpecificTypeValueFromObject('object')(i)`와 같은 구문이 되지만, 콜백인자 `i`를 제거하면 축약형으로 가독성을 높일 수 있다.
- 함수 실행결과는 다음과 같다.

```jsx
[
	{
		common: 'baz'
	},
	{
		common: 'qux'
	}
]
```

- `result2[i].list`에 `concatable2`을 합쳐주면 원하는 형태의 결과물을 아래와 같이 얻을 수 있다.

```jsx
const data2 = result2
	.map((i, idx) => i.list
		.map(j => ({ 
			...j, 
			...concatable2[idx] 
		})))
	.flat()
```

```jsx
[
	{
		id: 1,
		name: 'foo',
		common: 'baz'
	},
	{
		id: 2,
		name: 'bar',
		common: 'baz'
	},
	{
		id: 3,
		name: 'faz',
		common: 'qux'
	},
	{
		id: 4,
		name: 'far',
		common: 'qux'
	},
]
```

커링을 사용하려면 아래와 같이 함수 파라미터를 변경해줘야 한다. 고차 함수에서 일반함수로 바꿔준다.

```ts
// as-is
const removeSpecificTypeKeyFromObject = type => obj => {
	const entries = Object.entries(obj)
	const removeType = i => typeof i[1] !== type
	return Object.fromEntries(entries.filter(removeType))
}

// to-be 
const removeSpecificTypeKeyFromObject = (type, obj) => {
	const entries = Object.entries(obj)
	const removeType = i => typeof i[1] !== type
	return Object.fromEntries(entries.filter(removeType))
}
```

이제 커리를 함수로 구현할 차례다. 구현이 중요하지는 않다. 사용이 중요하다.
```ts
function curry(func) {
  return function curried(...args) {
    if (args.length >= func.length) {
      return func.apply(this, args)
    } else {
      return function(...args2) {
        return curried.apply(this, args.concat(args2))
      }
    }
  }
}
```

커리를 적용한 result1은 다음과 같이 바꿀 수 있다.

```ts
// as-is
const concatable1 = removeSpecificTypeKeyFromObject('object')(result1)

// to-be
const concatable1 = removeSpecificTypeKeyFromObject('object', result1)
```

마찬가지로 result2는 다음과 같이 바꿀 수 있다.

```ts
// as-is
const concatable2 = result.map(removeSpecificTypeValueFromObject('object'))

// to-be
const concatable2 = result.map(curry(removeSpecificTypeValueFromObject)('object'))
```