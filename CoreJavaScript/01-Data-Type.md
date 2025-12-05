# 01.데이터 타입(Data-Type)

## 1 - 1 데이터 타입의 종류

### 자바스크립트의 데이터 타입의 종류

![Alt text](../images/DataTypeImage.jpg)

- **기본형(primitive type)**

  - number (숫자)
  - string (문자열)
  - boolean (불리언)
  - null
  - undefined
  - symbol (심볼) **ES6 +**

- **참조형(reference type)**
  - object (객체)
  - array (배열)
  - function (함수)
  - date (날짜)
  - regExp (정규표현식)
  - map, weakMap, set, weakSet **(ES6 +)**

<br />

### 어떤 기준으로 기본형과 참조형을 구분 하는걸까?

일반적으로 기본형은 할당이나 연산 시 복제되고 참조형은 참조된다고 알려져 있습니다.
둘 다 모두 복제를 하지만 기본형은 값이 담긴 주소값을 바로 복제하는 반면 참조형은 값이 담긴 주소값들로 이루어진 묶음을 가리키는 주솟값을 복제한다는 점이 다릅니다.

**기본형은 불변성(immutability)을 뜁니다**
불변성을 잘 이해하려면 식별자와 변수의 개념을 구분할 수 있어야합니다.
