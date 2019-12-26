#window platform
보통은 window를 생략하여 사용하며, 생략하지 않을 경우 그만한 이유가 존재해야 함

###alert
윈도우 창을 띄운다.
```javascript
var x = 3;
var y = 0;
window.alert(x+y);
```

###prompt
user에게 값을 입력 받기 위한 창을 띄운다.
```javascript
var x, y;
x = prompt("x값 입력");
y = prompt("y값 입력");
alert(x+y);
```
하지만 x=3, y=4를 입력할 경우 7이 아니라 34가 출력된다.

prompt를 이용하여 값을 입력 받으면 변수에 값이 문자열로 전달되어진다.

이를 해결하기 위해 parseInt를 사용한다.

###parseInt
값을 Int형으로 변환한다.
```javascript
x = prompt("x값 입력");
y = parseInt(prompt("y값 입력"));
x = parseInt(x);
alert(x+y);
```
출력값 : 7

###confirm 
확인과 취소 버튼이 있는 창을 띄운다.
```javascript
var answer = "삭제 하시겠습니까?";
if(answer)
    alert("삭제 되었습니다.");
```
확인을 누를 경우 answer에는 true(1), 취소를 누를 경우 false(0) 값이 전달된다. 

#Programming based on event
페이지가 읽혀질 때 실행
```javascript
<script>
</script>
```
이벤트가 발생할 때 실행
```javascript
<input onclick = ""/>
<input onmouseover = ""/>
```
가독성을 위해 script와 event를 적절히 함께 사용한다.

- event만 사용
```javascript
<input type = "button" value="출력" onclick="var x,y;" +
 "x= prompt("x값 입력");y=prompt("y값 입력"); alert(x+y);"/>
```
- script와 event 함께 사용
```javascript
<script>
function printResult() {
    var x,y;
    x = prompt("x값 입력");
    y = prompt("y값 입력");
    alert(x+y);
}
</script>
<head/>
<body>
<input type = "button" value = "출력" onclick = "printResult();"/>
```

#Element objects
```javascript
<script>
function printResult() {
    var x,y;
    x = prompt("x값 입력");
    y = prompt("y값 입력");
    btnPrint.value = x+y;
}
 btnPrint.onclick = printResult();
</script>
<head/>
<body>
<input type = "button" value = "출력" id ="btnPrint"/>
```
앞의 코드에 id값을 주어 value값을 printResult()함수에서 다룰 수 있게 수정했다.

하지만 이 코드는 error가 발생하는데, 그 원인은 btnPrint 객체가 아직 선언되지 않은 상태에

btnPrint를 불러내고 있기 때문이다. 해결 방안은 아래와 같이 두가지이다.
 
- 객체 선언 코드를 객체 호출 전에 삽입한다.
 ```javascript
<head>
 <input type = "button" value = "출력" id ="btnPrint"/>
 <script>
 function printResult() {
     var x,y;
     x = prompt("x값 입력");
     y = prompt("y값 입력");
     btnPrint.value = x+y;
 }
  btnPrint.onclick = printResult();
 </script>
 <head/>
 ```
- window.onload event를 사용한다.
```javascript
<script>
function printResult() {
    var x,y;
    x = prompt("x값 입력");
    y = prompt("y값 입력");
    btnPrint.value = x+y;
}
function init() {
    btinPrint.onclick = printResult()
}
window.onload = init();
</script>
<head/>
<body>
<input type = "button" value = "출력" id ="btnPrint"/>
```
제일 먼저 생성되는 window 객체는 나머지 코드들이 다 load 되면 init()함수를 호출한다.

그러나 사실 init 함수는 명명할 이유가 없는 함수이며, 

window.onload event를 두 번 이상 사용시에 초기화가 대체하는 문제점이 생긴다.

```javascript
<script>
window.addEventListener("load", function){
  var add = function(x,y){
      return x+y;
};
      x = prompt("x값 입력");
      y = prompt("y값 입력");
      btnPrint.value = x+y;
};

}
```
#객체 id 명명
- html의 경우 

단어와 단어 사이에 -를 삽입하고 모두 소문자를 쓴다. ex) btn-print

- javascript의 경우

두번 째 단어의 조합부터 첫 문자를 대문자로 쓴다. ex) btnPrint

###document.getElementById()
javascript에서는 -를 허용하지 않기 때문에 html에서 선언한 변수 이름을 그대로 사용하게 되면 error가 발생한다. 

이 때, document.getElementById() 함수를 이용하여 html에서 만든 변수를 javascript에서 새로 명명 할 수 있다.

#select element
```javascript
<section id = "sec1">
<li> 번호1 </li>
<li> 번호2 </li>
</section>

<section id = "sec2"> 
<div class="box">
<input class="txt-x" type="text" value = "a"/>
</div>
```
###- getElementsByName(), getElementsByClassName()
```javascript
var list = sec1.getElementById("li")
list[0].textContent = "Hello";
```
### - querySelector(), querySelectorAll()

괄호 안에는 css 문법이 들어간다. class일 경우 '.', id일 경우 '#'을 사용
```javascript
var sec2 = document.getElementById("sec2")
var sec2 = sec2.querySelector(".txt-x");
```
### - childeNodes(), children()
```javascript
var sec2 = document.getElementById("sec2")
var sec2 = sec2.querySelector(".box");
var input = box.childNodes[0];
```
Node라는 것은 comment나 text도 포함하기에 인덱스 번호로 값을 꺼내려고하면 이상한 값이 들어 오는 경우도 있다. 
 
이를 방지하기 위해 태그 형태의 Node들만 갖고 오는 children을 사용한다.

#속성과 스타일 변경
```javascript
img.style["border-color"] = colotInput.value;
img.style.bordrColor = colotInput.value
```
자바스크립트에서 CSS를 문법을 이용하여 속성을 바꿀 수 있다.  

#텍스트 노드
###추가
```javascript
addButton.onclick = function(){
    var txtNode = document.createTextNode(titleInput.value);
    menuListDiv.appendChild(txtNode)
};
```
1. createTextNode로 원하는 값을 넣은 텍스트 노드를 만든다. 

2. appemdChild로 menuListDiv에 차곡차곡 텍스트 노드를 추가시킨다.

###삭제
```javascript
delButton.onclick = function(){
   menuListDiv.removeChild(menuListDiv.childNodes[0]);
};
```
1. 맨 앞에 있는 노드부터 삭제를 하기 위해 childNodes의 인덱스 0번을 가져온다.
2. removeChild로 해당 노드를 삭제한다.


#엘리먼트 노드
###추가
createElement(), append() 사용
```javascript
addButton.onclick = function(){
    var title = titleInput.value;
    var html = '<a href="">'+title+'</a>';
    var li = document.createElement("li");
    li.innerHTML = html;
    menuListUI.append(li);
};

```
###삭제
children, remove() 사용
```javascript
delButton.onclick = function(){
    var liNode = menuListUl.children[0];
    liNode.remove();
};
```

#Node
###cloneNode()
동일한 노드가 다수 필요한 경우 노드를 복제한다.
```javascript
var a = document.getElementByid('a-a')
var a1 = a.cloneNode();
body.appendChild(a1);
```
###insertBefore(), insertAdjacentElement()
insertBefore, insertAdjacentElement의 사용으로 노드를 순회할 수 있다.
```javascript
currentNode.insertBefore(nextNode, currentNode);
currentNode.insertAdjacentElement(nextNode);
```

#event
###target
이벤트에는 target이라는 속성이 존재한다. 
target은 이벤트가 일어난 대상이 무엇인지 알려준다.
```javascript
imgs[0].onclick = function(e) {
    currentImg.src = e.target.src;
};
```
###event bubbling
img-> li-> ul 구조일 때 user는 img를 통해 입력을 하고, 

img에 이벤트가 발생하면 ul까지 이벤트가 전달되게 하는 것을 이벤트 버블링이라고 한다.

반복적으로 이벤트를 처리할 필요 없다는 점에서 큰 장점을 갖는다.

####stopingPropagation()
자식 이벤트만 필요한 상황에서 이벤트 버블링으로 인해 부모 이벤트까지 실행이 될 때,
이벤트 버블링을 멈추게 해야한다.
```javascript
button.onclick = function(e) {
    e.stopPropagation();
};
```

###preventDefault();
이벤트가 발생했을 때 타고 오는 버블링 과정에서 어떠한 element도 기본 행위를 갖지 않게 한다.
```javascript
button.onclick = function(e) {
    e.preventDefault();
};
```