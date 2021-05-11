# State management: Provider

- `ChangeNotifier`
  - 리스너에 변화를 알려주는 클래스
  - 상태변화를 구독할 수 있음 (Observable)
  - 앱 상태를 캡슐화하는 방법 중 하나
  - 간단한 모델에서는 하나의 `ChangeNotifier`만 사용하면 되지만, 복잡한 구조에서는 여러개를 사용할 수 있음
  - `notifyListeners()`는 위젯에 바뀐 상태를 알려 모델을 리빌드시키는 역할
- `ChangeNotifierProvider`
  - `ChangeNotifier`의 인스턴스를 `ChangeNotifier`의 자식에게 제공해주는 위젯
  - 생성한 인스턴스가 필요해지지 않을때 자동으로 `dispose()`를 호출해줌
  - 1개 이상을 제공하려면 `MultiProvider`를 사용
- `Consumer`
  - `ChangeNotifierProvider`를 상단에서 선언하고나서 상태를 사용할 수 있게 해주는 위젯
  - `Consumer` 위젯을 쓸 때는 반드시 제네릭으로 모델을 삽입해줘야 함
  - `builder` 메서드
    - 함수로 `ChangeNotifier`에 변화가 생기면 호출됨
    - `notifyListeners()`를 호출할 경우 모든 `Consumer`의 `builder` 메서드가 호출됨
  - `Provider.of()`는 UI를 변경하지는 않지만 상태에 접근하고 할때 사용
    - 파라미터로 들어가는 `listen`은 기본값이 `false`