# Content-Type

```jsx
Content-Type: application/json
```

이렇게 json 형태로 보냄을 명시해주어야하는데, 해당 페이지에서 사용했던 jQuery 코드가 디폴트로 contentType을 아래처럼 url encoding 방식으로 지정해버려서 문제가 되었다. 이러한 형식을 사용할 경우에는 따로 encoding이 필요하다.

```jsx
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
```

[application/x-www-form-urlencoded](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods/POST): &으로 분리되고, "=" 기호로 값과 키를 연결하는 key-value tuple로 인코딩되는 값입니다. 영어 알파벳이 아닌 문자들은 percent encoded 으로 인코딩됩니다. 따라서, 이 content type은 바이너리 데이터에 사용하기에는 적절치 않습니다. (바이너리 데이터에는 use multipart/form-data 를 사용해 주세요.)

## Content-Type이란?

MIME(Multipurpose Internet Mail Extensions, 다목적 인터넷 메일 확장) 타입이라고 하는 데이터 포맷 라벨.

## 해결

api 호출하는 제이쿼리 코드 변경

1. contentType 지정(application/json)
2. dataType 지정(json)

```jsx
$.ajax({
	url: "url",
  data: JSON.stringify(params),
  cache: false,
  contentType: 'application/json',
  type: 'POST',
  dataType: 'json',
})
```

## 결론

- API 호출 시 Header를 잘 살펴보자.
  - 특히 API POST 시 Content-Type 및 Accept 부분을 잘 살펴봐야한다.