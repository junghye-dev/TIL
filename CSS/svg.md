# SVG 속성들

## **`stroke-dasharray`**

-   선을 대쉬 형태로 만들어줍니다.
-   dash 크기, gap 크기 순서대로 값을 사용하면 됩니다.

[MDN의 예제](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/stroke-dasharray)로 한번 알아볼까요?

See the Pen [SVG\_stroke-dasharray](https://codepen.io/junghye-dev/pen/QWdoygq) by junghye-dev ([@junghye-dev](https://codepen.io/junghye-dev)) on [CodePen](https://codepen.io).

<script src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script><script src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

다른건 알겠는데, 4번이 조금 헷갈리죠?

어떻게 된건지 자세히 볼까요?

[##_Image|kage@efKIiy/btq3t4znP3o/qd6F0anBLwcjlvGzzRXwBk/img.png|widthContent|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|||_##]

말 그대로, 적은 숫자 패턴 그대로 반복됩니다.

> **_dash(4) - gap(1) - dash(2) - gap(4) - dash(1) - gap(2) ..._**

이렇게요!  
무조건 홀수번째는 dash 값, 짝수번째는 gap 값이라고 생각하면 안되겠습니다.

## **`stroke-dashoffset`**

MDN에서는 'dash array 렌더링의 오프셋을 정의하는 속성'이라고 말하고 있는데요.

여기서 오프셋(offset)이란 무엇일까요? [위키백과](https://ko.wikipedia.org/wiki/%EC%98%A4%ED%94%84%EC%85%8B_(%EC%BB%B4%ED%93%A8%ED%84%B0_%EA%B3%BC%ED%95%99))는 이렇게 설명하고 있습니다.

> 일반적으로 동일 오브젝트 안에서 오브젝트 처음부터 주어진 요소나 지점까지의 변위차를 나타내는 정수형

뭔가 **시작 지점으로부터 얼만큼 떨어져있는지?** 생각해보면 될 것 같은데요. 정리해보자면,

-   stroke-dasharray 값으로 점선이 그려질 때, 그 점선이 어디서부터 시작할지 그 지점을 설정합니다. (dash array 계산의 시작 지점을 정한다)
-   그러므로, stroke-dasharray 값이 지정되어 있어야 합니다.

이번에도 [MDN의 예제](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/stroke-dashoffset)로 한번 알아보겠습니다.

See the Pen [SVG\_stroke-dashoffset](https://codepen.io/junghye-dev/pen/LYxaNZZ) by junghye-dev ([@junghye-dev](https://codepen.io/junghye-dev)) on [CodePen](https://codepen.io).

<script src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

이번엔 3번부터 헷갈리기 시작합니다. 자세히 볼까요?

### **3번**

-   dash array 계산이 3 user units 만큼 당겨졌습니다. (is pulled)
-   dash 값이 3, gap 값이 1인 상태에서, dash offset 값을 3만큼 주자 dash 3이 빠지고, gap 1부터 시작하게 되었습니다.
-   마치 3만큼 점선을 왼쪽으로 당긴 후 렌더링하기 시작한 느낌입니다.

> **dash offset 값이 양수인 경우?**  
> 원래 시작부터 3만큼 **앞으로(오른쪽으로)** 간 뒤 dash를 그리기 시작합니다.

4번은 음수이니, 반대로 생각하면 됩니다.

### **4번**

-   dash array 계산이 3만큼 밀어졌다. (is pushed)
-   dash 값이 3, gap 값이 1인 상태에서, dash offset 값을 -3만큼 주자 gap 1이 빠지고, dash 3에서 2만큼 없어진 dash 1이 보이는 지점부터 시작하게 되었습니다.
-   마치 3만큼 점선을 오른쪽으로 민 후 렌더링하기 시작한 것 같습니다.  

> **dash offset 값이 음수인 경우?**  
> 원래 시작부터 3만큼 **뒤로 (왼쪽으로)** 간 뒤 dash를 그리기 시작합니다.