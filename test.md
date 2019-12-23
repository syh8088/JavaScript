#JavaScript

###탄생
#####유효성 검사를 위한 Javascript
- 문제 상황 : 로그인 시 아이디와 비밀번호 입력 없이 로그인 버튼만 눌러도 프로세스가 올라간다.

- 문제점 : 서버 자원 방비, 디도스 공격 위험

- 해결방안 : 유효한 입력값이 입력 되었는지 폼 객체 검사 후 서버에 전송

- 폼 객체 : html 문서와 같은 구조의 폼 객체가 생성 되면 프로그래밍 언어를 사용해 조건식으로 입력값을 걸러낸다.
 
 
###데이터 객체와 wrapper class
 
##### 변수 선언
```javascript
var x = 3;
var x = 3.5;
var x = 'A';
var x = "JAEYEON"
```
위와 같이 정수, 실수, 문자, 문자열 모두 var로 선언한다.

#####메모리 공간 할당
모두 var로 선언을 하면 메모리 공간 할당은 어떻게 할까?

-JavaScript에 내장 되어 있는 Wrapper class가 Auto boxing을 한다. 

#####Wrpper Class
- 부울 Boolean

- 정수, 실수 Number

- 문자, 문자열 String
```javascript
var x = 3;
var x = new Number(3);
```
위의 두개의 식은 같은 완전히 같은 식으로, var x =3 이라는 선언만으로도 wrapper class로 인해 자동으로 정수에 해당되는 메모리 공간이 할당된다.

#####undefined
```javascript
var x;
if (x == undefined){
    document.write("ABC");
}
```
변수는 선언되어 있으나 값을 할당하지 않아 참조하는 객체가 없는 상태를 undefined 상태라고 한다.

undefined 역시 하나의 값으로 조건문 등에 이용할 수 있다.

###변수의 영역

```javascript
var a = 1;
alert(a);
```
위의 식은 기본적인 식으로 출력값은 1이다.
```javascript
alert(a);
var a = 1;
```
출력값 : undefined
 
변수 선언은 코드 실행 전에 된다는 것을 알 수 있다.

```javascript
a = 1;
alert(a);
```
출력값 : 1

a = 1은 window.a =1이다.

앞의 window를 생략하고 쓴 것과 같기 때문에 var를 이용한 변수 선언 없이도 error가 발생하지 않는다. 

```javascript
alert(a);
a = 1;
```
error 발생

a라는 변수가 정의조차 되어 있지 않은 상태이다.
```javascript
var f = function() {
    a = 1;
    var a = 3;
    a++;
    alert(a);
}
f();
```
출력값 : 4

a = 1 즉 window.a = 1은 위치에 상관 없이 전역 변수인 반면, var a = 3은 함수 내에서만 존재하는 지역 변수이다. 이렇게 전역 변수과 지역 변수가 충돌할 시에는 지역 변수의 우선 순위가 더 높으므로 a는 3이 된다.

###클로저(Closure)
```javascript
function f1() {
    var a =1;
    
    return function f2() {
        return a;      
    }  
}

var f = f1();
var a = f();
alert(a);
```
- funtion f2()에서는 자신보다 윗 함수인 f1의 지역변수 a를 사용하는게 가능하다.

변수 f를 선언하면서 함수 f1를 호출하게 되면 return 되는 값이 함수 f2()이다. 그런데 f2()는 다시 a를 return하고 있으므로 최종적으로는 a의 값인 1이 변수 f에 할당이 된다.
var a = f()에서 변수 a는 그런 f를 호출하고 있으므로 역시 1이라는 값이 할당된다.

여기에서, var f = f1()으로 f1은 호출이 끝났지만 var a = f()에서 다시 한번 호출이 되어져 결국엔 함수 f2까지 호출 되어야한다. 이럴 경우 f1()은 앞의 호출이 끝났더라도 f2()를 위해 함수를 닫지 않는다. 
이러한 f2()를 바로 클로저라고 한다.