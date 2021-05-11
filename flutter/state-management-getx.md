# State management: GetX

- provider: 데이터를 만드는 곳과 사용하는 곳이 분리되어 코드관리가 수월해지고, 옵저버 패턴과 유사하다.
  - 기본
    - 데이터 생산: 생성에는 데이터 타입을 정의해야 한다.
      ```dart
      Provider<int>.value(
        value: 5,
        child: Container(),
      )
      ```
    - 데이터 소비: `Provider`에서 제공하는 데이터를 사용하기 위해 `Provider.of(context)`나 `Consumer()` 위젯을 사용한다.
      ```dart
      var data = Provider.of<int>(context)
      ```
  - 변하는 상태
    - `setState`와 같은 일을 수행하기 위해서 `Provider`에서는 `ChangeNotifier`를 사용한다. `ChangeNotifier`를 믹스인한 클래스는 `notifyListener()`를 호출할 수 있다. 해당 함수를 사용시 UI가 업데이트된다.
      ```dart
      class Counter with ChangeNotifier {
        int _counter;
        Counter(this._counter);

        getCounter() => _counter;
        setCounter(int counter) => _counter = counter;

        void increment() {
          _counter++;
          notifyListeners();
        }
        void decrement() {
          _counter--;
          notifyListeners();
        }
      }
      ```
    - 변경되는 값을 사용하기 위해 `ChangeNotifierProvider`로 위젯을 감싼다. `ChangeNotifierProvider`를 사용하기 위해서는 타입을 정의해야 한다. `Counter` 클래스의 데이터가 변하는지 리스닝하다 변하면 알려주고, 초기값을 지정할 수 있다.
      ```dart
      class App extends StatelessWidget {
        @override
        Widget build(BuildContext context) {
          return ChangeNotifierProvider<Counter>(
            builder: (_) => Counter(0),
            child: MaterialApp(
              home: HomePage(),
            ),
          );
        }
      }
      ```
    - `MaterialApp` 부모 위젯에 정의해준 `Provider` 데이터를 사용하기 위해 데이터를 선언해야 한다. `Provider.of()`로 정의한 타입의 데이터를 불러와 변수에 입력한다. 
      ```dart
      class HomePage extends StatefulWidget {
        HomePage({ Key key }) : super(key: key);

        @override
        _HomePageState createState() => _HomePageState();
      }

      class _HomePageState extends State<HomePage> {
        @override
        Widget build(BuildContext context) {
          final counter = Provider.of<Counter>(context);

          return Scaffold(
            appBar: AppBar(),
            body: Center(),
            floatingActionButton: Column(
              mainAxisAlignment: MainAxisAlignment.end,
              children: <Widget>[
                FloatingActionButton(
                  onPressed: counter.increment, // here
                  tooltip: 'increment',
                ),
                FloatingActionButton(
                  onPressed: counter.decrement, // here
                  tooltip: 'decrement',
                )
              ],
            ),
          );
        }
      }
      ```
  - 여러 `Provider` 동시 사용
    - `Provider`가 중첩될수록 복잡도가 올라간다. 이 경우 `MultiProvider`를 이용한다. `MultiProvider`는 `providers` 속성에 원하는 `Provider`를 작성하면 된다. `Row`, `Column`과 비슷하게 여러개를 작성할 수 있다.
      ```dart
      MultiProvider(
        providers: [
          Provider<int>.value(value: 50),
          Provider<String>.value(value: 'Foo'),
        ]
      )
      ```
    - 자료형으로 어떤 값을 가져올지 구분한다. 만약 동일한 자료형을 여러번 정의한다면 가장 밑에 있는 `Provider`에 접근한다. 즉 200을 가져온다.
      ```dart
      MultiProvider(
        providers: [
          Provider<int>.value(value: 50),
          Provider<int>.value(value: 100),
          Provider<int>.value(value: 200),
        ]
      )
      ```
    - `Provider`로 정의한 데이터들을 `number`, `string` 변수에 `int`, `String` 타입으로 가장 가까운 `Provider`에서 불러오도록 작성한 코드이다.
      ```dart
      class _HomePageState extends State<HomePage> {
        @override
        Widget build(BuildContext context) {
          final number = Provider.of<int>(context);
          final string = Provider.of<String>(context);

          return Scaffold(
            appBar: AppBar(),
            body: Center(
              child: Column(
                children: <Widget>[
                  Text(
                    'Number: $number',
                  ),
                  Text(
                    'String: $string',
                  ),
                ],
              ),
            ),
          );
        }
      }
      ```