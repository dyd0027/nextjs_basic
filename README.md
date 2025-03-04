# nextjs_basic

next.js
### 환경설정
- 어떤 기술로 만들어졌는지 확인하는 크롬 extention: wappalyzer
- yarn
	- yarn버전 업데이트: yarn set version stable
	- yarn버전 확인: yarn -v
- node
	- node버전 확인: node -v
	- node버전 업데이트(윈도우): 그냥 공식 홈페이지서 다운받기
- 설치방법: npx create-next-app@latest

### 2.4 CSR특징, 장/단점
- 리엑트만 사용했을 때인 CSR(Client(브라우저) Side Rendering): 서버측에서 html(비어있음: js로 코드가 구현되어 있으니깐), 라이브러리, js코드를 다운받고 Client(브라우저)측에서 랜더링 시켜줌.
	- 장점
		1. 한 번만 로딩 되면, 빠른 UX 제공 -> fetch를 사용해서 부분적으로 랜더링가능
		2. 서버의 부하가 적음
	- 단점
		1. 페이지 로딩 시간이 길다.
		2. js활성화 필수임.
		3. 서버에 갔다와야해서 보안에 취야함.
		4. CDN(한국에서 미국까지의 데이터 왔다갔다 오래걸리니 일본에 들렸다가 없으면 일본에서 다시 미국으로..그리고 일본에는 캐시가 남게됨)에 캐시가 안됨.
		-> 의 해결책: SSG, ISR

### 2.6 SSG 특징, 장/단점
- CSR의 단점을 개선함 SSG(Static Site Generation): 서버측에서 빌드 될 때 랜더링함
	- 장점
		1. 페이지 로딩 시간이 빠르다.
		2. 자바스크립트 필요 없음.
		3. 보안이 좋음.
		4. CDN 캐시 가능
	- 단점
		1. 데이터가 정적임
		2. 사용자별 정보 제공의 어려움 -> 모든사용자한테 정적인 데이터일 때 굉장히 유리함.
		-> 의 해결책: ISR
		
### 2.7 ISR 특징, 장/단점
- SSG단점을 개선함 ISR(Incremental Static Regeneration: 서버측에서 주기적으로 랜더링함
- SSG와 동일한 원리이지만 정해진 주기에 따라 페이지를 다시 생성함.
	- 장점: SSG의 장점 + 데이터가 주기적으로 업데이트
	- 단점
		1. 실시간 데이터가 아님
		2. 사용자별 정보 제공이 어려움
		-> 의 해결책: ISR
		
### 2.7 SSR 특징, 장/단점
- SSR(Server Side Rendering): 서버측에서 요청시 랜더링함
	- 장점: SSG장점 + 실시간 데이터 사용자 + 사용자별 데이터
	- 단점
		1. 비교적 느릴 수 있음.
		2. 서버의 과부화 걸릴 수 있음.
		3. CDN캐시가 안됨.
	- 정적인 html을 먼저 보여주고 그 뒤에 js를 다운받아 실행함
		- 그래서 그 사이의 간격(TTI: Time to Interact)을 줄이는게 중요포인트
### nextjs는 ISR, SSG, SSR/CSR(심지어 한 페이지에서도 가능), CSR을 혼합해서 사용가능 -> 성능좋게 만들기 위해서

### 2.12 환경에 따른 개발방법
- 로그인이 필요: CSR, SSR, hybrid
- 로그인 필요 x
	- 데이터 변경 x: SSG
	- 데이터가 변경
		- 빈도수가 자주: SSG, CSR
		- 빈도수가 별루: ISR
		
### 4.4 정적 라우팅(버전13)
- 페이지를 만들고 싶으면 app폴더안에 각각 폴더를 만들고 그 안에 page.tsx를 만들어 주면 됨.

### 4.7 빌드 결과 분석 해보기
- npm run dev: SSR로 되기 때문에 모든 페이지가 요청과 함께 compile되어서 오래걸림
- build -> start: html파일은 ssg로 js는 ssr로 되기때문에 요청과 함께 html이 즉각 반응 됨.
