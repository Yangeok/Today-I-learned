# type guard란

- 타입 단언을 좀 더 깔끔하게 할 수 있도록 도와준다.
- 타입가드는 런타임에서 타입체크를 컴파일러에게 알려주는 기능을 한다.
- `var is type`과 같은 문법을 사용해 선언하면 된다.

```ts
class Character {
  isWizard(): this is Wizard {
  return this instanceof Wizard;
  }
  isWarrior(): this is Warrior {
  return this instanceof Warrior;
  }
}
```
