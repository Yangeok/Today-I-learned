# 제네릭 관련 예약어

- `keyof`: 속성을 포함하는 대상을 찾아 유니언 타입처럼 동작시킴

    ```ts
    interface IFoo {
     prop1: any
     prop2: any
    }
    
    type LookedUp = keyof IFoo // 'prop1' | 'prop2'
    ```

- `typeof`: 타입 정의에서도 다음과 같이 응용 가능

    ```ts
    // way 1
    type Predicate = (x: unkown) => boolean
    type K = ReturnType<Predicate> // boolean
    
    // way 2
    function f() {
     return { x: 10, y: 3 }
    }
    type P = ReturnType<typeof f> // { x: number; y: number; }
    ```

- 인덱스 접근: `Type[’a’]`와 같이 특정 프로퍼티에 접근하는 룩업 방식

    ```ts
    type Person = {
     age: number
     name: string
     alive: boolean
    }
    type Age = Person['age']
    
    type I1 = Person['age' | 'name']
    type I2 = Person[keyof Person] // string | number | boolean
    
    type AliveOrName = 'alive' | 'name'
    type I3 = Person[AliveOrName] // string | number
    
    const array = [
     { name: 'foo', age: 1 },
     { name: 'bar', age: 2 },
    ]
    type Person = typeof array[number] // { name: string; age: number; }
    
    const key = 'age'
    type Age = Person[key] // not working
    ```

- 조건부: 조건식 연산자를 통해 타입 표기

    ```tsx
    interface IIdLabel {
     id: number
    }
    interface INameLabel {
     name: string
    }
    
    type NameOrId<T etxtends number | string> = T extends number
     ? IIdLabel
     : NameLabel
    
    type MessageOf<T extends { message: unkown }> = T['message']
    interface Email {
     message: string
    }
    type EmailMessageContents = MessageOf<Email> // string
    
    type ToArray<T> = T extends any ? T[] : never
    type StrOrNumberArr = ToArray<string | number> // string[] | number[]
    ```
