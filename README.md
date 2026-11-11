# 스킨랩코리아 홈페이지 (자체 호스팅)

큐샵(qshop.ai)에서 운영하던 www.skinlabkorea.com 을 정적 사이트로 다시 만든 것입니다.

## 폴더 구성

| 경로 | 내용 |
|---|---|
| `site/` | 실제로 배포하는 사이트 (이 폴더만 올리면 됨) |
| `site/index.html` | 메인 |
| `site/company/index.html` | 회사소개 (비전, 연혁, 시설) |
| `site/brand/index.html` | 브랜드 BASUP |
| `site/assets/` | 스타일(`style.css`), 스크립트(`main.js`), 이미지(`img/`) |
| `_backup_qshop/` | 큐샵 원본 백업 (원본 이미지 36장, 페이지 HTML). **배포하지 않음** |

## 수정하는 법

- 글 수정: 해당 페이지의 `index.html`을 열어 문구를 직접 고치면 됩니다.
- 연혁 추가: `site/company/index.html`의 `<ol class="history">` 맨 위에 연도 블록을 하나 복사해서 추가합니다.
- 사진 교체: `site/assets/img/`에 같은 이름의 파일을 덮어쓰면 됩니다. 가로 2000px 이하의 WebP를 권장합니다.
- 내 컴퓨터에서 미리보기: `cd site && python3 -m http.server 8000` 실행 후 http://localhost:8000 접속.

## 배포 (GitHub Pages, 무료)

- 저장소: https://github.com/whdlrghks/skinlabkorea-homepage
- `main` 브랜치에 올리면 `.github/workflows/deploy.yml`이 `site/` 폴더를 자동 배포합니다 (1~2분).
- 수정 후 반영: `git add -A && git commit -m "내용" && git push`
- GitHub 웹사이트에서 파일을 직접 고쳐도 자동 반영됩니다.
- `_backup_*` 폴더는 `.gitignore`로 제외되어 이 컴퓨터에만 있습니다. **따로 백업해 두세요.**

## 도메인 연결 (메일 끊김 주의)

현재 도메인 DNS는 큐샵의 AWS 네임서버에 있으므로 가비아 DNS로 되돌리면서 설정합니다.

1. 가비아 → My가비아 → 도메인 관리 → skinlabkorea.com → **네임서버를 가비아 기본 네임서버로 변경**
2. 가비아 **DNS 관리**에서 레코드 입력

   | 타입 | 호스트 | 값 | 우선순위 |
   |---|---|---|---|
   | MX | @ | aspmx.daum.net. | 10 |
   | MX | @ | alt.aspmx.daum.net. | 20 |
   | CNAME | www | whdlrghks.github.io. | |
   | A | @ | 185.199.108.153 | |
   | A | @ | 185.199.109.153 | |
   | A | @ | 185.199.110.153 | |
   | A | @ | 185.199.111.153 | |

   → **MX 두 줄이 없으면 회사 메일(ikhwancho@skinlabkorea.com) 수신이 끊깁니다.**
3. GitHub 저장소 → Settings → Pages → Custom domain에 `www.skinlabkorea.com` 입력 → 확인 후 **Enforce HTTPS** 체크
4. 몇 시간~하루 뒤 확인할 것:
   - https://skinlabkorea.com, https://www.skinlabkorea.com 접속
   - 외부 메일(Gmail 등)에서 회사 메일로 테스트 메일 보내서 수신 확인
5. 며칠 동안 이상이 없으면 **큐샵 해지**

## 연간 비용

- 호스팅: 0원 (GitHub Pages 무료)
- 도메인: 가비아 연장비만 발생 (만료일 2027-11-15)
