---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the FlyingLet API
---

# Introduction

FlyingLet API에 오신 것을 환영합니다! 우리의 API를 사용하여 데이터베이스에 있는 다양한 로봇에 대한 정보를 얻을 수 있습니다.

우리는 Shell, Ruby, Python, JavaScript에서의 언어 바인딩을 제공합니다! 오른쪽의 어두운 영역에서 코드 예제를 확인할 수 있으며, 오른쪽 상단의 탭을 사용하여 예제의 프로그래밍 언어를 변경할 수 있습니다.

이 예시 API 문서 페이지는 Slate로 생성되었습니다. 필요에 따라 편집하고, 자체 API 문서의 기반으로 사용하실 수 있습니다.

# Authentication

## Access Token, Refresh Token 발급 

> To authorize, use this code:

```python
import requests

# POST 요청 보내기
data = {
    "email":"your@email.com",
    "password":"password"
}

response = requests.post('https://dev.flyinglet.com/login', json=data)

# 응답 상태 코드 확인
status_code = response.status_code
print(f'Status Code: {status_code}')

# 응답 본문 출력
data = response.json()
print('Response Body:')
print(data)

```

> The above command returns JSON structured like this:

```json
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTY4ODM3MTgyNiwianRpIjoiMWVmNjc3YjUtNTM0OS00NjA3LTg3ZjAtZmI2MzkwM2VlOTMxIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImltZ3VteEBuYXZlci5jb20iLCJuYmYiOjE2ODgzNzE4MjYsImV4cCI6MTY4ODM3MTg4Niwicm9sZSI6InVzZXIifQ.xtzQhYpB4TW__m6dyG3YL_wp2DDsi_ShPOHIztBKKrQ",
    "refresh_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTY4ODM3MTgyNiwianRpIjoiZjE1ZDJkNmMtMDgyZS00Njg5LTk1NjctYTg3NDc3NmFhNDI2IiwidHlwZSI6InJlZnJlc2giLCJzdWIiOiJpbWd1bXhAbmF2ZXIuY29tIiwibmJmIjoxNjg4MzcxODI2LCJleHAiOjE2ODgzNzU0MjZ9.qV4hdV0cNGW1YTEc4AzhZ0qvHB3ORXIWX2CBkKq4iLI"
}
```

> Make sure to replace `meowmeowmeow` with your API key.


1) 클라이언트에서 로그인 시 인증 서버에 유저 인증 요청.

2) 인증 서버에서 클라이언트로 Access token 과 Refresh token 발급, 클라이언트 쿠키에 저장.

3) 클라이언트에서 유효한 Access token을 헤더에 담아 서버에 리소스 요청.

4) Access token 이 유효하면 요청 리소스 응답.

5) 클라이언트에서 유효하지 않은 Access token을 헤더에 담아 서버에 리소스 요청.

6) 서버에서 클라이언트로 토큰 에러 메시지 응답.

7) 클라이언트에서 토큰 에러 메시지를 받았다면, 인증 서버로 Refresh token 전송.

8) Refresh token이 유효하다면 새 Access token 과 기존 Refresh token 응답.

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal Access token.
</aside>

# Kittens

## Get All Kittens

```python
import requests

# GET 요청 보내기
response = requests.get('https://dev.api.flyinglet.com/')

# 응답 상태 코드 확인
status_code = response.status_code
print(f'Status Code: {status_code}')

# 응답 본문 출력
data = response.json()
print('Response Body:')
print(data)

```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```
> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

