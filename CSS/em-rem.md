# em, rem
- 절대값인 px의 반대되는 상대값
- 폰트값을 기준으로 배율단위
- px는 특별한 경우를 제외하고는 사용 금지

## em
- 상위 엘리먼트의 `font-size`를 기준 (정확히는, 실제 사용된 요소의 폰트 크기와 직접 연관)
- em 보다는 rem으로 처리하는게 더 유연

## rem
- 루트인 html의 `font-size`를 기준
- 특별한 선언없을땐 브라우저 기본인 `16px`이 `1rem`임
- media query로 break point에 html의 `font-size`만 변경하면 디스플레이 사이즈마다 손쉽게 가변적 변경 가능
- `font-size`를 `10px`로 초기화해놓으면 `1.1rem`은 `11px`, `1.2rem`은 `12px`와 같이 계산하기 쉬움
