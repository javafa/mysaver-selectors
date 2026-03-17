# MySaver Remote Selectors

MySaver Chrome Extension이 사용하는 DOM 셀렉터 설정 파일입니다.

## 구조

```
selectors/
  manifest.json      ← 버전 인덱스 (익스텐션이 이것만 먼저 fetch)
  youtube.json       ← YouTube 셀렉터
  instagram.json     ← Instagram 셀렉터
  pinterest.json     ← Pinterest 셀렉터
  tiktok.json        ← TikTok 셀렉터
```

## 브랜치 전략

| 브랜치 | 용도 |
|--------|------|
| `dev` | 개발/테스트용. 익스텐션 dev 모드에서 참조 |
| `main` | 프로덕션용. 익스텐션 prod 모드에서 참조 |

셀렉터 수정 → `dev`에서 테스트 → 확인 후 `main`으로 merge

## 업데이트 방법

1. 해당 플랫폼 JSON 파일의 셀렉터 수정
2. `manifest.json`에서 해당 플랫폼의 `version` 값 +1, `updatedAt` 갱신
3. `dev` 브랜치에 push → 익스텐션 dev 모드로 테스트
4. 확인 후 `main`으로 merge

## 동작 원리

- **수집 버튼 클릭 시**: `manifest.json` fetch → 버전 비교 → 변경된 플랫폼만 JSON fetch → `chrome.storage.local` 캐시
- **네트워크 실패 시**: 캐시된 마지막 값 사용
- **캐시도 없을 때**: 익스텐션 번들 기본값 사용
