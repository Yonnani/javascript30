# 04 - Array Cardio Day 1

### 1. Filter the list of inventors for those who were born in the 1500's

#### Array.prototype.filter()

> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/filter

- `filter()` 메소드는 제공된 함수로 구현된 테스트를 통과하는 모든 요소가 있는 새로운 배열을 만듦

- 구문

  ```javascript
  var new_array = arr.filter(callback[, thisArg])
  ```

  - 매개변수
    - `callback` 
      - 배열의 각 요소를 테스트하는 함수
      - 인수 `(element, index, array)`와 함께 호출됨
      - 요소를 (새 배열에) 계속 두기 위해 `true`를 반환, 그렇지 않으면 `false`를 반환
    - `thisArg`
      - 선택사항
      - `callback`을 실행할 때 `this`로 사용하는 값
  - 반환값
    - 테스트를 통과한 요소가 있는 새로운 배열

- 예제

  ```javascript
  // 1. Filter the list of inventors for those who were born in the 1500's
  let filteredList = inventors.filter(inventor => (inventor.year >= 1500 && inventor.year < 1600));
  console.table(filteredList);
  ```

### 2. Give us an array of the inventors' first and last names

#### Array.Prototype.map()

> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map

- `map()` 메소드는 배열 내의 모든 요소 각각에 대하여 제공된 함수(callback)를 호출하고, 그 결과를 모아서, 새로운 배열을 반환함

- 구문

  ```javascript
  var new_array = arr.map(function callback(currentValue[, index[, array]]) {
      // new_array의 새 요소 반환
  }[, thisArg])
  ```

  - 매개변수
    - `callback`
      - 새로운 배열 요소를 생성하는 함수
      - 인수 `currentValue` : 배열의 요소 중, 현재 처리되고 있는 요소
      - 인수 `index` : 현재 처리되는 요소의 배열 내 인덱스
      - 인수 `array` : map 메소드가 적용되는 본래 배열
    - `thisArg`
      - 선택사항
      - `callback`을 실행할 때 `this`로 사용되는 값

- 예제

  ```javascript
  // Array.prototype.map()
  // 2. Give us an array of the inventors' first and last names
  let nameList1 = inventors.map(inventor => inventor.first + ' ' + inventor.last);
  console.table(nameList1);
  let nameList2 = inventors.map(inventor => `${inventor.first} ${inventor.last}`);
  console.table(nameList2);
  ```

  - ES6부터 템플릿 문자열 사용 가능

    > https://www.zerocho.com/category/EcmaScript/post/5759b3a732522e883c6f6ddb

### 3. Sort the inventors by birthdate, oldest to youngest

#### Array.prototype.sort()

> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/sort

- `sort()` 메서드는 배열의 요소를 적절한 위치에 정렬하고 배열을 반환함

- 구문

  ```javascript
  arr.sort([compareFunction])
  ```

  - 매개변수

    - `compareFunction`

      - 선택사항

      - 정렬 순서를 정의하는 함수를 지정함 (생략하면 각 요소의 문자열 변환에 따라 각 문자의 유니 코드 포인트 값에 따라 정렬됨)

      - `compareFunction(a, b)`이 0보다 작은 경우 a를 b보다 낮은 색인으로 정렬함(오름차순)

        `compareFunction(a, b)`이 0보다 큰 경우, b를 a보다 낮은 인덱스로 소트함(내림차순)

        ``` javascript
        function compare(a, b) {
            if (a is less than b by some ordering criterion) {
                return -1;
            }
            if (a is greater than b by the ordering criterion) {
                return 1;
            }
            // a must be equal to b
            return 0;
        }
        ```

  - 반환값

    - 정렬된 배열
    - 원 배열이 정렬됨(복사본 아님)

- 예제

  ```javascript
  // Array.prototype.sort()
  // 3. Sort the inventors by birthdate, oldest to youngest
  inventors.sort((a, b) => {
      if (a.year > b.year) {
          return 1;
      } else {
          return -1;
      }
  });
  inventors.sort((a, b) => (a.year > b.year ? 1 : -1));
  inventors.sort((a, b) => a.year - b.year);
  ```

### 4. How many years did all the inventors live?

#### Array.prototype.reduce()

> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce

- `reduce()` 메서드는 왼쪽에서 오른쪽으로 이동하며 배열의 각 요소마다 누적 계산 값과 함께 함수를 적용해 하나의 값으로 줄임

- 구문

  ```javascript
  arr.reduce(callback[, initialValue])
  ```

  - 매개변수
    - `callback`
      - 배열의 각 (요소) 값에 실행할 함수
      - 인수 `accumulator` : 누적 계산값은 콜백의 반환값을 누적함
      - 인수 `currentValue` : 배열 내 현재 처리되고 있는 요소(element)
      - 인수 `currentIndex` : 배열 내 현재 처리되고 있는 요소의 인덱스. `initialValue`가 주어진 경우 0부터, 그렇지 않으면 1부터 시작함
      - 인수 `array` : `reduce`가 호출된 배열
    - `initialValue`
      - 선택사항
      - `callback`의 첫 호출에 첫 번째 인수로 사용하는 값

- 예제

  ```javascript
  // Array.prototype.reduce()
  // 4. How many years did all the inventors live?
  let totalYears = inventors.reduce((total, inventor) => {
      return total + (inventor.passed - inventor.year)
  }, 0);
  ```

### 5. Sort the inventors by years lived 

```javascript
inventors.sort(function (a, b) {
    const lastGuy = a.passed - a.year;
   	const nextGuy = b.passed - b.year;
    return lastGuy > nextGuy ? -1 ; 1;
});
```

### 6. create a list of Boulevards in Paris that contain 'de' anywhere in the name

> https://en.wikipedia.org/wiki/Category:Boulevards_in_Paris

```javascript
const category = document.querySelector('.mw-category');
const nodes = category.querySelectorAll('a'); // NodeList로 반환됨
const links = [...nodes];
const links = Array.from(nodes);

const de = links
			.map(link => link.textContent)
			.filter(streetName => streetName.includes('de'));
```

- 유사 배열 vs 배열

  > https://www.zerocho.com/category/JavaScript/post/5af6f9e707d77a001bb579d2

- Spread 문법

  > https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Spread_syntax

### 7. sort Exercise

#### Sort the people alphabetically by last name

```javascript
const people = ['Beck, Glenn', 'Becker, Carl', 'Beckett, Samuel', 'Beddoes, Mick', 'Beecher, Henry', 'Beethoven, Ludwig', 'Begin, Menachem', 'Belloc, Hilaire', 'Bellow, Saul', 'Benchley, Robert', 'Benenson, Peter', 'Ben-Gurion, David', 'Benjamin, Walter', 'Benn, Tony', 'Bennington, Chester', 'Benson, Leana', 'Bent, Silas', 'Bentsen, Lloyd', 'Berger, Ric', 'Bergman, Ingmar', 'Berio, Luciano', 'Berle, Milton', 'Berlin, Irving', 'Berne, Eric', 'Bernhard, Sandra', 'Berra, Yogi', 'Berry, Halle', 'Berry, Wendell', 'Bethea, Erin', 'Bevan, Aneurin', 'Bevel, Ken', 'Biden, Joseph', 'Bierce, Ambrose', 'Biko, Steve', 'Billings, Josh', 'Biondo, Frank', 'Birrell, Augustine', 'Black, Elk', 'Blair, Robert', 'Blair, Tony', 'Blake, William'];

people.sort((a, b) => {
    // const aLastName = a.split(', ')[0];
    // const bLastName = b.split(', ')[0];
    const [aLastName, aFirstName] = a.split(', ');
    const [bLastName, bFirstName] = b.split(', ');
    return aLastName > bLastName ? 1 : -1;
});
```

- 비구조화 할당

> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment

### 8. Reduce Exercise

#### Sum up the instances of each of these

```javascript
const data = ['car', 'car', 'truck', 'truck', 'bike', 'walk', 'car', 'van', 'bike', 'walk', 'car', 'van', 'car', 'truck' ];
const transportation = data.reduce((obj, item) => {
    if (!obj[item]) {
        obj[item] = 0;
    }
    obj[item]++;
    return obj;
}, {});
```

