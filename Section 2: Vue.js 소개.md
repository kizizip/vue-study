# Vue는 무엇인가?

- MVVM 패턴의 뷰모델 레이어에 해당하는 화면(View)단 라이브러리
<img width="1600" height="850" alt="mvvm" src="https://github.com/user-attachments/assets/cba9b426-ef87-46c6-a15e-ff4f79bdbaeb" />


---

### Reactivity 구현

<details>
  
<summary>
  코드 보기
</summary>

   ```jsx
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app"></div>

    <script>
        var div = document.querySelector('#app');
        var viewModel = {};

        // Object.defineProperty(대상 객체, 객체의 속성, {
        //     // 정의할 내용 
        // })
        // -> 객체의 동작을 재정의하는 메서드.
        // 참고 사이트: https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty
        
        Object.defineProperty(viewModel, 'str', {
            // 속성에 접근했을 때의 동작 정의
            get: function() {
                console.log('접근');
            }, 
            // 속성에 값을 할당했을 때의 동작 정의
            set: function(newValue) {
                console.log('할당', newValue);
                div.innerHTML = newValue;
            }
        })

    </script>
</body>
</html>
```
</details>
    
    
    
- Vue에서의 **reactivity**란, 데이터의 변화가 자동으로 DOM에 반영되어 UI가 동기화되는 시스템이다.

---

### Reactivity 코드 라이브러리화 하기

<details>
  
<summary>
  코드 보기
</summary>

```jsx
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app"></div>

    <script>
        var div = document.querySelector('#app');
        var viewModel = {};

        // IIFE(즉시 실행 함수 표현): 전역 이름공간을 오염시키는 것을 방지 위함
        // 정의하자마자 실행되게끔 해서 다른 곳에서 쓰이지 않게 한다.
        (function() {

            function init() {
                Object.defineProperty(viewModel, 'str', {
                    // 속성에 접근했을 때의 동작 정의
                    get: function () {
                        console.log('접근');
                    },
                    // 속성에 값을 할당했을 때의 동작 정의
                    set: function (newValue) {
                        console.log('할당', newValue);
                        div.innerHTML = newValue;
                    }
                })
            }

            function render(value) {
                div.innerHTML = value;
            }

            init();

        })();
        
    </script>
</body>
</html>
```

</details>

- Reactivity에서의 예제와 마찬가지로 콘솔에서 viewModel.str에 접근하거나, 값을 할당하는 등의 동작을 시험해 볼 수 있다.
  
<details>
  <summary>+ 함수 리터럴 (Functional Literal)</summary>

  **구성 요소:**
    
    1. 예약어 function (필수)
    2. 함수 이름 (선택)
    3. 매개변수 집합 (필수)
    4. 함수 본문 (필수)
    
    → 위와 같은 함수 리터럴 표현식을 통해 즉시 실행 함수를 정의할 수 있는 것이다.
</details>

    

---

### Hello Vue.js와 개발자 도구

<img width="1249" height="679" alt="%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202025-11-11%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2011 55 49" src="https://github.com/user-attachments/assets/56f66c2e-61c1-4585-be2c-7cb2d518c9b9" />


- 확장 프로그램에서 Vue Devtools를 설치 및 실행시, 개발자 도구에서 `Vue 탭` 확인 가능.
- 캡쳐는 `Component`를 볼 수 있는 화면이고, 하단의 data에서 message를 수정할 수 있다 → 즉시 화면 반영

