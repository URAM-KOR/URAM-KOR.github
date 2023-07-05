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

# URL
url = 'https://dev.flyinglet.com/login'

# POST 요청 보내기
data = {
    "email":"your@email.com",
    "password":"password"
}

response = requests.post(url, json=data)

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

1) 클라이언트에서 로그인 시 인증 서버에 유저 인증 요청.

2) 인증 서버에서 클라이언트로 Access token 과 Refresh token 발급, 클라이언트 쿠키에 저장.

3) 클라이언트에서 유효한 Access token을 헤더에 담아 서버에 리소스 요청.

4) Access token 이 유효하면 요청 리소스 응답.

5) 클라이언트에서 유효하지 않은 Access token을 헤더에 담아 서버에 리소스 요청.

6) 서버에서 클라이언트로 토큰 에러 메시지 응답.

7) 클라이언트에서 토큰 에러 메시지를 받았다면, 인증 서버로 Refresh token 전송.

8) Refresh token이 유효하다면 새 Access token 과 기존 Refresh token 응답.

### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | 회원 가입 시 등록한 E-mail.
password | false | 회원 가입 시 등록한 비밀번호.


## Access Token 재발급 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/refresh'

# GET 요청 보내기
response = requests.get(url)

# 응답 상태 코드 확인
status_code = response.status_code
print(f'Status Code: {status_code}')

# 응답 본문 출력
data = response.json()
print('Response Body:')
print(data)
```

7) 클라이언트에서 토큰 에러 메시지를 받았다면, 인증 서버로 Refresh token 전송.

8) Refresh token이 유효하다면 새 Access token 과 기존 Refresh token 응답.

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal Refresh token.
</aside>

> The above command returns JSON structured like this:

```json
{
    "new_access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTY4ODM3NTgxNSwianRpIjoiYTEyZjFiYjAtOTY0YS00MTI5LWI3YTEtNTM0YjNkNzQwN2Q0IiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImltZ3VteEBuYXZlci5jb20iLCJuYmYiOjE2ODgzNzU4MTUsImV4cCI6MTY4ODM3NTg3NSwicm9sZSI6InVzZXIifQ.P0lGrivKnWIPz9CqRD6a0_sFTrkBVJSDLk3wyeRSyoY"
}
```

# Data managment

## Get Admin collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Admin'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "63894ed9390843c9e175c20b"
        },
        "email": "jsmsumin2@integrit.ai",
        "password": "1234",
        "role": "일반관리자",
        "phoneNumber": "12341234",
        "adminName": "장수민2",
        "adminId": "63894ed9390843c9e175c20b",
        "createAt": "2022-12-13 09:50:41",
        "adminProfile": "{\"success\": \" \", \"login\": \" \", \"owner_id\": \" \", \"user\": {\"user_id\": \" \", \"profile\": {\"name\": \" \", \"profile_img\": \" \", \"owner_id\": \" \"}}, \"group_info\": {\"name\": \" \", \"address\": \" \", \"profile_img\": \" \"}, \"robot_list\": [{\"robot_id\": \" \", \"map_id\": \" \", \"port\": \" \"}], \"map_list\": [{\"id\": \" \", \"name\": \" \"}]}"
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Admin`

### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Create Admin collection 

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Admin'

# POST 요청 보내기
data = {
    "email": "new_admin@integrit.ai",
    "password": "1234",
    "role": "일반관리자",
    "phoneNumber": "12341234",
    "adminName": "장수민2",
    "adminId": "63894ed9390843c9e175c20b",
    "adminProfile": "{\"success\": \" \", \"login\": \" \", \"owner_id\": \" \", \"user\": {\"user_id\": \" \", \"profile\": {\"name\": \" \", \"profile_img\": \" \", \"owner_id\": \" \"}}, \"group_info\": {\"name\": \" \", \"address\": \" \", \"profile_img\": \" \"}, \"robot_list\": [{\"robot_id\": \" \", \"map_id\": \" \", \"port\": \" \"}], \"map_list\": [{\"id\": \" \", \"name\": \" \"}]}"
}

response = requests.post(url, json=data)
# 응답 상태 코드 확인
status_code = response.status_code
print(f'Status Code: {status_code}')

# 응답 본문 출력
data = response.json()
print('Response Body:')
print(data)

```

> The above command returns TEXT structured like this:

```text
64a4fe3dc0cca540d70b7858
```

### HTTP Request

`POST https://dev.flyinglet.com/Admin`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | email
password | false | password
role | false | role
phoneNumber | false | phoneNumber
adminId | false | adminId
adminProfile | false | adminProfile


## Get Robots collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Robots'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "6389a31716beaa76e42a2821"
        },
        "profile_id": "6389a37016beaa76e42a284c",
        "createAt": "2022-11-01",
        "agentID": " d6456517-3e13-47fd-878b-4e567e5d70f3",
        "alias": " ",
        "location_id": " ",
        "model_id": " ",
        "offStateCustomImgUrl": " ",
        "onStateCustomImgUrl": " "
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Robots`

### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Create Robots collection 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Robots'

# POST 요청 보내기
data = {
        "profile_id": "6389a37016beaa76e42a284c",
        "agentID": " d6456517-3e13-47fd-878b-4e567e5d70f3",
        "alias": " ",
        "location_id": " ",
        "model_id": " ",
        "offStateCustomImgUrl": " ",
        "onStateCustomImgUrl": " "
    }

response = requests.post(url, json=data)
# 응답 상태 코드 확인
status_code = response.status_code
print(f'Status Code: {status_code}')

# 응답 본문 출력
data = response.json()
print('Response Body:')
print(data)

```

> The above command returns TEXT structured like this:

```text
64a5081ec0cca540d70b788e
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>

### HTTP Request

`POST https://dev.flyinglet.com/Users`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
profile_id | false | profile_id
agentID | false | agentID
alias | false | alias
model_id | false | model_id
offStateCustomImgUrl | false | offStateCustomImgUrl
onStateCustomImgUrl | false | onStateCustomImgUrl


## Get Users collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Users'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "638ead49375c1b4d5eeabc71"
        },
        "email": "lotteworld_adventure@flyinglet.com",
        "password": "N949kh5U",
        "role": "admin",
        "userName": "롯데월드",
        "phoneNumber": "01012345678",
        "managedRobotIds": [
            "6389a31716beaa76e42a2821"
        ],
        "createAt": "2022-12-26 06:26:46",
        "loginProfile": {
            "success": 1,
            "login": 1,
            "owner_id": "00g3iat15h9RAJAcu5d7",
            "user": {
                "user_id": "00u3ias75zYoF6hTb5d7",
                "profile": {
                    "name": "롯데월드",
                    "profile_img": "https://dolseokmaru.flyinglet.com/images/lotte_user.png"
                }
            },
            "group_info": {
                "name": "롯데월드 어드벤처",
                "address": "서울 송파구 올림픽로 240",
                "profile_img": "https://dolseokmaru.flyinglet.com/images/lotte_world.jpeg"
            },
            "robot_list": [
                {
                    "robot_id": "cubrick_01_00_00",
                    "map_id": "lotteworld_museum",
                    "port": 21000
                },
                {
                    "robot_id": "dconic_0124_112351",
                    "map_id": "lotteworld_museum",
                    "port": 21001
                }
            ],
            "managedRobots": [
                {
                    "_id": {
                        "$oid": "6389a31e16beaa76e42a2826"
                    },
                    "serialNum": "2jSTYTcPFziudha7qpaQ",
                    "profile_id": "6389a38816beaa76e42a2856",
                    "profile": {
                        "_id": {
                            "$oid": "6389a38816beaa76e42a2856"
                        },
                        "alias": "CUBRICK_LOTTE",
                        "onStateCustomImgUrl": "/robot_model/cubrick/robot_lotteworld.png",
                        "offStateCustomImgUrl": "/robot_model/cubrick/robot_cubrick_off.png",
                        "model_id": "63ad25d1a2116f9b697cfed7",
                        "location_id": "6389a71c16beaa76e42a294d"
                    }
                },
                {
                    "_id": {
                        "$oid": "6389a31716beaa76e42a2821"
                    },
                    "serialNum": "259hSADFjGuhoQb9EMB9",
                    "profile_id": "6389a37016beaa76e42a284c",
                    "createAt": "",
                    "profile": {
                        "_id": {
                            "$oid": "6389a37016beaa76e42a284c"
                        },
                        "alias": "D.CORNIC_LOTTE",
                        "onStateCustomImgUrl": "/robot_model/dconic_v1/base.png",
                        "offStateCustomImgUrl": "/robot_model/dconic_v1/base_off.png",
                        "model_id": "63ad25c6a2116f9b697cfed4",
                        "location_id": "6389a70e16beaa76e42a2948",
                        "createAt": " "
                    }
                }
            ],
            "map_list": [
                {
                    "id": "lotteworld_adventure",
                    "name": "롯데월드 어드벤처"
                },
                {
                    "id": "lotteworld_folk_museum",
                    "name": "롯데월드 민속박물관"
                }
            ]
        },
        "group_info": {
            "address": "서울 송파구 올림픽로 240",
            "name": "롯데월드 어드벤처",
            "profile_img": "https://dolseokmaru.flyinglet.com/images/lotte_world.jpeg"
        },
        "login": "1",
        "map_list": [
            {
                "id": "lotteworld_adventure",
                "name": "롯데월드 어드벤처"
            },
            {
                "id": "lotteworld_folk_museum",
                "name": "롯데월드 민속박물관"
            }
        ],
        "owner_id": "00g3iat15h9RAJAcu5d7",
        "robot_list": [
            {
                "map_id": "lotteworld_museum",
                "oid": "63dc6f9afcdf6a52ae5f5332",
                "port": 21000,
                "robot_id": "cubrick_01_00_00"
            },
            {
                "map_id": "lotteworld_museum",
                "oid": "63dc6f9afcdf6a52ae5f5332",
                "port": 21001,
                "robot_id": "cubrick_01_00_00"
            },
            {
                "map_id": "lotteworld_museum",
                "oid": "63dc7008fcdf6a52ae5f5346",
                "port": 21002,
                "robot_id": "dconic_0124_112351"
            }
        ],
        "success": "1",
        "user": {
            "profile": {
                "name": "롯데월드",
                "profile_img": "https://robot-develop-server.s3.ap-northeast-2.amazonaws.com/2023-02-09-15:31:30_5.png",
                "uploaded_profile_img": "https://robot-develop-server.s3.ap-northeast-2.amazonaws.com/2023-02-09-15:31:30_5.png"
            },
            "user_id": "00u3ias75zYoF6hTb5d7"
        },
        "site_id": "6389a4ae16beaa76e42a28b7",
        "managedRobots": [
            {
                "_id": {
                    "$oid": "6389a31716beaa76e42a2821"
                },
                "profile_id": "6389a37016beaa76e42a284c",
                "createAt": "2022-11-01",
                "agentID": " d6456517-3e13-47fd-878b-4e567e5d70f3",
                "alias": " ",
                "location_id": " ",
                "model_id": " ",
                "offStateCustomImgUrl": " ",
                "onStateCustomImgUrl": " ",
                "profile": [
                    {
                        "_id": {
                            "$oid": "6389a37016beaa76e42a284c"
                        },
                        "alias": "D.CORNIC_LOTTE",
                        "onStateCustomImgUrl": "/robot_model/dconic_v1/base.png",
                        "offStateCustomImgUrl": "/robot_model/dconic_v1/base_off.png",
                        "model_id": "63ad25c6a2116f9b697cfed4",
                        "location_id": "6389a70e16beaa76e42a2948",
                        "createAt": " "
                    }
                ]
            }
        ],
        "subUserIDs": [
            "00g1z852ki8nSmOlP5d7",
            "00g3ukdrjuYT8Hg4L5d7",
            "hyundaipangyo",
            "hyundaitrade",
            "coex",
            "ssg",
            "skt"
        ],
        "hashed": "24326224313224314e4f7969786d49635a5638745275716633612f3075344869787a72534969717773325a786e78414c7344476c3639767536537775"
    }
]
```

`Authorization: meowmeowmeow`

[//]: # (<aside class="notice">)

[//]: # (You must replace <code>meowmeowmeow</code> with your personal Access token.)

[//]: # (</aside>)


### HTTP Request

`GET https://dev.flyinglet.com/Robots`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Create Users collection 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Users'

# POST 요청 보내기
data = [
    {
        "email": "uram@naver.com",
        "password": "1234",
        "role": "admin",
        "userName": "uram",
        "phoneNumber": "01012345678",
        "login": "1",
        "success": "1"
    }
]

response = requests.post(url, json=data)
# 응답 상태 코드 확인
status_code = response.status_code
print(f'Status Code: {status_code}')

# 응답 본문 출력
data = response.json()
print('Response Body:')
print(data)

```

> The above command returns TEXT structured like this:

```text
64a5081ec0cca540d70b788e
```

### HTTP Request

`POST https://dev.flyinglet.com/Users`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | email
password | false | password
role | false | role
phoneNumber | false | phoneNumber
login | false | login
success | false | success


## Get Profiles collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Profiles'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "6389a37016beaa76e42a284c"
        },
        "alias": "D.CORNIC_LOTTE",
        "onStateCustomImgUrl": "/robot_model/dconic_v1/base.png",
        "offStateCustomImgUrl": "/robot_model/dconic_v1/base_off.png",
        "model_id": "63ad25c6a2116f9b697cfed4",
        "location_id": "6389a70e16beaa76e42a2948",
        "createAt": " "
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Profiles`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Create Profiles collection 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Profiles'

# POST 요청 보내기
data = {
        "alias": "D.alias",
        "onStateCustomImgUrl": "/robot_model/dconic_v1/base.png",
        "offStateCustomImgUrl": "/robot_model/dconic_v1/base_off.png",
        "model_id": "63ad25c6a2116f9b697cfed4",
        "location_id": "6389a70e16beaa76e42a2948"
    }

response = requests.post(url, json=data)
# 응답 상태 코드 확인
status_code = response.status_code
print(f'Status Code: {status_code}')

# 응답 본문 출력
data = response.json()
print('Response Body:')
print(data)

```

> The above command returns TEXT structured like this:

```text
64a5081ec0cca540d70b788e
```

### HTTP Request

`POST https://dev.flyinglet.com/Profiles`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
alias | false | alias
onStateCustomImgUrl | false | onStateCustomImgUrl
offStateCustomImgUrl | false | offStateCustomImgUrl
model_id | false | model_id
location_id | false | location_id


## Get Models collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Models'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "63ad25c6a2116f9b697cfed4"
        },
        "modelName": "D.CORNIC",
        "onStateDefaultImgUrl": "/robot_model/dconic_v1/base.png",
        "offStateDefaultImgUrl": "/robot_model/dconic_v1/base_off.png",
        "specialFunctions": "컨시어지, AUTONOMOUS, 발열탐지, 음성대화, 도슨트, 노마스크탐지",
        "createAt": "2022-12-29 05:29:42",
        "supplierContact": " ",
        "supplierHomepage": " ",
        "supplierName": " ",
        "homepage": " ",
        "manufacturer": " ",
        "manufacturerContact": "",
        "manufacturingDate": "",
        "modelId": "63ad25c6a2116f9b697cfed4"
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Models`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Create Models collection 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Models'

# POST 요청 보내기
data = {
        "modelName": "D.CORNIC",
        "onStateDefaultImgUrl": "/robot_model/dconic_v1/base.png",
        "offStateDefaultImgUrl": "/robot_model/dconic_v1/base_off.png",
        "specialFunctions": "컨시어지, AUTONOMOUS, 발열탐지, 음성대화, 도슨트, 노마스크탐지",
        "supplierContact": " ",
        "supplierHomepage": " ",
        "supplierName": " ",
        "homepage": " ",
        "manufacturer": " ",
        "manufacturerContact": "",
        "manufacturingDate": "",
        "modelId": "63ad25c6a2116f9b697cfed4"
    }


response = requests.post(url, json=data)
# 응답 상태 코드 확인
status_code = response.status_code
print(f'Status Code: {status_code}')

# 응답 본문 출력
data = response.json()
print('Response Body:')
print(data)

```

> The above command returns TEXT structured like this:

```text
64a5081ec0cca540d70b788e
```

### HTTP Request

`POST https://dev.flyinglet.com/Models`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
modelName | false | modelName
onStateDefaultImgUrl | false | onStateDefaultImgUrl
offStateDefaultImgUrl | false | offStateDefaultImgUrl
specialFunctions | false | specialFunctions
supplierContact | false | supplierContact
supplierHomepage | false | supplierHomepage
supplierName | false | supplierName
homepage | false | homepage
manufacturer | false | manufacturer
manufacturerContact | false | manufacturerContact
manufacturingDate | false | manufacturingDate
modelId | false | modelId


## Get Locations collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Locations'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "6389a6e616beaa76e42a293e"
        },
        "type": "location",
        "locationName": "출입구",
        "locationPoint": "3층",
        "site_id": "6389a48f16beaa76e42a2898",
        "locationId": "6389a6e616beaa76e42a293e",
        "createAt": ""
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Locations`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Create Locations collection 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Locations'

# POST 요청 보내기
data = {
        "type": "location",
        "locationName": "출입구",
        "locationPoint": "3층",
        "site_id": "6389a48f16beaa76e42a2898",
        "locationId": "6389a6e616beaa76e42a293e",
    }

response = requests.post(url, json=data)
# 응답 상태 코드 확인
status_code = response.status_code
print(f'Status Code: {status_code}')

# 응답 본문 출력
data = response.json()
print('Response Body:')
print(data)

```

> The above command returns TEXT structured like this:

```text
64a5081ec0cca540d70b788e
```

### HTTP Request

`POST https://dev.flyinglet.com/Locations`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
type | false | type
locationName | false | locationName
locationPoint | false | locationPoint
site_id | false | site_id
locationId | false | locationId


## Get Sites collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Sites'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "6389a42716beaa76e42a2880"
        },
        "type": "site",
        "siteName": "신세계 Art&Science",
        "address": "대전광역시 유성구 엑스포로 17",
        "latitude": "127.3819045",
        "longitude": "36.3751677",
        "summaries_id": "6389a4e716beaa76e42a28cb",
        "createAt": " ",
        "locations": [
            {
                "_id": {
                    "$oid": "63914483e40bdfbe2e866a51"
                },
                "locationName": "BMW",
                "locationPoint": "5층",
                "site_id": "6389a42716beaa76e42a2880",
                "type": "location"
            }
        ],
        "summary": {
            "_id": {
                "$oid": "6389a4e716beaa76e42a28cb"
            },
            "point": "2층",
            "robotCount": "2",
            "flagshipStore": "민속박물관, 저잣거리",
            "routeDistance": "1100",
            "routeTime": "70",
            "videoCount": "7",
            "createAt": ""
        }
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Sites`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Create Sites collection 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Sites'

# POST 요청 보내기
data = {
        "type": "type",
        "siteName": "siteName",
        "address": "address",
        "latitude": "latitude",
        "longitude": "longitude",
        "summaries_id": "summaries_id",
    }
response = requests.post(url, json=data)
# 응답 상태 코드 확인
status_code = response.status_code
print(f'Status Code: {status_code}')

# 응답 본문 출력
data = response.json()
print('Response Body:')
print(data)

```

> The above command returns TEXT structured like this:

```text
64a5081ec0cca540d70b788e
```

### HTTP Request

`POST https://dev.flyinglet.com/Sites`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | email
password | false | password
role | false | role
phoneNumber | false | phoneNumber
login | false | login
success | false | success


## Get Summaries collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Summaries'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "6389a4e716beaa76e42a28cb"
        },
        "point": "2층",
        "robotCount": "2",
        "flagshipStore": "민속박물관, 저잣거리",
        "routeDistance": "1100",
        "routeTime": "70",
        "videoCount": "7",
        "createAt": ""
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Summaries`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Create Users collection 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Users'

# POST 요청 보내기
data = [
    {
        "email": "uram@naver.com",
        "password": "1234",
        "role": "admin",
        "userName": "uram",
        "phoneNumber": "01012345678",
        "login": "1",
        "success": "1"
    }
]

response = requests.post(url, json=data)
# 응답 상태 코드 확인
status_code = response.status_code
print(f'Status Code: {status_code}')

# 응답 본문 출력
data = response.json()
print('Response Body:')
print(data)

```

> The above command returns TEXT structured like this:

```text
64a5081ec0cca540d70b788e
```

### HTTP Request

`POST https://dev.flyinglet.com/Users`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | email
password | false | password
role | false | role
phoneNumber | false | phoneNumber
login | false | login
success | false | success


## Get Registry collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Registry'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "63c7bf02c87c271cea17d0e8"
        },
        "deviceName": "더현대큐브릭1",
        "deviceNum": "1",
        "kcCertificationNumber": "ICRT-TR-E223277-0A",
        "mainAbility": [
            "spcfunc-aichat"
        ],
        "manufacturer": "INTEGRIT",
        "min": "",
        "modelImg": {
            "off": "https://app.flyinglet.com/images/robot_model/integrit/cubrick_base_off.png",
            "on": "https://app.flyinglet.com/images/robot_model/integrit/cubrick_thehyundai.png"
        },
        "modelName": "CUB-DS210V",
        "modelNumber": "",
        "modelVersion": "1",
        "productName": "CUBRICK",
        "operatingLocation": "더현대서울1F",
        "serialNumber": "11000",
        "subAbility": [
            "spcfunc-docent",
            "spcfunc-hightemp"
        ],
        "specialFunctions": [
            {
                "id": "spcfunc-aichat",
                "mainType": 1,
                "value": 1
            },
            {
                "id": "spcfunc-docent",
                "mainType": 0,
                "value": 1
            },
            {
                "id": "spcfunc-hightemp",
                "mainType": 0,
                "value": 1
            }
        ],
        "fCode": "INTE-CUB-04184-012301-00000",
        "manufacturerCode": "INTE",
        "productCode": "CUB",
        "modelCode": "CUB",
        "createAt": "2023-01-18  6:42:26 PM",
        "productDate": "",
        "manager_01": "",
        "sms_01": "",
        "manager_02": "전기만",
        "sms_02": "8201085850124",
        "manager_03": "",
        "sms_03": "",
        "userID": "",
        "location_id": "",
        "realRobotID": "",
        "battery": "",
        "current_covid_info": {},
        "current_waypoint_id": "",
        "drive_distance": "",
        "drive_status": "",
        "drive_time": "",
        "map_id": "",
        "network": "",
        "robot_id": "robot_cubrick_01_v2",
        "robot_status": "",
        "speed": "",
        "total_distance": "",
        "total_time": "",
        "isActive": "True",
        "alarm_01": "False",
        "alarm_02": "0",
        "alarm_03": "False",
        "mac_address": "00:15:5d:e1:cf:59",
        "secretKey": "1234",
        "authentication_timestamp": "1684117946",
        "getnode": "91769392985",
        "machine": "AMD64",
        "node": "DESKTOP-QM8726M",
        "platform": "Windows-10-10.0.25352-SP0",
        "processor": "AMD64 Family 25 Model 68 Stepping 1, AuthenticAMD",
        "release": "10",
        "system": "Windows",
        "uname": "Windows",
        "version": "10.0.25352",
        "photo_log": {
            "1684921527": {
                "43269": {
                    "robot_id": "robot_cubrick_01_v2",
                    "pose": {
                        "x": 1213,
                        "y": 78,
                        "rotate": -32.27673803755728
                    },
                    "store_id": 3,
                    "timestamp": 1684921527.43269,
                    "map_id": "thehyundai_1f",
                    "drive_info": null,
                    "drive_status": "Stop",
                    "traffic": 2
                }
            }
        },
        "chipSN": "0x42fc3212"
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Registry`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Create Users collection 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Users'

# POST 요청 보내기
data = [
    {
        "email": "uram@naver.com",
        "password": "1234",
        "role": "admin",
        "userName": "uram",
        "phoneNumber": "01012345678",
        "login": "1",
        "success": "1"
    }
]

response = requests.post(url, json=data)
# 응답 상태 코드 확인
status_code = response.status_code
print(f'Status Code: {status_code}')

# 응답 본문 출력
data = response.json()
print('Response Body:')
print(data)

```

> The above command returns TEXT structured like this:

```text
64a5081ec0cca540d70b788e
```

### HTTP Request

`POST https://dev.flyinglet.com/Users`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | email
password | false | password
role | false | role
phoneNumber | false | phoneNumber
login | false | login
success | false | success


## Get Managers collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Managers'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "63bcc3c181cd3069ff42fd4b"
        },
        "createAt": "2023-01-10 10:47:45",
        "deviceName": "D.conic",
        "deviceNum": " test",
        "manager_01": " m1",
        "manager_02": " m2",
        "manager_03": " m3",
        "sms_01": " s1",
        "sms_02": " s2",
        "sms_03": " s3"
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Managers`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Create Users collection 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Users'

# POST 요청 보내기
data = [
    {
        "email": "uram@naver.com",
        "password": "1234",
        "role": "admin",
        "userName": "uram",
        "phoneNumber": "01012345678",
        "login": "1",
        "success": "1"
    }
]

response = requests.post(url, json=data)
# 응답 상태 코드 확인
status_code = response.status_code
print(f'Status Code: {status_code}')

# 응답 본문 출력
data = response.json()
print('Response Body:')
print(data)

```

> The above command returns TEXT structured like this:

```text
64a5081ec0cca540d70b788e
```

### HTTP Request

`POST https://dev.flyinglet.com/Users`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | email
password | false | password
role | false | role
phoneNumber | false | phoneNumber
login | false | login
success | false | success


## Get Manufacturers collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Manufacturers'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "63e0a3a9c6f98e87f3f58da5"
        },
        "createAt": "2023-01-17 18:32:41",
        "code": "INTE",
        "contact": "02-2051-0978",
        "manufacturer": "INTEGRIT",
        "manufacturerAddress": "서울 강남구 삼성로 547 (삼성동, BK타워)",
        "manufacturerHomepage": "integrit.ai"
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Manufacturers`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Create Users collection 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Users'

# POST 요청 보내기
data = [
    {
        "email": "uram@naver.com",
        "password": "1234",
        "role": "admin",
        "userName": "uram",
        "phoneNumber": "01012345678",
        "login": "1",
        "success": "1"
    }
]

response = requests.post(url, json=data)
# 응답 상태 코드 확인
status_code = response.status_code
print(f'Status Code: {status_code}')

# 응답 본문 출력
data = response.json()
print('Response Body:')
print(data)

```

> The above command returns TEXT structured like this:

```text
64a5081ec0cca540d70b788e
```

### HTTP Request

`POST https://dev.flyinglet.com/Users`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | email
password | false | password
role | false | role
phoneNumber | false | phoneNumber
login | false | login
success | false | success


## Get LoginDataGroup collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/LoginDataGroup'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "63c75a8566dadd88acf0fac3"
        },
        "createAt": "2023-01-18 11:33:41",
        "Admin": "[]",
        "Locations": "['6389a70e16beaa76e42a2948','6389a71c16beaa76e42a294d']",
        "LoginDataGroup": "[]",
        "Managers": "['63bcc3c181cd3069ff42fd4b]",
        "Manufacturers": "['63c66b3987bc4b5508de6c67']",
        "Models": "['63ad25c6a2116f9b697cfed4','63ad25d1a2116f9b697cfed7']",
        "Profiles": "['6389a37016beaa76e42a284c','6389a38816beaa76e42a2856']",
        "Registry": "['63c10ba26ce1ed85231fffd8']",
        "Robots": "['6389a31716beaa76e42a2821','6389a31e16beaa76e42a2826']",
        "Sites": "['6389a4ae16beaa76e42a28b7']",
        "Summaries": "['6389a4e716beaa76e42a28cb']",
        "Users": "['638ead49375c1b4d5eeabc71']",
        "email": "lotteworld_adventure@flyinglet.com",
        "registry": "[]"
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/LoginDataGroup`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Create Users collection 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Users'

# POST 요청 보내기
data = [
    {
        "email": "uram@naver.com",
        "password": "1234",
        "role": "admin",
        "userName": "uram",
        "phoneNumber": "01012345678",
        "login": "1",
        "success": "1"
    }
]

response = requests.post(url, json=data)
# 응답 상태 코드 확인
status_code = response.status_code
print(f'Status Code: {status_code}')

# 응답 본문 출력
data = response.json()
print('Response Body:')
print(data)

```

> The above command returns TEXT structured like this:

```text
64a5081ec0cca540d70b788e
```

### HTTP Request

`POST https://dev.flyinglet.com/Users`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | email
password | false | password
role | false | role
phoneNumber | false | phoneNumber
login | false | login
success | false | success


## Get Robots Data Stream

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/stream'

# GET 요청 보내기
response = requests.get(url)

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
  "create_at": "2023-07-04T05:20:00+09:00",
  "covid_info": {
    "idx": false,
    "robot_id": false,
    "map_id": false,
    "store_id": false,
    "position_x": false,
    "position_y": false,
    "rotate": false,
    "location_desc": false,
    "temp": false,
    "mask_flag": false,
    "image": false,
    "timstamp": false,
    "year": false,
    "month": false,
    "date": false,
    "week_day": false,
    "hour": false,
    "timestamp": false,
    "day": false,
    "day_of_week": false,
    "description": false,
    "route_log_id": false,
    "lap_log_id": false,
    "section_log_id": false,
    "status": false
  }
}
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/stream`


## Get One Robot Data Stream

```python
import requests

# URL 
url = 'https://dev.api.flyinglet.com/stream/robot?robot_id=robot_id'

# GET 요청 보내기
response = requests.get(url)

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
  "create_at": "2023-07-04T06:58:11+09:00",
  "covid_info": {
    "idx": false,
    "robot_id": false,
    "map_id": false,
    "store_id": false,
    "position_x": false,
    "position_y": false,
    "rotate": false,
    "location_desc": false,
    "temp": false,
    "mask_flag": false,
    "image": false,
    "timstamp": false,
    "year": false,
    "month": false,
    "date": false,
    "week_day": false,
    "hour": false,
    "timestamp": false,
    "day": false,
    "day_of_week": false,
    "description": false,
    "route_log_id": false,
    "lap_log_id": false,
    "section_log_id": false,
    "status": false
  },
  "drive_section_log": {
    "section_log_id": false,
    "robot_id": false,
    "drive_time_id": false,
    "route_log_id": false,
    "lap_log_id": false,
    "current_index": false,
    "start_timestamp": false,
    "end_timestamp": false,
    "drive_time": false,
    "drive_distance": false,
    "resource": false,
    "update_at": false
  },  
  "lap_drive_log": {
    "lap_log_id": false,
    "route_log_id": false,
    "repetition": false,
    "drive_time": false,
    "drive_distance": false,
    "resource": false,
    "start_timestamp": false,
    "end_timestamp": false,
    "update_at": false,
    "robot_id": false
  },
  "map_store": {
    "idx": false,
    "map_idx": false,
    "map_id": false,
    "store_id": false,
    "store_name": false,
    "center_x": false,
    "center_y": false,
    "bound": false
  },
  "notification_token": {
    "id": false,
    "token": false,
    "group_id": false,
    "invalid": false,
    "user_agent": false,
    "checked_at": false
  },
  "red_zone": {
    "id": false,
    "map_id": false,
    "name": false,
    "state": false,
    "creator": false,
    "points": false,
    "update_at": false,
    "color": false
  },
  "robot_base_status": {
    "staus_idx": 37478894.0,
    "robot_id": "cubrick_01_00_00",
    "speed": 0.394,
    "battery": 48.0,
    "network": "GOOD",
    "drive_status": "Driving",
    "current_way_point_id": "lotte_folk_220719_cruzing_220728.csv",
    "map_id": "lotte_folk_220719",
    "timestamp": 1688453891021.0
  },
  "robot_drive_info": {
    "drive_idx": false,
    "robot_id": false,
    "robot_idx": false,
    "start_time_stamp": false,
    "start_year": false,
    "start_month": false,
    "start_date": false,
    "start_week_day": false,
    "start_time": false,
    "end_time_stamp": false,
    "end_time": false,
    "drive_time": false,
    "drive_distance": false,
    "average_speed": false,
    "max_speed": false,
    "min_speed": false,
    "total_distance": false,
    "total_time": false,
    "map_id": false
  },
  "robot_info": {
    "idx": false,
    "mac_address": false,
    "name": false,
    "hw_ver": false,
    "sw_ver": false,
    "access_scope": false,
    "owner": false,
    "type": false,
    "update_at": false,
    "delete_at": false
  },
  "robot_region": {
    "traffic_idx": false,
    "region_id": false,
    "map_id": false,
    "position_x": false,
    "position_y": false,
    "width": false,
    "height": false
  },
  "route_drive_log": {
    "route_log_id": false,
    "way_point_id": false,
    "robot_id": false,
    "drive_time": false,
    "drive_distance": false,
    "start_timestamp": false,
    "end_timestamp": false,
    "resource": false,
    "update_at": false,
    "map_id": false,
    "way_point_repetition": false
  },
  "schedule": {
    "index": false,
    "id": false,
    "map_id": false,
    "title": false,
    "state": false,
    "week_days": false,
    "robots": false,
    "update_at": false,
    "cron_format": false,
    "timezone": false,
    "timer_timer_index": false,
    "timer_index": false,
    "timer_order_weight": false,
    "timer_hours": false,
    "timer_minutes": false,
    "timer_repeats": false,
    "timer_path_id": false,
    "timer_go_charger": false,
    "timer_update_at": false,
    "timer_cron_format": false
  },
  "schedule_timer": {
    "index": false,
    "schedule_index": false,
    "order_weight": false,
    "hours": false,
    "minutes": false,
    "repeats": false,
    "path_id": false,
    "go_charger": false,
    "update_at": false,
    "cron_format": false
  },
  "traffic_count": {
    "id": false,
    "robot_id": false,
    "map_id": false,
    "count": false,
    "start_utc_hours": false,
    "start_timestamp": false,
    "month": false,
    "weekOfDay": false,
    "hour": false,
    "update_at": false,
    "add_count": false
  },
    "visitor_count": {
    "id": 4250108.0,
    "robot_id": "robot_cubrick_01_v2",
    "map_id": "thehyundai_1f",
    "count": "1",
    "duration": 5.0,
    "start_timestamp": 1688453891.0,
    "update_at": false,
    "day_of_week": 2.0,
    "hour": 6.0,
    "route_log_id": -1.0,
    "lap_log_id": -1.0,
    "section_log_id": -1.0,
    "position": {
      "x": 1414,
      "y": 81,
      "rotate": -56.30890718111302
    }
  },
  "way_point_list": {
    "idx": false,
    "way_point_id": false,
    "name": false,
    "map_id": false,
    "version": false,
    "points": false,
    "update_at": false,
    "drive_distance": false,
    "drive_time": false,
    "id_color": false,
    "avaliable": false
  }
}
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.api.flyinglet.com/stream/robot?robot_id={{robot_id}}`

## Get Robot info

```python
import requests

# URL
url = 'https://dev.api.flyinglet.com/Registry/robot_id/robot_cubrick_01_v2'

# GET 요청 보내기
response = requests.get(url)

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
    "data": {
        "_id": {
            "$oid": "63c7bf02c87c271cea17d0e8"
        },
        "alarm_01": "False",
        "alarm_02": "0",
        "alarm_03": "False",
        "authentication_timestamp": "1684117946",
        "battery": "",
        "chipSN": "0x42fc3212",
        "createAt": "2023-01-18  6:42:26 PM",
        "current_covid_info": {},
        "current_waypoint_id": "",
        "deviceName": "더현대큐브릭1",
        "deviceNum": "1",
        "drive_distance": "",
        "drive_status": "",
        "drive_time": "",
        "fCode": "INTE-CUB-04184-012301-00000",
        "getnode": "91769392985",
        "isActive": "True",
        "kcCertificationNumber": "ICRT-TR-E223277-0A",
        "location_id": "",
        "mac_address": "00:15:5d:e1:cf:59",
        "machine": "AMD64",
        "mainAbility": [
            "spcfunc-aichat"
        ],
        "manager_01": "",
        "manager_02": "전기만",
        "manager_03": "",
        "manufacturer": "INTEGRIT",
        "manufacturerCode": "INTE",
        "map_id": "",
        "min": "",
        "modelCode": "CUB",
        "modelImg": {
            "off": "https://app.flyinglet.com/images/robot_model/integrit/cubrick_base_off.png",
            "on": "https://app.flyinglet.com/images/robot_model/integrit/cubrick_thehyundai.png"
        },
        "modelName": "CUB-DS210V",
        "modelNumber": "",
        "modelVersion": "1",
        "network": "",
        "node": "DESKTOP-QM8726M",
        "operatingLocation": "더현대서울1F",
        "photo_log": {
            "1684921527": {
                "43269": {
                    "drive_info": null,
                    "drive_status": "Stop",
                    "map_id": "thehyundai_1f",
                    "pose": {
                        "rotate": -32.27673803755728,
                        "x": 1213,
                        "y": 78
                    },
                    "robot_id": "robot_cubrick_01_v2",
                    "store_id": 3,
                    "timestamp": 1684921527.43269,
                    "traffic": 2
                }
            }
        },
        "platform": "Windows-10-10.0.25352-SP0",
        "processor": "AMD64 Family 25 Model 68 Stepping 1, AuthenticAMD",
        "productCode": "CUB",
        "productDate": "",
        "productName": "CUBRICK",
        "realRobotID": "",
        "release": "10",
        "robot_id": "robot_cubrick_01_v2",
        "robot_status": "",
        "secretKey": "1234",
        "serialNumber": "11000",
        "sms_01": "",
        "sms_02": "8201085850124",
        "sms_03": "",
        "specialFunctions": [
            {
                "id": "spcfunc-aichat",
                "mainType": 1,
                "value": 1
            },
            {
                "id": "spcfunc-docent",
                "mainType": 0,
                "value": 1
            },
            {
                "id": "spcfunc-hightemp",
                "mainType": 0,
                "value": 1
            }
        ],
        "speed": "",
        "subAbility": [
            "spcfunc-docent",
            "spcfunc-hightemp"
        ],
        "system": "Windows",
        "total_distance": "",
        "total_time": "",
        "uname": "Windows",
        "userID": "",
        "version": "10.0.25352"
    }
}
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.api.flyinglet.com/Registry/robot_id/{{robot_id}}`


### Path Parameters

Path 의 '{{robot_id}}'와 collection 내 'robot_id' 의 값이 일치하는 document 조회

Parameter | Default | Description
--------- | ------- | -----------
robot_id | false | Robot 등록시 저장된 'robot_id' 값.


# Business logic

## Admin Sign in 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/signin/Admin'

# POST 요청 보내기
data = {
    "email":"admin@email.com",
    "password":"password"
}

response = requests.post(url, json=data)
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
    "_id": {
        "$oid": "63894ed9390843c9e175c20b"
    },
    "email": "jsmsumin2@integrit.ai",
    "password": "1234",
    "role": "일반관리자",
    "phoneNumber": "12341234",
    "adminName": "장수민2",
    "adminId": "63894ed9390843c9e175c20b",
    "createAt": "2022-12-13 09:50:41",
    "adminProfile": "{\"success\": \" \", \"login\": \" \", \"owner_id\": \" \", \"user\": {\"user_id\": \" \", \"profile\": {\"name\": \" \", \"profile_img\": \" \", \"owner_id\": \" \"}}, \"group_info\": {\"name\": \" \", \"address\": \" \", \"profile_img\": \" \"}, \"robot_list\": [{\"robot_id\": \" \", \"map_id\": \" \", \"port\": \" \"}], \"map_list\": [{\"id\": \" \", \"name\": \" \"}]}"
}
```

### HTTP Request

`POST https://dev.flyinglet.com/signin/Admin`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | Admin email
password | false | Admin password

## User Sign in 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/signin'

# POST 요청 보내기
data = {
    "email":"user@email.com",
    "password":"password"
}

response = requests.post(url, json=data)
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
        "_id": {
            "$oid": "63e5d3007bf79f7a964eb356"
        },
        "addressDetail": "집주소",
        "companyName": "인티그리트",
        "createAt": "2023-02-10 14:15:44",
        "email": "User@integrit.ai",
        "fullAddress": "집주소",
        "group_info": {
            "address": "",
            "name": "",
            "profile_img": ""
        },
        "hashed": "2432622431322436515059395869384f32426c43394347583041516a2e7455625243594c4c717957745135434a50504a4b5577427272745967697a65",
        "job": "",
        "jobPosition": "",
        "login": "",
        "loginProfile": {
            "group_info": {
                "address": "사무실",
                "name": "인티그리트",
                "profile_img": "https://dolseokmaru.flyinglet.com/images/integrit_group.png"
            },
            "login": 1,
            "managedRobots": [
                {
                    "_id": {
                        "$oid": "6389a32b16beaa76e42a2830"
                    },
                    "profile": {
                        "_id": {
                            "$oid": "6389a3b116beaa76e42a2867"
                        },
                        "alias": "DCORNIC_INTEGRIT",
                        "location_id": "6389a6e616beaa76e42a293e",
                        "model_id": "63ad25c6a2116f9b697cfed4",
                        "offStateCustomImgUrl": "/robot_model/dconic_v1/base_off.png",
                        "onStateCustomImgUrl": "/robot_model/dconic_v1/base.png"
                    },
                    "profile_id": "6389a3b116beaa76e42a2867",
                    "serialNum": "4mV8vQRTySWTEsmSGja6"
                },
                {
                    "_id": {
                        "$oid": "6389a33516beaa76e42a283a"
                    },
                    "profile": {
                        "_id": {
                            "$oid": "6389a3c416beaa76e42a286d"
                        },
                        "alias": "CUBRICK_INTEGRIT",
                        "location_id": "6389a6f516beaa76e42a2943",
                        "model_id": "63ad25d1a2116f9b697cfed7",
                        "offStateCustomImgUrl": "/robot_model/cubrick/robot_cubrick_off.png",
                        "onStateCustomImgUrl": "/robot_model/cubrick/robot_cubrick_on.png"
                    },
                    "profile_id": "6389a3c416beaa76e42a286d",
                    "serialNum": "11jfmzFzf93fxkvmaklmv3"
                }
            ],
            "map_list": [
                {
                    "id": "kimpo_test_map",
                    "name": "강남대로 547 5층"
                },
                {
                    "id": "integrit_office",
                    "name": "강남대로 547 5층"
                }
            ],
            "owner_id": "00g3ukdrjuYT8Hg4L5d7",
            "robot_list": [
                {
                    "map_id": "kimpo_test_map",
                    "port": 21001,
                    "robot_id": "cubrick_212439084360"
                },
                {
                    "map_id": "integrit_office",
                    "port": 21003,
                    "robot_id": "cubrick_2234_634600"
                }
            ],
            "success": 1,
            "user": {
                "profile": {
                    "name": "integrit",
                    "profile_img": 0
                },
                "user_id": "00u3ukdmei72iPzOE5d7"
            }
        },
        "managedRobotIds": [],
        "managedRobots": [],
        "map_list": [
            {
                "id": "",
                "name": ""
            }
        ],
        "owner_id": "",
        "phoneNumber": "01037894591",
        "robot_list": [
            {
                "map_id": "",
                "oid": "",
                "port": "",
                "robot_id": ""
            }
        ],
        "role": "user",
        "site_id": "",
        "success": true,
        "user": {
            "profile": {
                "name": "사용자이름",
                "profile_img": "https://app.flyinglet.com/images/profile_icons/type-02/015-moustache.png"
            }
        },
        "userName": "사용자이름",
        "zipCode": "집주소"
    }
]
```

### HTTP Request

`POST https://dev.flyinglet.com/signin`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | User email
password | false | User password


## Check Password

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/check_password'

# POST 요청 보내기
data = {
    "email":"admin@email.com",
    "password":"password"
}

response = requests.post(url, json=data)
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
    "success": 1
}
```

### HTTP Request

`POST https://dev.flyinglet.com/signin/Admin`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | User email
password | false | User password

## Admin Sign in 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/signin/Admin'

# POST 요청 보내기
data = {
    "email":"admin@email.com",
    "password":"password"
}

response = requests.post(url, json=data)
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
    "_id": {
        "$oid": "63894ed9390843c9e175c20b"
    },
    "email": "jsmsumin2@integrit.ai",
    "password": "1234",
    "role": "일반관리자",
    "phoneNumber": "12341234",
    "adminName": "장수민2",
    "adminId": "63894ed9390843c9e175c20b",
    "createAt": "2022-12-13 09:50:41",
    "adminProfile": "{\"success\": \" \", \"login\": \" \", \"owner_id\": \" \", \"user\": {\"user_id\": \" \", \"profile\": {\"name\": \" \", \"profile_img\": \" \", \"owner_id\": \" \"}}, \"group_info\": {\"name\": \" \", \"address\": \" \", \"profile_img\": \" \"}, \"robot_list\": [{\"robot_id\": \" \", \"map_id\": \" \", \"port\": \" \"}], \"map_list\": [{\"id\": \" \", \"name\": \" \"}]}"
}
```

### HTTP Request

`POST https://dev.flyinglet.com/signin/Admin`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | Admin email
password | false | Admin password

## Admin Sign in 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/signin/Admin'

# POST 요청 보내기
data = {
    "email":"admin@email.com",
    "password":"password"
}

response = requests.post(url, json=data)
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
    "_id": {
        "$oid": "63894ed9390843c9e175c20b"
    },
    "email": "jsmsumin2@integrit.ai",
    "password": "1234",
    "role": "일반관리자",
    "phoneNumber": "12341234",
    "adminName": "장수민2",
    "adminId": "63894ed9390843c9e175c20b",
    "createAt": "2022-12-13 09:50:41",
    "adminProfile": "{\"success\": \" \", \"login\": \" \", \"owner_id\": \" \", \"user\": {\"user_id\": \" \", \"profile\": {\"name\": \" \", \"profile_img\": \" \", \"owner_id\": \" \"}}, \"group_info\": {\"name\": \" \", \"address\": \" \", \"profile_img\": \" \"}, \"robot_list\": [{\"robot_id\": \" \", \"map_id\": \" \", \"port\": \" \"}], \"map_list\": [{\"id\": \" \", \"name\": \" \"}]}"
}
```

### HTTP Request

`POST https://dev.flyinglet.com/signin/Admin`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | Admin email
password | false | Admin password

## Admin Sign in 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/signin/Admin'

# POST 요청 보내기
data = {
    "email":"admin@email.com",
    "password":"password"
}

response = requests.post(url, json=data)
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
    "_id": {
        "$oid": "63894ed9390843c9e175c20b"
    },
    "email": "jsmsumin2@integrit.ai",
    "password": "1234",
    "role": "일반관리자",
    "phoneNumber": "12341234",
    "adminName": "장수민2",
    "adminId": "63894ed9390843c9e175c20b",
    "createAt": "2022-12-13 09:50:41",
    "adminProfile": "{\"success\": \" \", \"login\": \" \", \"owner_id\": \" \", \"user\": {\"user_id\": \" \", \"profile\": {\"name\": \" \", \"profile_img\": \" \", \"owner_id\": \" \"}}, \"group_info\": {\"name\": \" \", \"address\": \" \", \"profile_img\": \" \"}, \"robot_list\": [{\"robot_id\": \" \", \"map_id\": \" \", \"port\": \" \"}], \"map_list\": [{\"id\": \" \", \"name\": \" \"}]}"
}
```

### HTTP Request

`POST https://dev.flyinglet.com/signin/Admin`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | Admin email
password | false | Admin password

## Admin Sign in 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/signin/Admin'

# POST 요청 보내기
data = {
    "email":"admin@email.com",
    "password":"password"
}

response = requests.post(url, json=data)
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
    "_id": {
        "$oid": "63894ed9390843c9e175c20b"
    },
    "email": "jsmsumin2@integrit.ai",
    "password": "1234",
    "role": "일반관리자",
    "phoneNumber": "12341234",
    "adminName": "장수민2",
    "adminId": "63894ed9390843c9e175c20b",
    "createAt": "2022-12-13 09:50:41",
    "adminProfile": "{\"success\": \" \", \"login\": \" \", \"owner_id\": \" \", \"user\": {\"user_id\": \" \", \"profile\": {\"name\": \" \", \"profile_img\": \" \", \"owner_id\": \" \"}}, \"group_info\": {\"name\": \" \", \"address\": \" \", \"profile_img\": \" \"}, \"robot_list\": [{\"robot_id\": \" \", \"map_id\": \" \", \"port\": \" \"}], \"map_list\": [{\"id\": \" \", \"name\": \" \"}]}"
}
```

### HTTP Request

`POST https://dev.flyinglet.com/signin/Admin`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | Admin email
password | false | Admin password

## Admin Sign in 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/signin/Admin'

# POST 요청 보내기
data = {
    "email":"admin@email.com",
    "password":"password"
}

response = requests.post(url, json=data)
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
    "_id": {
        "$oid": "63894ed9390843c9e175c20b"
    },
    "email": "jsmsumin2@integrit.ai",
    "password": "1234",
    "role": "일반관리자",
    "phoneNumber": "12341234",
    "adminName": "장수민2",
    "adminId": "63894ed9390843c9e175c20b",
    "createAt": "2022-12-13 09:50:41",
    "adminProfile": "{\"success\": \" \", \"login\": \" \", \"owner_id\": \" \", \"user\": {\"user_id\": \" \", \"profile\": {\"name\": \" \", \"profile_img\": \" \", \"owner_id\": \" \"}}, \"group_info\": {\"name\": \" \", \"address\": \" \", \"profile_img\": \" \"}, \"robot_list\": [{\"robot_id\": \" \", \"map_id\": \" \", \"port\": \" \"}], \"map_list\": [{\"id\": \" \", \"name\": \" \"}]}"
}
```

### HTTP Request

`POST https://dev.flyinglet.com/signin/Admin`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | Admin email
password | false | Admin password

## Admin Sign in 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/signin/Admin'

# POST 요청 보내기
data = {
    "email":"admin@email.com",
    "password":"password"
}

response = requests.post(url, json=data)
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
    "_id": {
        "$oid": "63894ed9390843c9e175c20b"
    },
    "email": "jsmsumin2@integrit.ai",
    "password": "1234",
    "role": "일반관리자",
    "phoneNumber": "12341234",
    "adminName": "장수민2",
    "adminId": "63894ed9390843c9e175c20b",
    "createAt": "2022-12-13 09:50:41",
    "adminProfile": "{\"success\": \" \", \"login\": \" \", \"owner_id\": \" \", \"user\": {\"user_id\": \" \", \"profile\": {\"name\": \" \", \"profile_img\": \" \", \"owner_id\": \" \"}}, \"group_info\": {\"name\": \" \", \"address\": \" \", \"profile_img\": \" \"}, \"robot_list\": [{\"robot_id\": \" \", \"map_id\": \" \", \"port\": \" \"}], \"map_list\": [{\"id\": \" \", \"name\": \" \"}]}"
}
```

### HTTP Request

`POST https://dev.flyinglet.com/signin/Admin`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | Admin email
password | false | Admin password

## Admin Sign in 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/signin/Admin'

# POST 요청 보내기
data = {
    "email":"admin@email.com",
    "password":"password"
}

response = requests.post(url, json=data)
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
    "_id": {
        "$oid": "63894ed9390843c9e175c20b"
    },
    "email": "jsmsumin2@integrit.ai",
    "password": "1234",
    "role": "일반관리자",
    "phoneNumber": "12341234",
    "adminName": "장수민2",
    "adminId": "63894ed9390843c9e175c20b",
    "createAt": "2022-12-13 09:50:41",
    "adminProfile": "{\"success\": \" \", \"login\": \" \", \"owner_id\": \" \", \"user\": {\"user_id\": \" \", \"profile\": {\"name\": \" \", \"profile_img\": \" \", \"owner_id\": \" \"}}, \"group_info\": {\"name\": \" \", \"address\": \" \", \"profile_img\": \" \"}, \"robot_list\": [{\"robot_id\": \" \", \"map_id\": \" \", \"port\": \" \"}], \"map_list\": [{\"id\": \" \", \"name\": \" \"}]}"
}
```

### HTTP Request

`POST https://dev.flyinglet.com/signin/Admin`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | Admin email
password | false | Admin password

## Admin Sign in 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/signin/Admin'

# POST 요청 보내기
data = {
    "email":"admin@email.com",
    "password":"password"
}

response = requests.post(url, json=data)
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
    "_id": {
        "$oid": "63894ed9390843c9e175c20b"
    },
    "email": "jsmsumin2@integrit.ai",
    "password": "1234",
    "role": "일반관리자",
    "phoneNumber": "12341234",
    "adminName": "장수민2",
    "adminId": "63894ed9390843c9e175c20b",
    "createAt": "2022-12-13 09:50:41",
    "adminProfile": "{\"success\": \" \", \"login\": \" \", \"owner_id\": \" \", \"user\": {\"user_id\": \" \", \"profile\": {\"name\": \" \", \"profile_img\": \" \", \"owner_id\": \" \"}}, \"group_info\": {\"name\": \" \", \"address\": \" \", \"profile_img\": \" \"}, \"robot_list\": [{\"robot_id\": \" \", \"map_id\": \" \", \"port\": \" \"}], \"map_list\": [{\"id\": \" \", \"name\": \" \"}]}"
}
```

### HTTP Request

`POST https://dev.flyinglet.com/signin/Admin`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | Admin email
password | false | Admin password

## Admin Sign in 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/signin/Admin'

# POST 요청 보내기
data = {
    "email":"admin@email.com",
    "password":"password"
}

response = requests.post(url, json=data)
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
    "_id": {
        "$oid": "63894ed9390843c9e175c20b"
    },
    "email": "jsmsumin2@integrit.ai",
    "password": "1234",
    "role": "일반관리자",
    "phoneNumber": "12341234",
    "adminName": "장수민2",
    "adminId": "63894ed9390843c9e175c20b",
    "createAt": "2022-12-13 09:50:41",
    "adminProfile": "{\"success\": \" \", \"login\": \" \", \"owner_id\": \" \", \"user\": {\"user_id\": \" \", \"profile\": {\"name\": \" \", \"profile_img\": \" \", \"owner_id\": \" \"}}, \"group_info\": {\"name\": \" \", \"address\": \" \", \"profile_img\": \" \"}, \"robot_list\": [{\"robot_id\": \" \", \"map_id\": \" \", \"port\": \" \"}], \"map_list\": [{\"id\": \" \", \"name\": \" \"}]}"
}
```

### HTTP Request

`POST https://dev.flyinglet.com/signin/Admin`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | Admin email
password | false | Admin password

## Admin Sign in 

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/signin/Admin'

# POST 요청 보내기
data = {
    "email":"admin@email.com",
    "password":"password"
}

response = requests.post(url, json=data)
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
    "_id": {
        "$oid": "63894ed9390843c9e175c20b"
    },
    "email": "jsmsumin2@integrit.ai",
    "password": "1234",
    "role": "일반관리자",
    "phoneNumber": "12341234",
    "adminName": "장수민2",
    "adminId": "63894ed9390843c9e175c20b",
    "createAt": "2022-12-13 09:50:41",
    "adminProfile": "{\"success\": \" \", \"login\": \" \", \"owner_id\": \" \", \"user\": {\"user_id\": \" \", \"profile\": {\"name\": \" \", \"profile_img\": \" \", \"owner_id\": \" \"}}, \"group_info\": {\"name\": \" \", \"address\": \" \", \"profile_img\": \" \"}, \"robot_list\": [{\"robot_id\": \" \", \"map_id\": \" \", \"port\": \" \"}], \"map_list\": [{\"id\": \" \", \"name\": \" \"}]}"
}
```

### HTTP Request

`POST https://dev.flyinglet.com/signin/Admin`


### Body(Json)

Parameter | Default | Description
--------- | ------- | -----------
email | false | Admin email
password | false | Admin password


## Get Robots collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Robots'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "6389a31716beaa76e42a2821"
        },
        "profile_id": "6389a37016beaa76e42a284c",
        "createAt": "2022-11-01",
        "agentID": " d6456517-3e13-47fd-878b-4e567e5d70f3",
        "alias": " ",
        "location_id": " ",
        "model_id": " ",
        "offStateCustomImgUrl": " ",
        "onStateCustomImgUrl": " "
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Users`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Get Robots collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Robots'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "6389a31716beaa76e42a2821"
        },
        "profile_id": "6389a37016beaa76e42a284c",
        "createAt": "2022-11-01",
        "agentID": " d6456517-3e13-47fd-878b-4e567e5d70f3",
        "alias": " ",
        "location_id": " ",
        "model_id": " ",
        "offStateCustomImgUrl": " ",
        "onStateCustomImgUrl": " "
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Users`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Get Robots collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Robots'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "6389a31716beaa76e42a2821"
        },
        "profile_id": "6389a37016beaa76e42a284c",
        "createAt": "2022-11-01",
        "agentID": " d6456517-3e13-47fd-878b-4e567e5d70f3",
        "alias": " ",
        "location_id": " ",
        "model_id": " ",
        "offStateCustomImgUrl": " ",
        "onStateCustomImgUrl": " "
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Users`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Get Robots collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Robots'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "6389a31716beaa76e42a2821"
        },
        "profile_id": "6389a37016beaa76e42a284c",
        "createAt": "2022-11-01",
        "agentID": " d6456517-3e13-47fd-878b-4e567e5d70f3",
        "alias": " ",
        "location_id": " ",
        "model_id": " ",
        "offStateCustomImgUrl": " ",
        "onStateCustomImgUrl": " "
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Users`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Get Robots collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Robots'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "6389a31716beaa76e42a2821"
        },
        "profile_id": "6389a37016beaa76e42a284c",
        "createAt": "2022-11-01",
        "agentID": " d6456517-3e13-47fd-878b-4e567e5d70f3",
        "alias": " ",
        "location_id": " ",
        "model_id": " ",
        "offStateCustomImgUrl": " ",
        "onStateCustomImgUrl": " "
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Users`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Get Robots collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Robots'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "6389a31716beaa76e42a2821"
        },
        "profile_id": "6389a37016beaa76e42a284c",
        "createAt": "2022-11-01",
        "agentID": " d6456517-3e13-47fd-878b-4e567e5d70f3",
        "alias": " ",
        "location_id": " ",
        "model_id": " ",
        "offStateCustomImgUrl": " ",
        "onStateCustomImgUrl": " "
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Users`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Get Robots collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Robots'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "6389a31716beaa76e42a2821"
        },
        "profile_id": "6389a37016beaa76e42a284c",
        "createAt": "2022-11-01",
        "agentID": " d6456517-3e13-47fd-878b-4e567e5d70f3",
        "alias": " ",
        "location_id": " ",
        "model_id": " ",
        "offStateCustomImgUrl": " ",
        "onStateCustomImgUrl": " "
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Users`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Get Robots collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Robots'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "6389a31716beaa76e42a2821"
        },
        "profile_id": "6389a37016beaa76e42a284c",
        "createAt": "2022-11-01",
        "agentID": " d6456517-3e13-47fd-878b-4e567e5d70f3",
        "alias": " ",
        "location_id": " ",
        "model_id": " ",
        "offStateCustomImgUrl": " ",
        "onStateCustomImgUrl": " "
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Users`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Get Robots collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Robots'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "6389a31716beaa76e42a2821"
        },
        "profile_id": "6389a37016beaa76e42a284c",
        "createAt": "2022-11-01",
        "agentID": " d6456517-3e13-47fd-878b-4e567e5d70f3",
        "alias": " ",
        "location_id": " ",
        "model_id": " ",
        "offStateCustomImgUrl": " ",
        "onStateCustomImgUrl": " "
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Users`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


## Get Robots collection

```python
import requests

# URL 
url = 'https://dev.flyinglet.com/Robots'

# GET 요청 보내기
response = requests.get(url)

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
        "_id": {
            "$oid": "6389a31716beaa76e42a2821"
        },
        "profile_id": "6389a37016beaa76e42a284c",
        "createAt": "2022-11-01",
        "agentID": " d6456517-3e13-47fd-878b-4e567e5d70f3",
        "alias": " ",
        "location_id": " ",
        "model_id": " ",
        "offStateCustomImgUrl": " ",
        "onStateCustomImgUrl": " "
    }
]
```

`Authorization: meowmeowmeow`

<aside class="notice">

You must replace <code>meowmeowmeow</code> with your personal Access token.

</aside>


### HTTP Request

`GET https://dev.flyinglet.com/Users`


### Path Parameters

Path의 '{{id}}'와 collection 내 '_id' 의 값이 일치하는 document 조회

`GET ~/{{id}}`

Parameter | Default | Description
--------- | ------- | -----------
id | false | DB에 저장된 '_id' 값.


[//]: # (Parameter | Default | Description)

[//]: # (--------- | ------- | -----------)

[//]: # (include_cats | false | If set to true, the result will also include cats.)

[//]: # (available | true | If set to false, the result will include kittens that have already been adopted.)

[//]: # ()
[//]: # (<aside class="success">)

[//]: # (Remember — a happy kitten is an authenticated kitten!)

[//]: # (</aside>)

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

