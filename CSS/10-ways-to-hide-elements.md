# 10 Ways to Hide Elements in CSS
![https://www.sitepoint.com/hide-elements-in-css/](https://www.sitepoint.com/hide-elements-in-css/)

1. `opacity`나 `filter: opacity()`
   - IE는 `opacity` 0 에서 1만 지원

2. `color`나 `background-color` Alpha Transparency
   - IE는 `transparent`와 `rgba`만 지원

3. `transform`의 `scale(0)`나 `translate(-999px, 0px)`

4. `clip-path: circle(0)`
   - modern browsers에서만 가능

5. `visibility`
   - animation 사용 불가

6. `display`
   - animation 사용 불가
   - layout 영역도 사라짐

7.  HTML `hidden` attribute

8. position `absolute`의 `left: -999px`
   - layout 영역도 사라짐(이동됨)

9. `::after`등 다른 element로 overlay

10. `height`등 사이즈 축소

## Conclusion
- 애니메이션이 필요하지 않을때는 `display: none` 추천
- 퍼포먼스를 생각하면 `transform`이나 `opacity`
