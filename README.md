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

# 참조한 사이트
> https://tailwindcss.com/  
> https://so-so.dev/web/tailwindcss-w-twin-macro-emotion/  
> https://medium.com/@sascha.wolff/utility-first-css-ridiculously-fast-front-end-development-for-almost-every-design-503130d8fefc
