# tailwind css 연구 프로젝트
tailwindcss 세팅 방법은 다음을 참조.  
참고로, next.js에서 제공하는 예제 repo내용과 같으므로 다음 사이트의 도큐먼트만 참조해도 상관없음.
> https://tailwindcss.com/docs/guides/nextjs

# 특징
### Utility-First Fundamentals
https://tailwindcss.com/docs/utility-first

부트스트랩과 비슷한 방식으로 tailwindcss에서 제공하는 정의된 css를 유틸처럼 불러와서 적용하면 된다.  
MUI를 사용했을 때를 생각해보면, `margin`, `padding` 등의 개념을 가져와서 쓰는 형태로 적용하면 끝난다.  
하나의 예로 기존의 CSS 적용 방식은 다음과 같다.
```html
<div style="max-width: 24rem; margin: 0 auto;">
    hello
</div>
```
위와 같이 일일이 적용했다면, tailwindcss에서는 Utility-First. 즉, 부트스트랩 쓸 때와 유사하다.
```html
<div class="max-w-sm mx-auto">
    hello
</div>
```
위와 같이 하면 `max-width`, `margin` 스타일이 먹힌 것이다. 스타일이 정의된 클래스를 꺼내와서 적용하면 된다.  
이전 회사에서 디자이너 분들이 미리 정의했던 CSS파일을 꺼내와서 적용했던 것도 생각이 나긴 한다.

또한, 프로젝트 규모가 커질수록 큰 CSS파일로 관리하는 것보단 Utility-First 방식이 관리하기 더 쉽다는 것이다.  
tailwind css에서 자랑하는 부분이기도 하다.  
성공 사례로 깃헙, 넷플릭스, 히로쿠, 등등의 사이트를 예시로든다.

규칙에 적응하느라 시간이 좀 걸리겠지만, `margin`, `padding` 같은 경우는 다음의 규칙을 따른다.  
`.{property}{side}-{size}`  
다음과 같은 예로 말이다.
- `.mt-5` for margin-top: 3rem 
- `.pb-3` for padding-bottom: 1rem 
- `.px-2` for padding-left and padding-right: 0.5rem

### Handling Hover, Focus, and Other States
https://tailwindcss.com/docs/hover-focus-and-other-states

tailwindcss의 모든 유틸리티 클래스는 조건을 줘서 상황에 따른 클래스를 적용할 수도 있다.  
하나의 예로 `bg-sky-700`색깔을 `hover`됐을 때 적용하고 싶다면 `hover:bg-sky-700`과 같이 적용할 수 있다.  
tailwindcss에선 또한, 개발자가 필요한 모든 것이 있으니 필요할 때 사용하면 된다는 것이다.
- *Pseudo-classes*, like `:hover`, `:focus`, `:first-child`, and `:required`
- *Pseudo-elements*, like `::before`, `::after`, `::placeholder`, and `::selection`
- *Media queries*, like responsive breakpoints, dark mode, and `prefers-reduced-motion`
- *Attribute selectors*, like `[dir="rtl"]` and `[open]`

모든 항목은 다음에서 확인할 수 있다.
> https://tailwindcss.com/docs/hover-focus-and-other-states#quick-reference

또한, 그룹마다 차별화를 둘 수도 있고, 형제(sibling) 상태에 따라 스타일을 `peer` 키워드를 이용해서 적용할 수 있으니 유용하다.
> https://tailwindcss.com/docs/hover-focus-and-other-states#styling-based-on-sibling-state  
> https://tailwindcss.com/docs/hover-focus-and-other-states#differentiating-peers  
> https://tailwindcss.com/docs/hover-focus-and-other-states#arbitrary-peers

처음 소개한대로 진짜 웬만한 건 다 지원하는 것 같다.  
RTL, details 태그 의 이벤트(`open`, `close`), 그 외에도 모든 부분에 대해서 한정지어서 적용할 수 있다.  
개발하다가 이거 지원할 거 같은데? 라는 생각이 들면 해당 부분을 봐야 겠다.

### Responsive Design
https://tailwindcss.com/docs/responsive-design

tailwindcss는 기기마다 사이즈에 대한 중단점이 있으므로 복잡하게 설정해서 적용할 필요가 없다고한다.  
중단점이란 다음을 의미한다.
- sm: 640px
- md: 768px
- lg: 1024px
- xl: 1280px
- 2xl: 1536px

특정 중단점에서만 적용하려면 다음과 같이 하면 된다.
```html
<!-- Width of 16 by default, 32 on medium screens, and 48 on large screens -->
<img class="w-16 md:w-32 lg:w-48" src="...">
```

모바일을 신경쓴다면, 모바일 타겟을 먼저 신경쓰도록 한다.
```html
<!-- This will center text on mobile, and left align it on screens 640px and wider -->
<div class="text-center sm:text-left"></div>
```

### Dark mode
https://tailwindcss.com/docs/dark-mode

tailwindcss를 사용하면 drakmode를 쉽게 적용할 수 있다고한다.

html의 class 목록에 `dark`가 있는 것을 보고 `dark 접근자`를 이용하여 색깔을 구분지어서 적용할 수 있는 것이다.  
다크모드를 수동으로 지원할 땐 모드를 `media`로 바꿔주면 된다. 원한다면 클래스 이름을 바꿀 수도 있음.

### Reusing Styles
https://tailwindcss.com/docs/reusing-styles

tailwindcss는 utility class를 가져가서 사용하는데, 다음 HTML 코드와 같이 같은 클래스를 여러번 사용하는 현상이 생길 수 있다.
```html
  <div class="mt-3 flex -space-x-2 overflow-hidden">
    <img class="inline-block h-12 w-12 rounded-full ring-2 ring-white" src="" alt=""/>
    <img class="inline-block h-12 w-12 rounded-full ring-2 ring-white" src="" alt=""/>
    <img class="inline-block h-12 w-12 rounded-full ring-2 ring-white" src="" alt=""/>
    <img class="inline-block h-12 w-12 rounded-full ring-2 ring-white" src="" alt=""/>
    <img class="inline-block h-12 w-12 rounded-full ring-2 ring-white" src="" alt=""/>
  </div>
```
별다른 특별한 방안을 제시하지는 않고, loop, map같은 기능을 사용하라고 권장하며, 별개의 컴포넌트로 관리하라고도 권장한다.  
tailwindcss에선 위의 방법이 권장되지만, `@apply`를 쓰면 custom CSS class로 따로 빼내어 관리할 수 있다.
```css
@layer components {
  .btn-primary {
    @apply py-2 px-4 bg-blue-500 text-white font-semibold rounded-lg shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75;
  }
}
```
그러나 권장하지는 않는다. 여기저기 파편화되어 있는 CSS파일은 오히려 더 더러워 보인다고 강조한다.

### Adding Custom Styles
https://tailwindcss.com/docs/adding-custom-styles

tailwindcss는 확장 가능하도록 설계되어 있다. 플러그인으로 custom CSS를 추가할 수 있는 것이다.  
중단점, 색상, 폰트, 등등을 변경하려면 tailwind.config.js파일에 추가하면 된다.  

사용자 정의 CSS를 추가할 때는 `@layer` directive를 사용하여 추가를 권장한다. `@layer`에는 `base`, `components`, `utilities` 이렇게 총 3가지가 있다.  
이렇게 나누는 이유는 동일한 프로퍼티를 적용하게 되면 어떤 선을 먹일지 우선순위를 결정한다고 보면된다.  
css 파일이 다음과 같이 있고,
```css
.btn {
  background: blue;
  /* ... */
}

.bg-black {
  background: black;
}
```
다음과 같이 두 버튼에 같은 클래스를 먹였다면, 먹인 순서에 상관없이 `.bg-black`이 css파일 뒤에 있으므로 검은색이 된다.
```html
<button class="btn bg-black">...</button>
<button class="bg-black btn">...</button>
```
그래서 layer로 나누는 것이다.
- `base` layer: 재설정/정규화된 기본 스타일 및 `--tw-xxx` css 변수를 정의한다. tailwindcss에서 기본 스타일을 HTML elements에 적용할 때 사용한 것이다.  
  https://play.tailwindcss.com/YpShH9YUHX?file=css 사이트에서 GeneratedCSS 탭을 눌러 Base layer를 확인할 수 있다.
- `components` layer: 기본적으로 비어있다. 개발자들이 추가하고 싶은 것을 추가하면서 사용할 수 있다. 가장 많이 건드릴듯하다.  
  ex) `.btn`, `.card`, ...
- `utilities` layer: 단일 목적 클래스. 즉, 하나의 스타일을 변경할 때만 권장한다. ex) `text-gray-900`, `font-bold`, ...

css파일을 여러개로 관리할 경우, tailwind가 작업에 들어가기 전에 하나의 파일로 결합해야 한다.  
가장 쉬운 방법은 [postcss-import](https://github.com/postcss/postcss-import)을 사용하는 것이다.  
`postcss.config.js`파일에 다음과 같이 플러그인을 추가하고 사용하면 된다.
```javascript
module.exports = {
  plugins: {
    'postcss-import': {},
    tailwindcss: {},
    autoprefixer: {},
  }
}
```

### Functions & Directives
https://tailwindcss.com/docs/functions-and-directives

tailwindcss에서 제공하는 css에서 사용할 수 있는 디렉티브와 함수를 설명해놓은 곳이다.

함수는 다음 두 가지를 제공한다.   
첫번 째로,  
`theme()` 함수는 tailwind의 config 설정값을 가져와서 사용할 수 있게 한다. 대괄호 접근자도 사용 가능하다.
```css
.content-area {
  height: calc(100vh - theme(spacing.12));
}
.content-area {
  height: calc(100vh - theme(spacing[2.5]));
}
```
`screen()` 함수는 
미디어 쿼리를 작성할 때 중단점(sm, xl, ...)을 선택할 수 있게 하는 도구다.
```css
@media screen(sm) {
  /* ... */
}
```


# 참조한 사이트
> https://tailwindcss.com/  
> https://so-so.dev/web/tailwindcss-w-twin-macro-emotion/  
> https://medium.com/@sascha.wolff/utility-first-css-ridiculously-fast-front-end-development-for-almost-every-design-503130d8fefc  
> https://bloggie.io/@kinopyo/organize-your-css-in-the-tailwind-style-with-layer-directive
