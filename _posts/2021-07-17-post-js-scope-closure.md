# 클로저(Closure)

## Lexical Scoping

```javascript
var name = "MDN";
function init() {
  var name = "Mozilla"; // name은 init에 의해 생성된 지역 변수이다. (또한 비공개 변수)
  function displayName() { // displayName() 은 내부 함수이며, 클로저다.
    console.log(name); // 부모 함수에서 선언된 변수를 사용한다.
  }
  displayName();
}
init();
```

스코프는 함수를 호출할 때가 아니라 선언할 때 생긴다. 함수를 선언하는 순간, 함수 내부의 변수는 자기 스코프로부터 가장 가까운 곳(상위 범위에서)에 있는 변수를 계속 참조하게 된다. displayName함수를 선언할 때, displayName 함수 안의 name은 선언 시 가장 가까운 지역변수 name을 참조하게 된다. 따라서, init함수 안에서 log를 호출해도, 전역변수인 name = 'MDN'를 참조하는 것이 아닌, 전역변수 name = 'Mozilla'가 나오게 된다.

[참고](https://www.zerocho.com/category/JavaScript/post/5741d96d094da4986bc950a0)



## Closure

### 클로저란?

```javascript
function init() {
  var name = "Mozilla"; // name은 init에 의해 생성된 지역 변수이다. (또한 비공개 변수)
  return function() { // displayName() 은 내부 함수이며, 클로저다.
    console.log(name); // 부모 함수에서 선언된 변수를 사용한다.
  }
}
var closure = init();
closure();
```

클로저에 대한 정의가 다양한데, 1) 내부함수가 외부함수의 맥락(context)에 접근할 수 있는 것, 2) 함수와 함수가 선언된 lexical environment의 조합, 3) 비공개 변수를 가질 수 있는 환경에 있는 함수, 4) 함수 내에서 함수를 정의하고 사용하는 것 등으로 정리된다. 

위 MDN 샘플 코드를 보면, init() 내부에 선언된 변수 name을 참조하고 있는 반환 함수가 클로저라 할 수 있다. init() 실행이 끝나, 내부 함수가 리턴되고 나면 지역변수 name에 더이상 접근할 수 없게 될 것으로 예상할 수 있겠지만 그렇지 않다. init()이 실행될 때 내부 함수는 지역변수 name에 대한 참조를 유지한다. 따라서 init()이 호출될 때 지역변수 name은 사용할 수 있는 상태로 남아있는 것이다. 정리하자면, 클로저는 환경을 기억한다. 함수 실행이 끝났다 하여 참조된 변수가 사라지는 것이 아닌, 여전히 제대로 된 값을 반환하고 있는 것을 알 수 있다.

function(){console.log(name)} 은 name 변수나, name 변수가 있는 스코프에 대해 클로저라 부를 수 있다.



```javascript
function counter(count) {
    let _count = count;
    function changeCount(number) {
        _count += number;
    }
    
    return {
        increase: function() {
            changeCount(1);
        },
        decrease: function() {
            changeCount(-1);
        },
        show: function() {
            console.log(_count);
        },
        getCount: function() {
            return _count;
        }
    }
};

const counter1 = counter(10);
const counter2 = counter(100);
counter1.increase();
counter1.increase();
counter1.show();
counter2.show();
```

클로저 관련 유명한 count 예제이다. 이 예제를 통해 알 수 있는 것들을 정리해보자면,

1) 동일한 외부함수 안에서 만들어진 내부함수나 메서드는 외부함수의 지역변수를 공유한다.
2) 외부함수가 실행될 때마다, 새로운 지역변수를 포함하는 클로저가 생성된다.
3) counter의 지역변수 _count는 getCount 메서드와 같은 방법이 제공되지 않을 경우에 어떤 방법으로도 접근이 불가능하다. 즉, 클로저를 통해 은닉화가 가능하다.

추가적으로, 위 예제는 자바스크립트 싱글톤 객체를 구현할 때 자주 사용하는 [Module Pattern](https://addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascript)의 모습이라고 한다.



### 반복문 클로저

### 클로저 성능





참고1) [shiren: 클로저, 그리고 캡슐화와 은닉화](https://blog.shiren.dev/2016-06-27-%ED%81%B4%EB%A1%9C%EC%A0%80,-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%EC%BA%A1%EC%8A%90%ED%99%94%EC%99%80-%EC%9D%80%EB%8B%89%ED%99%)
참고2) [MDN 클로저](https://developer.mozilla.org/ko/docs/Web/JavaScript/Closures)
참고3) [제로초: 실행 컨텍스트](https://www.zerocho.com/category/JavaScript/post/5741d96d094da4986bc950a0)
참고4) [hyunseob: JavaScript 클로저](https://hyunseob.github.io/2016/08/30/javascript-closure/)
참고5) [생활코딩 클로저](https://opentutorials.org/course/743/6544)

