# 4. 변수와 스코프, 메모리

## 4.1 원시 값과 참조 값

원시 타입: undefined, Null, Boolean, String, Number

참조 타입: 원시 타입을 제외한 나머지, 객체



### 4.1.2 값 복사

원시 값을 다른 변수로 복사할 때, 현재 저장된 값을 새로 생성한 다음 새로운 변수에 복사한다.

```javascript
let num1 = 5;
let num2 = num1;
num1 = 10;
console.log(num2);
```



참조 값을 변수에서 다른 변수로 복사하면 원래 변수에 들어있던 값이 변수에 복사되기는 마찬가지이나, 그 값이 객체 자체가 아닌 힙에 저장된 객체를 가리키는 포인터라는 차이점이 있다.

```javascript
let obj1 = new Object();
let obj2 = obj1;
obj1.name = "kim";
console.log(obj2.name);
```

[참고](https://velog.io/@nomadhash/Java-Script-%EA%B9%8A%EC%9D%80-%EB%B3%B5%EC%82%AC%EC%99%80-%EC%96%95%EC%9D%80-%EB%B3%B5%EC%82%AC)



### 4.1.3 매개변수 전달

ECMAScript의 함수 매개변수는 모두 값으로 전달된다.

```javascript
function addTen(num){
    num += 10;
    return num;
}
let count = 20;
let result = addTen(count);
count;
result;


function setName(obj){
    obj.name = "kim";
}
let person = new Object();
person.name = "lee";
setName(person);
person.name;


function setName(obj){
    obj.name = "kim";
    obj = new Object();
    obj.name = "lee";
}
let person = new Object();
setName(person);
person.name;
```

함수 내부에서 obj와 person이 모두 같은 객체를 가르킨다. 결과적으로 obj는 함수에 값 형태로 전달되었지만, 참조를 통해 객체에 접근한다. obj가 가르키는 것이 힙에 존재하는 전역 객체이다.





### 참고

[깊은 복사, 얕은 복사](https://velog.io/@recordboy/JavaScript-%EC%96%95%EC%9D%80-%EB%B3%B5%EC%82%ACShallow-Copy%EC%99%80-%EA%B9%8A%EC%9D%80-%EB%B3%B5%EC%82%ACDeep-Copy)

