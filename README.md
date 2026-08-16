# 트레일러(Trailer) 공식 웹사이트

기차 여행 앱 **트레일러**의 서비스 소개 및 법적 고지 게시용 정적 웹사이트입니다.
빌드 도구나 백엔드 없이 HTML / CSS / JS 파일만으로 동작합니다.

## 페이지 구성

| 경로 | 파일 | 설명 |
| --- | --- | --- |
| `/` | `index.html` | 랜딩 — 히어로, 핵심 기능, 실시간 알림(`#alerts`), 이용 흐름 3단계, CTA, 문의 |
| `/features/` | `features/index.html` | 기능별 상세 소개 (앵커 10종) |
| `/privacy/` | `privacy/index.html` | 개인정보처리방침 (본문 placeholder) |
| `/terms/` | `terms/index.html` | 이용약관 (본문 placeholder) |
| `/location-terms/` | `location-terms/index.html` | 위치기반서비스 이용약관 (본문 placeholder) |
| `/delete-account/` | `delete-account/index.html` | 계정 삭제 안내 (Google Play 데이터 삭제 정책 대응, 본문 작성 완료) |
| — | `404.html` | 404 페이지 |

공통 자산: `assets/css/style.css`, `assets/js/main.js`, `assets/img/*.svg`

## 로컬 미리보기

모든 링크가 **루트 기준 절대경로**(`/privacy/` 등)라 파일을 직접 여는 방식(`file://`)으로는
페이지 이동이 되지 않습니다. 간단한 로컬 서버로 확인하세요.

```bash
# 프로젝트 루트에서
python -m http.server 5173
# → http://localhost:5173
```

## 배포

정적 호스팅(Netlify, Vercel, Cloudflare Pages, GitHub Pages 등)에 루트 디렉터리를 그대로 업로드하면 됩니다.
빌드 명령 없음 / 퍼블리시 디렉터리는 프로젝트 루트입니다.

> GitHub Pages를 **하위 경로**(`user.github.io/repo/`)에 배포할 경우 절대경로 링크가 깨집니다.
> 커스텀 도메인 또는 루트 배포를 사용하거나, `/` 로 시작하는 경로를 상대경로로 바꿔야 합니다.

## 교체해야 할 placeholder 목록

모든 교체 지점은 소스에 `[교체 위치]` 주석으로 표시해 두었습니다.

### 1. 이미지
| 파일 | 용도 | 상태 | 권장 규격 |
| --- | --- | --- | --- |
| `assets/img/TLogo.png` | 로고 원본 (흰색 마크 · 투명 배경, 704×752) | 확정 | — |
| `assets/img/logo-icon.png` | 앱 아이콘 (헤더 · 푸터 · 파비콘 공용) | 확정 · `TLogo.png` 로 생성 | 512×512 PNG |
| `assets/img/screen-home.svg` | 히어로 대표 화면 (홈) | 실제 화면 기준 목업 | 1080×2340 PNG |
| `assets/img/screen-plan.svg` | 여행 상세 · 타임라인 화면 | 실제 화면 기준 목업 | 1080×2340 PNG |
| `assets/img/screen-scenery.svg` | 알림 화면 (창밖 풍경 · 일정 알림) | 실제 화면 기준 목업 | 1080×2340 PNG |
| `assets/img/screen-video.svg` | 여행 영상(릴스) 화면 | 실제 화면 기준 목업 | 1080×2340 PNG |
| `assets/img/screen-place.svg` | 테마별 여행지 화면 | 실제 화면 기준 목업 | 1080×2340 PNG |
| `assets/img/screen-place-detail.svg` | 장소 상세 화면 | 실제 화면 기준 목업 | 1080×2340 PNG |
| `assets/img/screen-ai.svg` | AI 일정 추천 (플랜 A·B·C) 화면 | 실제 화면 기준 목업 | 1080×2340 PNG |
| `assets/img/screen-ticket.svg` | 승차권 화면 (DAY별 카드) | 실제 화면 기준 목업 | 1080×2340 PNG |
| `assets/img/og-image.png` | SNS 공유 이미지 | 확정 | 1200×630 PNG |

> `screen-` 으로 시작하는 파일 중 "실제 화면 기준 목업"은 운영 중인 앱 화면을 SVG 로 옮긴 것입니다.
> 실제 스크린샷 PNG 로 바꿀 때는 파일을 추가한 뒤 각 HTML 의 `src` 확장자만 `.png` 로 변경하면 됩니다.

> `TLogo.png` 는 흰색 마크에 배경이 없어 흰 바탕에서는 보이지 않습니다. 그래서 브랜드 배경(`#5E84F4`)과
> 둥근 모서리를 입힌 `logo-icon.png` 를 만들어 헤더 · 푸터 · 파비콘 · apple-touch-icon 에 사용합니다.
> 로고를 교체할 때는 `TLogo.png` 를 새 파일로 바꾼 뒤 `logo-icon.png` 를 다시 생성하세요.
>
> 로고 텍스트 "트레일러"는 이미지가 아닌 텍스트로 렌더링됩니다.
> 워드마크 이미지로 바꾸려면 각 페이지의 `.logo__text` 를 `<img>` 로 교체하세요.

### 2. 도메인 — 반영 완료
현재 도메인: **`https://trailer-sage.vercel.app`** (Vercel 프로덕션)

커스텀 도메인을 붙이면 아래 위치를 일괄 치환하세요. (총 32곳)
- 각 HTML 의 `<link rel="canonical">`, `og:url`, `og:image`, `twitter:image`
- `robots.txt`, `sitemap.xml`

> Vercel 의 배포별 URL(`trailer-xxxxx-....vercel.app`)은 배포마다 바뀌므로 절대 쓰지 마세요.
> 항상 최신 배포를 가리키는 프로덕션 도메인만 사용합니다.

### 3. Google Play 스토어 URL
`https://play.google.com/store/apps/details?id=com.trailer.app` 의 패키지명을 실제 값으로 변경합니다.
공식 Google Play 배지 이미지를 쓰려면 `.btn--store` 링크 내부를 배지 `<img>` 로 교체하세요.

### 4. 법적 문서 본문

| 페이지 | 상태 |
| --- | --- |
| `terms` (이용약관) | **본문 게시 완료** · 시행일 2026. 08. 16. |
| `location-terms` (위치기반서비스 이용약관) | **본문 게시 완료** · 시행일 2026. 08. 16. |
| `privacy` (개인정보처리방침) | **본문 게시 완료** · 공고·시행일 2026. 08. 16. |

세 페이지 본문은 각각 `legal-export/md/` 의 `service.md` · `location.md` · `privacy.md` 를 기준으로 옮겼습니다.
개정할 때는 해당 md 를 먼저 갱신한 뒤 HTML 에 반영하고, `doc-hero__meta` 의 날짜도 함께 수정하세요.

(`marketing.md` 는 앱 내 마케팅 활용동의 화면용으로, 현재 웹사이트에 대응 페이지가 없습니다.)

### 5. 계정 삭제 안내
`delete-account/index.html` 은 본문이 작성되어 있습니다. 아래 두 곳만 운영 기준에 맞춰 확인하세요.
- 법령상 보관 항목 · 보관 기간 표 행 (보관 항목이 없으면 행 삭제)
- 이메일 삭제 요청 처리 기간 (기본값: 영업일 기준 7일)

## 브랜드 토큰

`assets/css/style.css` 의 `:root` 에서 한 번에 관리합니다.

| 토큰 | 값 | 용도 |
| --- | --- | --- |
| `--brand` | `#5E84F4` | 메인 블루 |
| `--mint` | `#81E4D0` | 포인트 민트 |
| `--bg-soft` | `#F1F4FB` | 배경 보조색 |
| `--ink` | `#21262F` | 본문 텍스트 |

폰트는 Pretendard Variable(jsDelivr CDN, dynamic-subset)을 사용합니다.

## 사업자 정보

상호 트레일러 · 대표 장윤영 · 사업자등록번호 566-32-01795
서울특별시 강서구 허준로 23 · 2026trailer@gmail.com
