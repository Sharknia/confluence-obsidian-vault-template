# Confluence Obsidian Vault Template

Confluence Obsidian Sync 플러그인이 포함된 Obsidian vault template입니다.

Template version: `0.0.3`

## 시작

1. 이 저장소를 ZIP으로 내려받거나 clone합니다.
2. Obsidian에서 이 폴더를 vault로 엽니다.
3. `Settings > Community plugins`에서 Restricted mode를 끄고 `Confluence Obsidian Sync`를 활성화합니다.
4. 플러그인 설정에서 Confluence base URL, Atlassian account email, API token을 입력합니다.
5. 왼쪽 리본 아이콘 또는 명령 팔레트의 `Open Sync Panel`을 실행합니다.
6. Root content URL 기본값 `https://selta.atlassian.net/wiki/spaces/IS/folder/23167000`을 확인하고 프로젝트를 생성한 뒤 `Pull Tree`를 실행합니다.

## 플러그인 업데이트와 터미널

Sync Panel의 `터미널 열기`는 이 vault 루트를 작업 폴더로 터미널을 엽니다.

Sync Panel의 `플러그인 업데이트`는 GitHub 최신 Release에서 플러그인 실행 파일만 교체합니다. `.obsidian/plugins/confluence-obsidian-sync/data.json`에 저장된 설정은 덮어쓰지 않습니다.

업데이트 후에는 Obsidian을 다시 시작하거나 플러그인을 다시 로드하세요.

## Git에 올리지 않는 항목

- `.obsidian/plugins/confluence-obsidian-sync/data.json`
- `.env`
- `confluence/` 안의 Pull 산출물
- `logs/` 안의 Pull 로그
- `.confluence-sync/` 안의 개인 설정, 인증 정보, 프로젝트 상태
- `graphify-out/` 안의 graphify 분석 산출물

## 폴더

- `confluence/`: Confluence Markdown 작업 사본
- `logs/`: 최근 Pull 결과 상세 로그
- `.confluence-sync/trash/`: 안전 삭제된 문서 보관 위치
- `graphify-out/`: 선택 설치한 graphify CLI 분석 결과

자세한 첫 실행 순서는 `처음 시작하기.md`를 확인하세요.
