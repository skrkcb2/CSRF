# CSRF
### 특징: 사용자 인증(세션, 토큰)이 완료 되고, 공격 백엔드의 함수의 모든 구조를 파악 완료 후, 사용자가 의도하지 않은 요청을 보내는 취약점  
### 공격 예시  
#### 1. 공격자가 원하는 동작의 API 요청 폼 제작(사용자 세션을 통해 게시판 입력 / POST요청)  
![image](https://github.com/user-attachments/assets/7be0885d-0e55-4594-9197-b8c01cf25017)
#### 2. 공격자 요청 폼의 url 짧게 변경  
![image](https://github.com/user-attachments/assets/a28ae90a-183b-4eaa-8cbb-5dbf23e8b824)
#### 3. 공격 화면  
#### 3.1 환경 설정 (사용자 도메인: backend.local, 공격자 도메인: front.local, 쿠키 설정: SameSite: none, Secure, HttpOnly)  
![image](https://github.com/user-attachments/assets/50c1c817-6756-4e7c-80ac-c72e7998de0f)
![csrf_none](https://github.com/user-attachments/assets/3e3f04a4-a339-4422-a174-d0bcf9073f1c)
#### 해당의 경우는 쿠키 설정을 통해 다른 도메인으로 쿠키가 전송되는 설정을 세팅하여 악성 폼 작동합니다.
#### 3.2 환경 설정 (사용자 도메인: backend.local, 공격자 도메인: front.local, 쿠키 설정: SameSite: Lax/Strict, Secure, HttpOnly)  
![image](https://github.com/user-attachments/assets/29380462-6193-4936-ba66-0eb966967640) ![image](https://github.com/user-attachments/assets/a625f1c9-2ed5-4445-8bdb-302733612692)  
![csrf_strict](https://github.com/user-attachments/assets/0b223808-9299-41ed-a1bd-de1e019fd4e1)
#### 해당의 경우는 쿠키 설정을 통해 다른 도메인으로 쿠키가 전송되지 않게 설정을 세팅하여 악성 폼 작동합니다(Strict) / + Lax 또한 결과는 같지만 GET 요청은 허용합니다 유의!  
### 보안 설정  
#### 1. 올바른 쿠키 설정 
#### 위에서 보다시피 쿠키의 설정에 따라 타 도메인에 쿠키를 허용하는냐(None)?, 아니면 같은 도메인만 허용 하느냐(Strict)?,또는 타 도메인에 GET 요청 만 허용 하느냐(Lax)?
#### 2. Referer 헤더 검증
#### 아래 이미지를 보면 각 요청에 Referer 헤더가 존재하는 것을 볼수 있다. 
![image](https://github.com/user-attachments/assets/3cf846a5-23fa-4f63-8edc-9aadb6511886)
#### 이미지를 보아하면 https://front.local:3001에서의 요청을 보낸것을 확인 할 수 있으며 기존 Insert API 의 경우는 https://backend.local:8443 에서 실행 된다. 그러하여 해당 내용을 api 로직에 추가 하면 된다.






 

