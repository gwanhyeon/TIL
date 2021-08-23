jQuery는 수행하는 데 많은 JavaScript 코드 행이 필요한 많은 일반적인 작업을 수행하고 이를 한 줄의 코드로 호출할 수 있는 메서드로 매핑시킵니다.

jQuery는 AJAX 호출 및 DOM 조작과 같은 JavaScript의 복잡한 많은 부분을 단순화합니다.

jQuery 라이브러리에는 다음 기능이 포함되어 있습니다.

- HTML/DOM 조작
- CSS 조작
- HTML 이벤트 메서드
- 효과 및 애니메이션
- AJAX
- 유용

다른 많은 JavaScript 라이브러리가 있지만 jQuery는 아마도 가장 인기 있고 가장 확장성이 뛰어날 것입니다.

```jsx
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
</head>
```

# jQuery Syntax

# selector

기본구문은 $(selector) 이며 다음과 같은 특징을 가지고 있습니다.

- jQuery를 정의/액세스하기 위한 $ 기호
- HTML 요소 를 위한 selector
- 요소에 대해 수행할 jQuery

selector example)

```jsx
$(this).hide() - 현재 요소를 숨깁니다.
$("p").hide() - 모든 <p> 요소를 숨깁니다.
$(".test").hide() - class="test"인 모든 요소를 숨깁니다.
$("#test").hide() - id="test"인 요소를 숨깁니다.
```

### $(document).ready(function(){})

모든 jQuery는 docuemnt 로드전에 코드가 실행되는것을 막기위하여 해당 $(document).ready()에 존재하게 됩니다.

```jsx
$(document).ready(function(){

  // jQuery methods go here...

});
```

만약에, 문서가 완전히 로드되기 전에 메서드가 실행되는 경우 실패할 수 있는 경우의 수는 다음과 같습니다.

- 아직 생성되지 않은 요소를 숨기는 경우
- 아직 로드되지 않은 이미지의 크기를 가져오는 경우

위의 구문은 복잡하기 때문에 jQuery에서는 조금 더 축약된 형태를 제공합니다.

```jsx
$(function(){
  // jQuery methods go here...
});
```

# jQuery Selectors

jQuery Selector는 jQuery라이브러리중 가장 중요한 부분중 하나이며 jQuery Selector를 사용하면 HTML 요소를 선택하고 조작할 수 있습니다.

jQuery 선택기는 이름, ID, 클래스, 유형, 속성, 속성 값 등을 기반으로 HTML 요소를 선택하는 데 사용됩니다. 기존 CSS Selectors를 기반으로 하며 , 일부 고유한 사용자 지정 선택기가 있습니다.

jQuery의 모든 선택자는 달러 기호와 괄호 $()로 시작합니다

### The element Selector

```jsx
$(document).ready(function(){
  $("button").click(function(){
    $("p").hide();
  });
});
```

### The #id Selector

```jsx
$(document).ready(function(){
  $("button").click(function(){
    $("#test").hide();
  });
});
```

### The .class Selector

```jsx
$(document).ready(function(){
  $("button").click(function(){
    $(".test").hide();
  });
});
```

[제목 없음](https://www.notion.so/d8b0deacc6da4b719bc2960381bbec39)

- Selector 예시

```jsx
$("table.tbl_result > thead > tr:first-child").find("input:checkbox").live("click",	function() {
				$("table.tbl_result > tbody > tr input:checkbox").not(":disabled").prop("checked", $(this).is(":checked"));
	});
```

table의 속성의 class이름이 tbl_result의 하위속성인 thead의 하위속성인 tr의 속성의 first-child 첫번재 요소중에 find()함수를 통하여 입력된 태그의 속성값이 input:checkbox인 경우 live()라는 함수를 통하여 이벤트 바인딩을 시켜주는 로직. (제이쿼리 1.7이상부터는 live()함수 대신 통합되는 on()함수를 사용하여 이벤트 바인딩을 시켜줍니다. 리팩토링 여부 필요)

즉, :은 태그의 속성을 뜻하고, .이 들어가면 클래스명을 뜻한다.

# jQuery - Set Content and Attributes

### 콘텐츠 설정 - text(), html() 및 val()

이전 페이지와 동일한 세 가지 방법을 사용하여 **콘텐츠** 를 **설정합니다** .

- `text()`

    - 선택한 요소의 텍스트 내용을 설정하거나 반환합니다.

    - **$(셀렉터).text()**

    셀렉터 하위에 있는 자식 태그들의 문자열만 출력

- `html()`

    - 선택한 요소(HTML 마크업 포함)의 내용을 설정하거나 반환합니다.

- `val()`

    - 양식 필드의 값을 설정하거나 반환합니다.

    - **$(셀렉터).val()**

    input태그에 정의된 value속성의 값을 확인하고자할때 사용

```jsx

$("#btn1").click(function(){
  $("#test1").text("Hello world!");
});
$("#btn2").click(function(){
  $("#test2").html("<b>Hello world!</b>");
});
$("#btn3").click(function(){
  $("#test3").val("Dolly Duck");
});

```

### Set Attributes - attr()

```jsx
- single
$("button").click(function(){
  $("#w3s").attr("href", "https://www.w3schools.com/jquery/");
});

- multi
$("button").click(function(){
  $("#w3s").attr({
    "href" : "https://www.w3schools.com/jquery/",
    "title" : "W3Schools jQuery Tutorial"
  });
});

- Get callback origin value 
$("button").click(function(){
  $("#w3s").attr("href", function(i, origValue){
    return origValue + "/jquery/";
  });
});
```

attr()함수를 사용하여 태그의 속성값을 변경한다. 그리고, 대괄호 {}를 사용하여 다양한 속성의 값을 변경시킬 수도 있다. .또한 콜백을 통하여 변경전 value값을 가져올 수도 있다.

# jQuery - Add Elements

### Add New HTML Content

We will look at four jQuery methods that are used to add new content:

- `append()` - Inserts content at the end of the selected elements
- `prepend()` - Inserts content at the beginning of the selected elements
- `after()` - Inserts content after the selected elements
- `before()` - Inserts content before the selected elements

```jsx
$(document).ready(function(){
  $("#btn1").click(function(){
    $("p").append(" <b>Appended text</b>.");
  });

  $("#btn2").click(function(){
    $("ol").append("<li>Appended item</li>");
  });
});
```

append()함수를 사용하여 뒷 부분에 기존의 텍스트값을 추가시켜줄 수 있다.

prepend()함수를 사용하여 앞 부분에 기존의 텍스트값을 추가시켜줄 수 있다.

응용하여 새로운 태그를 생성하여 추가시켜줄 수 있다.

```jsx
function appendText() {
  var txt1 = "<p>Text.</p>";        // Create text with HTML
  var txt2 = $("<p></p>").text("Text.");  // Create text with jQuery
  var txt3 = document.createElement("p");
  txt3.innerHTML = "Text.";         // Create text with DOM
  $("body").append(txt1, txt2, txt3);   // Append new elements
}
```

# jQuery - Remove Elements

jQuery remove() Method

jQuery remove()메서드는 선택한 요소와 그 자식 요소를 제거합니다.

```jsx
$(document).ready(function(){
  $("button").click(function(){
    $("#div1").remove();
  });
});
```

다음과같이 id값이 div1인값인 태그를 모두 삭제하는 로직

jQuery empty() Method

jQuery empty()메서드는 선택한 요소의 자식 요소를 제거합니다.

```jsx
$(document).ready(function(){
  $("button").click(function(){
    $("#div1").empty();
  });
});
```

응용하면 각각의 요소를 제거 할 수도 있다.

```jsx
$(document).ready(function(){
  $("button").click(function(){
    $("p").remove(".test");
  });
});
```

# jQuery - Get and Set CSS Classes

jQuery에는 CSS 조작을 위한 여러 가지 방법이 있습니다. 다음 방법을 살펴보겠습니다.

스타일속성을 추가하고 삭제할 수 있는 용도. toggle같은경우는 추가,삭제를 모두 한번에 기능으로 처리할 수 있다.

- `addClass()`

    - 선택한 요소에 하나 이상의 클래스를 추가합니다.

- `removeClass()`

    - 선택한 요소에서 하나 이상의 클래스를 제거합니다.

- `toggleClass()`

    - 선택한 요소에서 클래스 추가/제거 사이를 전환합니다.

- `css()`

    - 스타일 속성을 설정하거나 반환

### jQuery addClass() Method

```jsx
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script>
$(document).ready(function(){
  $("button").click(function(){
    $("h1, h2, p").addClass("blue");
    $("div").addClass("important");
  });
});
</script>
<style>
.important {
  font-weight: bold;
  font-size: xx-large;
}

.blue {
  color: blue;
}
</style>
</head>
<body>

<h1>Heading 1</h1>
<h2>Heading 2</h2>

<p>This is a paragraph.</p>
<p>This is another paragraph.</p>

<div>This is some important text!</div><br>

<button>Add classes to elements</button>

</body>
</html>
```

### jQuery removeClass() Method

```jsx
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script>
$(document).ready(function(){
  $("button").click(function(){
    $("h1, h2, p").removeClass("blue");
  });
});
</script>
<style>
.blue {
  color: blue;
}
</style>
</head>
<body>

<h1 class="blue">Heading 1</h1>
<h2 class="blue">Heading 2</h2>

<p class="blue">This is a paragraph.</p>
<p>This is another paragraph.</p>

<button>Remove class from elements</button>

</body>
</html>
```

### jQuery toggleClass() Method

```jsx
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script>
$(document).ready(function(){
  $("button").click(function(){
    $("h1, h2, p").toggleClass("blue");
  });
});
</script>
<style>
.blue {
  color: blue;
}
</style>
</head>
<body>

<h1>Heading 1</h1>
<h2>Heading 2</h2>

<p>This is a paragraph.</p>
<p>This is another paragraph.</p>

<button>Toggle class</button>

</body>
</html>
```

# jQuery - css() Method

Return a CSS Property

```jsx
$(document).ready(function(){
  $("button").click(function(){
    alert("Background color = " + $("p").css("background-color"));
  });
});
```

Set a CSS Property

```jsx
$(document).ready(function(){
  $("button").click(function(){
    $("p").css("background-color", "yellow");
  });
});
```

# jQuery - Dimensions

- `width()`
- `height()`
- `innerWidth()`
- `innerHeight()`
- `outerWidth()`
- `outerHeight()`

```jsx
$("button").click(function(){
  var txt = "";
  txt += "Width: " + $("#div1").width() + "</br>";
  txt += "Height: " + $("#div1").height();
  $("#div1").html(txt);
});
```

# jQuery Traversing

"이동"을 의미하는 jQuery 순회는 다른 요소와의 관계를 기반으로 HTML 요소를 "찾거나" 선택하는 데 사용됩니다. 하나의 선택으로 시작하여 원하는 요소에 도달할 때까지 해당 선택을 통해 이동합니다.

아래 이미지는 HTML 페이지를 트리(DOM 트리)로 나타낸 것입니다. jQuery 순회를 사용하면 선택한(현재) 요소에서 시작하여 트리에서 위로(상위), 아래(하위) 및 옆으로(형제) 쉽게 이동할 수 있습니다. 이 움직임을 DOM 트리를 가로지르는 것 또는 통과하는 것을 말합니다.

![https://www.w3schools.com/jquery/img_travtree.png](https://www.w3schools.com/jquery/img_travtree.png)

```jsx
<div> 요소는 <ul> 의 부모 이며, 그 안에 있는 모든 것의 조상 입니다.
<ul> 요소는 두 <li> 요소 의 상위 요소이고 <div> 요소의 하위 요소입니다.
왼쪽 <LI> 요소이다 부모 <SPAN>의 자식 <UL>과의 자손 <div>의
의 <SPAN> 요소는 인 아이 왼쪽 <LI>과의 자손 <UL> 및 <div>의
두 개의 <li> 요소는 형제입니다 (같은 부모를 공유합니다).
오른쪽 <LI> 요소 인 부모 의 <B>, 아이 <UL>과의 자손 <div>의
의 <b> 요소는 인 아이 오른쪽 <LI>과의 자손 <UL> 및 <div>의
```

### jQuery Traversing - Ancestors

Three useful jQuery methods for traversing up the DOM tree are:

- `parent()`

```jsx
$(document).ready(function(){
	$("span").parent();
});
```

- `parents()`

```jsx
$(document).ready(function(){
  $("span").parents("ul");
});
```

- `parentsUntil()`

```jsx
$(document).ready(function(){
  $("span").parentsUntil("div");
});
```

# jQuery Traversing - Descendants

DOM 트리를 탐색하는 데 유용한 두 가지 jQuery 메서드는 다음과 같습니다.

- `children()`
- `find()`

### jQuery children() 메서드

이 `children()`메서드는 선택한 요소의 모든 직계 자식을 반환합니다.

이 메서드는 DOM 트리 아래의 단일 수준만 탐색합니다.

```jsx
$(document).ready(function(){
  $("div").children("p.first");
});
```

### jQuery find() 메서드

`ind()`메서드는 마지막 하위 항목까지 선택한 요소의 하위 요소를 반환합니다.

다음 예 `<span>`에서는 의 하위 항목인 모든 요소를 반환합니다 `<div>`.

```jsx
<script>
$(document).ready(function(){
	$("div").find("span").css({"color":"red", "border" : 2px solid red"});
});
</script>
```

# jQuery Traversing - Siblings

## DOM 트리에서 옆으로 순회하기

DOM 트리에서 옆으로 탐색하는 데 유용한 jQuery 메서드가 많이 있습니다.

- `siblings()`
- `next()`
- `nextAll()`
- `nextUntil()`
- `prev()`
- `prevAll()`
- `prevUntil()`

### jQuery siblings() Method

이 siblings()메서드는 선택한 요소의 모든 형제 요소를 반환합니다.

```jsx

$(document).ready(function(){
  $("h2").siblings();
});

$(document).ready(function(){
  $("h2").siblings("p");
});
```

### jQuery next() Method

```jsx
$(document).ready(function(){
  $("h2").next();
});

```

이 `next()`메서드는 선택한 요소의 다음 형제 요소를 반환합니다.

다음 예제는 의 다음 형제를 반환합니다 `<h2>`.

### jQuery nextAll() 메서드

이 nextAll()메서드는 선택한 요소의 다음 형제 요소를 모두 반환합니다.

```jsx
$(document).ready(function(){
  $("h2").nextAll();
});
```

### jQuery nextUntil() 메서드

이 nextUntil()메서드는 주어진 두 인수 사이의 모든 다음 형제 요소를 반환합니다.

```jsx
$(document).ready(function(){
  $("h2").nextUntil("h6");
});
```

# jQuery 순회 - 필터링

# first(), last(), eq(), filter() 및 not() 메서드

가장 기본적인 필터링 방법은 `first()`, `last()`및 이며 `eq()`, 이를 통해 요소 그룹에서의 위치에 따라 특정 요소를 선택할 수 있습니다.

다른 필터링 방법은, 같은 `filter()`과 `not()`당신이 일치하는 요소를 선택할 수있게하거나, 특정 기준과 일치하지 않습니다.

### jQuery first() 메서드

first()메소드는 지정된 요소의 첫 번째 요소를 반환한다.

```jsx
$(document).ready(function(){
  $("div").first().css("background-color", "yellow");
});
```

### jQuery last() 메서드

last()메소드는 지정된 요소의 마지막 요소를 반환합니다.

```jsx

$(document).ready(function(){
  $("div").last();
});
```

# jQuery eq() 메서드

이 `eq()`메서드는 선택한 요소의 특정 인덱스 번호가 있는 요소를 반환합니다.

색인 번호는 0에서 시작하므로 첫 번째 요소의 색인 번호는 1이 아니라 0입니다. 다음 예에서는 두 번째 `<p>`요소(인덱스 번호 1) 를 선택합니다 .

```jsx
$(document).ready(function(){
  $("p").eq(1).css("background-color", "yellow");
});
```

# jQuery filter() 메서드

이 `filter()`방법을 사용하면 기준을 지정할 수 있습니다. 기준과 일치하지 않는 요소는 선택에서 제거되고 일치하는 요소가 반환됩니다.

다음 예제는 `<p>`클래스 이름이 "intro"인 모든 요소 를 반환합니다 .

```jsx
<script>
$(document).ready(function(){
  $("p").filter(".intro").css("background-color", "yellow");
});
</script>
```

# jQuery not() 메서드

이 `not()`메서드는 기준과 일치하지 않는 모든 요소를 반환합니다.

**팁 :**`not()` 방법은 반대입니다 `filter()`.

다음 예제 `<p>`에서는 클래스 이름 "intro"가 없는 모든 요소를 반환합니다 .

```jsx
<script>
$(document).ready(function(){
  $("p").not(".intro").css("background-color", "yellow");
});
</script>
```

# jQuery - AJAX load() 메서드

# jQuery load() 메서드

jQuery `load()`메서드는 간단하지만 강력한 AJAX 메서드입니다.

이 `load()`메서드는 서버에서 데이터를 로드하고 반환된 데이터를 선택한 요소에 넣습니다.

**통사론:**

`$(selector).load(URL,data,callback);`

필수 URL 매개변수는 로드하려는 URL을 지정합니다.

선택적 데이터 매개변수는 요청과 함께 보낼 쿼리 문자열 키/값 쌍 세트를 지정합니다.

선택적 콜백 매개변수는 `load()`메소드가 완료된 후 실행할 함수의 이름입니다 .

```jsx
<script>
$(document).ready(function(){
  $("button").click(function(){
    $("#div1").load("demo_test.txt");
  });
});
</script>
```

선택적 콜백 매개변수는 `load()`메소드가 완료 될 때 실행할 콜백 함수를 지정합니다 . 콜백 함수는 다른 매개변수를 가질 수 있습니다.

- `responseTxt`

    - 호출이 성공하면 결과 콘텐츠를 포함합니다.

- `statusTxt`

    - 통화 상태를 포함합니다.

- `xhr`

    - XMLHttpRequest 객체를 포함

다음 예제에서는 load() 메서드가 완료된 후 경고 상자를 표시합니다. 는 IF `load()`방법이 성공했다, 그것은! "외부 콘텐츠가 성공적으로로드"표시하고 실패 할 경우 오류 메시지가 표시됩니다 :

# jQuery - AJAX get() 및 post() 메서드

### HTTP 요청: GET, POST

클라이언트와 서버 간의 요청-응답에 일반적으로 사용되는 두 가지 방법은 GET 및 POST입니다.

- **GET**

    - 지정된 리소스에서 데이터를 요청합니다.

- **POST**

    - 처리할 데이터를 지정된 리소스에 제출합니다.

GET은 기본적으로 서버에서 일부 데이터를 가져오기(검색)하는 데 사용됩니다. **참고:** GET 메서드는 캐시된 데이터를 반환할 수 있습니다.

POST를 사용하여 서버에서 일부 데이터를 가져올 수도 있습니다. 그러나 POST 메서드는 데이터를 캐시하지 않으며 요청과 함께 데이터를 보내는 데 자주 사용됩니다.

### jQuery $.get() 메서드

이 `$.get()`메서드는 HTTP GET 요청으로 서버에서 데이터를 요청합니다.

**통사론:**

$.get(URL,callback);

필수 URL 매개변수는 요청하려는 URL을 지정합니다.

선택적 콜백 매개변수는 요청이 성공하면 실행할 함수의 이름입니다.

다음 예제에서는 `$.get()`메서드를 사용 하여 서버의 파일에서 데이터를 검색합니다.

```jsx
$("button").click(function(){
  $.get("demo_test.asp", function(data, status){
    alert("Data: " + data + "\nStatus: " + status);
  });
});
```

### jQuery $.post() 메서드

이 `$.post()`메서드는 HTTP POST 요청을 사용하여 서버에서 데이터를 요청합니다.

$.post(URL,data,callback);

필수 URL 매개변수는 요청하려는 URL을 지정합니다.

선택적 데이터 매개변수는 요청과 함께 보낼 일부 데이터를 지정합니다.

선택적 콜백 매개변수는 요청이 성공하면 실행할 함수의 이름입니다.

다음 예제에서는 이 `$.post()`메서드를 사용 하여 요청과 함께 일부 데이터를 보냅니다.

```jsx
$("button").click(function(){
  $.post("demo_test_post.asp",
  {
    name: "Donald Duck",
    city: "Duckburg"
  },
  function(data, status){
    alert("Data: " + data + "\nStatus: " + status);
  });
});
```

# jQuery - noConflict() 메서드

### jQuery 및 기타 JavaScript 프레임워크

이미 알고 있듯이; jQuery는 `$`기호를 jQuery의 바로 가기로 사용합니다 .

Angular, Backbone, Ember, Knockout 등과 같은 널리 사용되는 JavaScript 프레임워크가 많이 있습니다.

**다른 JavaScript 프레임워크에서도 $ 기호를 바로 가기로 사용하면 어떻게 될까요?**

두 개의 다른 프레임워크가 동일한 바로 가기를 사용하는 경우 그 중 하나가 작동을 멈출 수 있습니다.

jQuery 팀은 이미 이에 대해 생각하고 `noConflict()`메서드를 구현했습니다 .

이 `noConflict()`메서드는 다른 스크립트에서 사용할 수 있도록 $ 바로 가기 식별자에 대한 보류를 해제합니다.

물론 바로 가기 대신 전체 이름을 쓰기만 하면 jQuery를 계속 사용할 수 있습니다.

```jsx
var jq = $.noConflict();
jq(document).ready(function(){
  jq("button").click(function(){
    jq("p").text("jQuery is still working!");
  });
});
```