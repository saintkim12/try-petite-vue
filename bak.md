# 들어가기 전에

[##_Image|kage@NBFr2/btrsRQWWOBp/xYgehaZk3tXH7HBkKkjPE1/img.png|CDM|1.3|{"originWidth":405,"originHeight":33,"style":"alignCenter","caption":"wow!"}_##]

-   Vue.js 공식 홈페이지([https://vuejs.org)에서](https://vuejs.org)%EC%97%90%EC%84%9C) 드디어 Vue 3 버전을 기본 버전으로 사용하게 되었다는 알림이 떠 있다.  
    ([관련글](https://blog.vuejs.org/posts/vue-3-as-the-new-default.html))  
    글에 따르면, 2022-02-07부터 기본 버전을 2에서 3이 되었으며, 그에 따른 관련 라이브러리도 3버전을 사용한다는 게 주된 내용이다.
-   이에 따라 기본 docs도 신규 작성된 버전이 올라가 있다.(따라서 한글 버전의 문서는 없다.)

---

-   전 회사에서 Vue(2) 및 vue-cli 기반 프로젝트를 구축/운영했었고, 이번 회사 신규 프로젝트에 Vue 3 및 vite를 도입하였다.  
    작년에(2021-06) 신규 프로젝트 작업 전에 기존 프로젝트(Spring 기반 MVC + jsp + jQuery)를 버전업하는 업무를 했었고, 프로젝트의 Spring을 Spring boot로 전환하는 등 버전업 작업을 진행했다.
-   이 과정에서 프론트엔드 프레임워크를 도입하는 것을 고려했으나,  
    1> 기존 jsp를 전환하는 작업  
    2> STS(이클립스)에 npm 생태계를 집어넣는 작업  
    3> 이클립스에서 javascript 코딩  
    등을 하고 싶지 않았기에 이 작업은 진행하지 않았다.
-   그럼 다음 고려한 사항은 "그럼 서버 템플릿 엔진 환경에서 데이터의 반응성을 처리해주는(React, Vue 같은) 라이브러리는 없을까" 였다.
-   그럼 이때 중요한 것은 1> 학습 레벨이 낮아 누구나 쉽게 사용할 수 있는지 2> 다른 라이브러리에 영향을 끼치지 않거나 보완할 수 있는지, 또는 호환이 잘 되는지 3> 레거시 브라우저에서도 작동하는 데 지장이 없는지 가 된다.
-   이때 조사한 라이브러리 목록을 보면,
    -   [alpine.js](https://alpinejs.dev/) - 아래 설명할 petite-vue와 유사한 느낌이었던 걸로 기억한다.
    -   [sinuous](https://github.com/luwes/sinuous) - Vue와 유사한 문법. Vue로부터 영감을 받았다고 본거 같은데..
    -   [stimulus](https://stimulus.hotwired.dev/) - 겸손한 야망을 가졌다는 게 인상적이다.
-   여러여러 이유로 결국은 이 라이브러리들을 사용하지 못했는데, 결론만 말하면 Vue, React 등 프론트엔드 프레임워크에 익숙해진 나와, jsp, jQuery에 익숙해진 다른 팀원들을 모두 만족시키는 라이브러리는 아니라고 판단했기 때문이다.

---

-   다시 맨 처음으로 돌아가서, 신규 vuejs.org의 문서를 읽다보면 다음 구절이 있다.If you are just looking for enhancing largely static HTML with light interactions, you can also check out petite-vue, a 5kb subset of Vue optimized for progressive enhancement.  
    가벼운 상호 작용으로 주로 정적인 HTML을 향상시키려는 경우 점진적 향상에 최적화된 Vue의 5kb 하위 집합인 petite-vue 도 확인할 수 있습니다.  
    [https://vuejs.org/guide/scaling-up/sfc.html#why-sfc](https://vuejs.org/guide/scaling-up/sfc.html#why-sfc)
-   즉 내가 찾던 라이브러리는 결국 vue 안에 있었던 것이다.(petite-vue 글이 검색되는 시기도 비슷하다 ㅋㅋㅋ)
-   잡설이 길었는데, 요약하면 작년에 해결하지 못한 숙제를 petite-vue가 해결해주길 바라면서 이 글을 작성했다.

# [petite-vue](https://github.com/vuejs/petite-vue)

-   petite-vue is an alternative distribution of Vue optimized for progressive enhancement.  
    (petite-vue는 점진적 향상 에 최적화된 Vue 의 대체 배포판입니다.)
-   (이상 내용은 해당 github 문서에서 인용하였음)
-   결론을 말하면, vue.js의 최소한의 기능만을 담아 기존 프로젝트에 최소한으로 가볍게 적용하거나, 아니면 추후 Vue.js를 적용할 수 있도록 확장해 나갈 수 있는 라이브러리인 듯 하다.
- 그리고 petite-vue는 (vue.js와는 다르게) Virtual DOM이 아니라고 한다.

# Vue.js

\-

# 적용을 고려해볼만한 상황

## 프론트엔드 개발 프레임워크를 적용하기 힘들거나 적용할 수 없는 경우

-   [ ]  서버 템플릿 엔진을 사용하는 경우(== 서버에서 화면에 필요한 값/텍스트 등을 내려줌)
    -   (java라면) **jsp**, thymeleaf 등
-   [ ]  전문 프론트엔드 환경이 갖춰지지 않았고, 갖출 수 없는 경우
    -   Node.js 기반의 빌드형 프론트엔드 프레임워크(webpack 등)를 쓰기 싫거나, 쓸 수 없는 경우
        -   레거시 js 라이브러리 등에 묶여 있거나 등
        -   팀의 프론트엔드 스킬 레벨 등 적용이 바로 불가능한 경우프론트엔드 프레임워크로 Vue.js 등을 써보고 싶은 경우
-   [ ]  이미 완성된 페이지에 [점진적으로](https://developer.mozilla.org/en-US/docs/Glossary/Progressive_Enhancement) Vue.js를 적용하고 싶은 경우
    -   레거시 -> **petite-vue** -> Vue.js (-> vite, vue-sfc 등 프론트엔드 프레임워크로 전환)
-   [ ]  Vue.js를 가볍게 쓰고싶은 경우
    -   살짝 써보는 것 + 진짜 가볍게(~6kb) 쓰는 두 의미 모두 포함
-   [ ]  **그런데도 어찌됐든 Vue.js를 써보고 싶은 경우**

# 사용해보기

## 메시지를 저장하고 화면에 출력하는 화면
(이거 예시 생각하느라 약 1주일 걸림 ㅋㅋ)

### 목표 화면

- 흔한 채팅?프로그램 같은 것
- vue.js 등 프론트엔드 프레임워크를 모른다면 동적인 데이터를 화면에 렌더링하는 (걸 jQuery나 순수 자바스크립트로 했으면 어떤 과정을 통해 했을지 생각해보며) 과정을 살피는 것으로 하며
- vue.js를 알고 있다면, vue.js 일반 버전와 어떻게 다른지 비교하며 살펴보도록 한다.


### 코딩!
1. html 파일을 만든다.(여기서는 input-box.html)
1. html 파일을 브라우저에서 연다(또는 드래그 앤 드롭)
    - Tip
        - 개발툴(IDE)로 VSCode를 사용한다면, Live Server 확장프로그램을 사용할 수 있다.
        - (여기서는 사용하지 않지만) 지금 방식으로는 로컬 파일을 바로 불러올 수 없다.
1. 일반 HTML 템플릿을 작성한다.
    - Tip
        - 개발툴(IDE)로 VSCode를 사용한다면, (html 빈 파일에서) html 입력 후 html:5를 선택하면 기본 템플릿이 작성된다.
        - 브라우저 자동번역이 보기 싫으면 ``<html lang="ko">``로 고치거나 lang 속성을 지운다(``<html>``)
    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
    </head>
    <body>
      
    </body>
    </html>
    ```
1. unpkg의 petite-vue를 include한다.  
  일단은 자동 초기화를 할 것이기 때문에 script 속성으로 ``defer``과 ``init``을 추가한다.
    ```html
    <script src="//unpkg.com/petite-vue" defer init></script>
    ```
1. 기본 css 및 골격을 작성한다 (css에 대한 이해도가 없으면 넘어가거나 그냥 붙여넣어도 좋다)
    ```html
    <link rel="stylesheet" href="//unpkg.com/normalize.css">
    <style>
      * {
        box-sizing: content-box;
      }
      #app {
        width: 100vw;
        height: 100vh;
      }
    </style>
    ```
    ```html
    <body>
      <div id="app">
        <div class="input-wrap">
          <!-- 입력 인풋 및 버튼 -->
        </div>
        <div class="input-log-wrap">
          <!-- 입력 결과 확인 창(chat log) -->
        </div>
      </div>
    </body>
    ```
1. 입력 인풋 및 버튼 컴포넌트를 그린다.
    ```html
    <div class="input-wrap">
      <input type="text" value="입력값" />
      <button>입력</button>
    </div>
    ```
1. 컴포넌트에 petite-vue를 적용하고, input에 값을 연결한다.  
    1. div#app에 ``v-scope`` 속성을 주는 것으로 시작해보자
        ```html
        <div id="app" v-scope>
          ...
        </div>
        ```  
      여기까지 진행해도 전 화면과 차이는 없다. 굳이 한다면 웹 브라우저의 개발자 도구(F12)를 띄워봐서 에러 없는지 확인하는 거 정도?
    2. 다음으로 v-scope에 값을 선언하고 그 값을 input의 value 값으로 줘본다.
        ```html
        <div id="app" v-scope="{ inputText: '초기값' }"><!-- 값은 Javascript Object 형태로 준다. -->
          ...
            <!--
              위에서 선언한 v-scope의 값에 속성을 연결하기 위한 colon(:) 문법 - 정확히는 v-bind:[속성명] - 을 사용하여 값을 지정한다.
              속성의 값은 v-scope에서 사용한 변수명을 전달하면 된다.
            -->
            <input type="text" :value="inputText" />
          ...
        </div>
        ```
        - Tip
            - 값을 화면에 출력해서 제대로 연결되었는지 확인할 수 있다.
                ```html
                <input type="text" :value="inputText" />
                현재 입력값: {{ inputText }}
                ```
       여기까지 진행하면, 기존 초기값('입력값') 대신 v-scope의 inputText로 적용한 초기값('초기값')이 설정 것을 확인할 수 있다.  
       (아직 동기화는 반영하지 않음)
    3. 실시간 입력값이 동기화되도록, 특수 문법인 ``v-model``을 사용한다.
        ```html
        <input type="text" v-model="inputText" />
        ```  
        (간단히 말하면, v-model은 :value + @input(입력 이벤트)을 연결할 때 쓰는 문법이다.)  
        여기까지 진행 시, 값이 실시간으로 반영되는 것을 확인할 수 있다.
1. 입력 버튼 이벤트를 작성한다.
    1. button에 click 이벤트인 ``@click`` 속성을 지정한다.  
       속성값에는 기능을 정의하면 되는데, 일단은 입력값을 빈값으로 초기화하는(바꾸는) 기능을 달아보자.
        ```html
        <!--
          click 이벤트를 정의하기 위해 @ 문법 - 정확히는 v-on:[이벤트명] - 을 사용하여 이벤트를 지정한다.
          속성의 값은 중괄호로 감싸진 함수라고 생각하고 내용을 작성하면 된다. (= 여러 줄은 세미콜론(;)을 사용하면 된다)
          나중에 함수 내용이 길고 복잡해지면 javascript에서 함수를 선언하고 그 함수명을 부르는 방식으로 전환한다.
        -->
        <button @click="inputText = '';">입력</button>
        ```  
        (화면에서 버튼을 클릭하여 입력값이 사라지는지 확인하자.)
    2. 이번에는 입력값을 배열에 저장하는 기능을 덧붙인다.  
       덧붙이기 전, v-scope에 입력값을 저장할 배열을 먼저 선언해준다.
        ```html
        <div id="app" v-scope="{ logList: [], inputText: '초기값' }"><!-- 값은 Javascript Object 형태로 준다. -->
          ...
            <button @click="logList.push(inputText); inputText = '';">입력</button><!-- Array.push를 사용하여 값을 배열 저장한 후, 입력값을 초기화한다. -->
          ...
        </div>
        ```  
        -  Tip
            - 마찬가지로, 배열값을 화면에 출력해서 제대로 연결되었는지 확인할 수 있다.(배열은 자동 문자열 변환됨)
                ```html
                <button @click="logList.push(inputText); inputText = '';">입력</button>
                현재 저장값: {{ logList }}
                ```
1. 배열 ``logList``에 저장된 값을 화면과 연결한다.
    1. 반복 데이터를 위한 문법인 ``v-for``을 사용한다.
        ```html
        <div class="input-log-wrap">
          <!--
            javascript의 for(idx in list) 문법과 유사하게, v-for="(item, idx) in list" 형태로 사용할 수 있다.
            item(첫번째 값)은 배열의 각 항목이며, idx(두번째 값)은 배열에서 항목의 순서(index)이다.
            v-for을 사용할 때 key값은 주는 것이 좋으며, 보통 고유한 id값을 주면 된다.(아래와 같은 배열 index를 사용하는 건 나쁜 예 중에 하나다.)
          -->
          <div v-for="(text, idx) in logList" :key="idx">
            <p>{{ text }}</p>
          </div>
        </div>
        ```  
        이렇게 한 경우 값을 추가할 때마다 값이 ``순서대로`` 출력되는 것을 확인할 수 있다.
1. 배열을 string 구조에서 object 구조로 변경해본다.
    - 단순 텍스트만 출력하는 것 대신 입력 시간을 추가해보기 위해, 데이터 구조를 변경한다.
        - 데이터 구조는 ``{ text: string, timestamp: Date }`` 구조로 한다.
    1. 입력부 변경
        ```html
        <button @click="logList.push({ text: inputText, timestamp: new Date() }); inputText = '';">입력</button>
        <!-- 이제 기존 string 대신 object({ text: string, timestamp: Date }) 구조가 들어간다. -->
        ```
    2. 출력부 변경
        ```html
        <div class="input-log-wrap">
          <div v-for="(log, idx) in logList" :key="idx">
            <p>
              <!-- 기존 string 대신 object 구조로 변경한 값에 맞춰 값을 가져온다. -->
              {{ log.text }}
              <span>{{ log.timestamp }}</span>
            </p>
          </div>
          <!-- 혹시 es6 구조할당분해에 익숙하다면 다음과 같이 해도 좋다. -->
          <!--
          <div v-for="({ text, timestamp }, idx) in logList" :key="idx">
            <p>
              {{ text }}
              <span>{{ timestamp }}</span>
            </p>
          </div>
          -->
        </div>
        ```

### 코딩!(발전)
1. 자동 초기화 대신 Javascript로 초기화하도록 코드를 변경
    ```html
    <!-- defer, init 삭제 -->
    <script src="//unpkg.com/petite-vue"></script>
    ```
    ```html
    <script>
      // 수동으로 petite-vue app을 생성하고 마운트해준다.
      PetiteVue.createApp().mount()
    </script>
    <!-- 혹시 es module 방식에 익숙하다면 -->
    <!--
      <script type="module">
        import { createApp } from 'https://unpkg.com/petite-vue?module'
        createApp().mount()
      </script>
    -->
    ```  
    - 자동 init은 분명 매력적인 기능이지만, 기존 프로젝트에 petite-vue를 적용하는 구조라면, 분명 초기화 타이밍이 이슈가 될것이라고 생각한다.
    - 따라서, 사용자가 올바른 초기화 타이밍에(예> 특정 컴포넌트 ready 후) 초기화를 실시할 수 있다.
1. 이벤트 함수, v-scope 변수를 javascript에서 정의하기
    - html 속성으로 복잡한(두 줄 이상의, 또는 라이브러리 함수가 연관된) 함수를 정의하는 것은 불가능하거나 속성이 복잡해진다.
    - 따라서 함수를 javascript에서 정의하고, 해당 함수명을 호출하는 방식으로 변경한다.
    - 함수 내에서 v-scope의 변수를 사용하기 위해서는 createApp의 파라미터로 값이 선언되어야 하므로 결국 **javascript에서 변수를 선언하도록 변경**하여야 한다.
    ```js
    PetiteVue.createApp({
      // v-scope의 값을 여기서 선언해줘야 함수에서 해당 값을 사용할 수 있다
      logList: [],
      inputText: '초기값',
      
      addLogList: function() { // 기존 인라인 함수 대신 ``addLogList`` 값을 전달한다
        // 기존 v-scope의 값은 여기서 this.* 형태로 사용할 수 있다
        // logList.push({ text: inputText, timestamp: new Date() });
        // inputText = '';
        // console.log(this)
        this.logList.push({ text: this.inputText, timestamp: new Date() })
        this.inputText = ''
      }
    }).mount()
    ```
    ```html
    <div id="app" v-scope><!-- v-scope의 속성 제거(global 속성으로 이용) -->
      ...
        <button @click="addLogList">입력</button><!-- @click에 함수명을 지정 -->
      ...
    </div>
    ```
1. 정의했던 기능들을 함수형 컴포넌트 LogApp으로 만들기
    - 기능을 재사용할 수 있도록 컴포넌트화해본다.
    ```js
    // log-app 기능을 LogApp 컴포넌트(함수형)으로 분리한다
    function LogApp(props) {
      return {
        logList: [],
        inputText: '초기값',
        addLogList: function() {
          this.logList.push({ text: this.inputText, timestamp: new Date() })
          this.inputText = ''
        }
      }
    }
    PetiteVue.createApp({
      // 컴포넌트 자체를 넘긴다
      LogApp
    }).mount()
    ```
    ```html
    <div id="app" v-scope="LogApp()"><!-- 함수형 컴포넌트를 실행하는 형태로 컴포넌트를 초기화한다 -->
    ```
1. 번외> reactive()를 사용하여 this를 대체해본다.
    - 장점: this에 종속되지 않음
        - arrow function 사용 가능 등
        - vue 3 composition api와 유사한 형태로 코드 스타일을 사용할 수 있다.(위의 스타일은 vue 2(option api)와 유사)
    - 단점: 반응형 값 처리를 위해 reacive()로 감싸진 값을 사용해야 함
    ```js
    function LogApp(props) {
      // Vue 3 reactive 기능과 비슷하게, 값이 변경될 경우 자동적으로 vue에서 처리하도록 reactive()로 객체를 감쌀 수 있다
      const state = PetiteVue.reactive({
        logList: [],
        inputText: '초기값',
      })
      return {
        state,
        addLogList: () => { /* this를 사용하지 않으므로 es6 arrow function 사용 가능 */
          // this.* 대신 state.*으로 변경
          state.logList.push({ text: state.inputText, timestamp: new Date() })
          state.inputText = ''
        }
      }
    }
    ```
    ```html
    <input type="text" v-model="state.inputText" /><!-- state로 감싼 형태로 값을 정의했으므로 호출시에도 변경 -->
    <div v-for="(log, idx) in state.logList" :key="idx"><!-- state로 감싼 형태로 값을 정의했으므로 호출시에도 변경 -->
    ```
<!-- ### 추가 미션 -->
<!-- - [ ] 특수 이벤트 ``@vue:mounted``, ``@vue:unmounted`` 사용해보기 -->
<!-- - [ ] template를 사용하도록 기능 변경(inline template 또는 <template id="" /> 형태) -->
<!-- - [ ] 날짜 출력 형태를 변경해보기 -->
<!-- - [ ] 행 삭제 기능 만들기(버튼으로) -->
<!-- - [ ] 전체 삭제 기능 만들기(버튼으로) -->
<!-- - [ ] 조건문(``v-if``, ``v-else``)을 사용하여 짝수행일 경우 글자색을 변경하기   -->
<!-- (위의 행 삭제 기능에 관계없이 홀/짝수행에 따라 출력할 수 있다.) -->

# 사용후기
- 자동완성이 없고, html 속성에 javascript 값을 줘야 하므로 syntax 구분이 힘들다.
- computed의 부재가 크다.
- petite-vue는 vue의 경량판이기도 하지만 확실히 다른 용도로 사용할 수 있을 것으로 생각됨
  (예> 레거시 프로젝트의 특정 부분에만 vue를 적용하는 경우)