# BLUE MARKET — GitHub + Render 배포 안내 (수정판)

이 프로젝트는 Node.js + Express + Socket.IO 웹 서비스입니다.

## 중요: 폴더 구조

GitHub 저장소 **루트**에 아래가 보여야 합니다.

```
package.json
server.js
render.yaml
public/
  index.html
  app.js
  style.css
  (이미지 파일들)
```

`public` 폴더 안의 파일을 루트에 풀지 마세요.  
(이전에 루트에 index.html 등이 있으면 서버가 404를 냅니다.)

## 1. GitHub에 올리기 (가장 쉬운 방법)

1. GitHub에서 **New repository** → 이름 예: `commerce-game` (또는 새로 만들기)
2. 아래 중 하나 선택:

### 방법 A — 웹에서 업로드
- 저장소 페이지에서 **Add file → Upload files**
- `blue_market_fixed` 폴더 **안의 모든 파일과 public 폴더**를 드래그해서 업로드
- `package.json`과 `server.js`가 저장소 첫 화면에 보이면 성공

### 방법 B — 기존 저장소 정리 후 다시 올리기
현재 `commerce-game` 저장소에 public 없이 파일이 루트에 올라가 있다면:
1. 저장소에서 잘못 올라간 `index.html`, `app.js`, `style.css`, 이미지 파일들을 삭제
2. `public` 폴더를 새로 만들고 그 안에 다시 업로드

## 2. Render에 배포

### 추천: Blueprint 사용
1. https://dashboard.render.com 로그인
2. **New + → Blueprint**
3. GitHub 저장소 연결
4. Render가 `render.yaml`을 읽으면 계속 진행
5. 환경변수 `ADMIN_PIN` 값을 입력 (기본값 유지하려면 `0403`)
6. 배포 완료 후 나오는 `https://xxxx.onrender.com` 주소로 접속

### 수동으로 Web Service 만들기
1. **New + → Web Service**
2. GitHub 저장소 연결
3. 설정:
   - **Root Directory**: 비워두기 (루트)
   - **Runtime**: Node
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Instance Type**: Free
4. Environment:
   - `ADMIN_PIN` = `0403` (원하는 비밀번호)
   - `NODE_ENV` = `production`
5. Create Web Service

## 3. 배포 후 확인

- 배포 로그에서 **Build successful** 과 **Your service is live** 가 나와야 합니다.
- 주소로 접속하면 로그인 화면이 보여야 합니다.
- 관리자 버튼 → PIN 입력 후 게임 시작 가능.

## 4. 주의사항

- 무료 플랜은 약 15분 동안 접속이 없으면 잠자기 모드로 들어가고, 다시 접속하면 30초~1분 정도 걸릴 수 있습니다.
- 무료 플랜에서는 서버가 재시작되면 게임 저장 데이터가 초기화될 수 있습니다. (영구 디스크는 유료)
- 실시간 게임은 **인스턴스 1개**만 사용하세요.
- 게임이 끝나면 ADMIN_PIN을 바꾸거나 서비스를 Suspend 하세요.

## 로컬 테스트

```bash
cd blue_market_fixed
npm install
npm start
```

브라우저에서 http://localhost:3000 접속.
