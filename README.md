# Confluence Obsidian Vault Template

Confluence Obsidian Sync 플러그인이 포함된 Obsidian vault template입니다.

Template version: `0.0.4`

Plugin / CLI version: `0.1.64`

## 시작

1. 이 저장소를 ZIP으로 내려받거나 clone합니다.
2. Obsidian에서 이 폴더를 vault로 엽니다.
3. `Settings > Community plugins`에서 Restricted mode를 끄고 `Confluence Obsidian Sync`를 활성화합니다.
4. 플러그인 설정에서 Confluence base URL, Atlassian account email, API token을 입력합니다.
5. 왼쪽 리본 아이콘 또는 명령 팔레트의 `Open Sync Panel`을 실행합니다.
6. Root content URL 기본값 `https://selta.atlassian.net/wiki/spaces/IS/folder/23167000`을 확인하고 `Pull Tree`를 실행합니다. 필요한 프로젝트는 Pull 실행 중 자동으로 생성됩니다.

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

- `cli/confluence-sync-cli.tgz`: 사용자 전역 CLI 설치 패키지
- `confluence/`: Confluence Markdown 작업 사본
- `logs/`: 최근 Pull 결과 상세 로그
- `.confluence-sync/trash/`: 안전 삭제된 문서 보관 위치
- `graphify-out/`: 선택 설치한 graphify CLI 분석 결과

자세한 첫 실행 순서는 `처음 시작하기.md`를 확인하세요.


## Obsidian 없이 동기화하기

Node.js 22 이상, npm, 사용자 전용 npm 전역 설치 경로가 필요합니다. Node가 없다면 [Node 공식 설치 안내](https://nodejs.org/en/download)를 확인하세요. Obsidian만 사용할 때는 Node 설치가 필요하지 않습니다.

먼저 `npm prefix --global`로 현재 Node/npm의 설치 위치를 확인하세요. 사용자 전용 경로여야 합니다. macOS·Linux는 `<prefix>/bin`, Windows는 `<prefix>`가 PATH에 있어야 합니다. 공유 설치 경로에 쓰기 권한이 있다는 것만으로 사용자 전용 설치가 되는 것은 아닙니다. [npm 경로 설명](https://docs.npmjs.com/cli/v11/configuring-npm/folders/)을 참고하세요.

받은 vault 폴더에서 다음 한 줄을 실행합니다. 코드 저장소 clone·빌드나 Obsidian 실행은 필요하지 않습니다.

```bash
npm install --global --engine-strict ./cli/confluence-sync-cli.tgz
```

설치 후 다른 작업 폴더에서도 사용할 수 있습니다. 설치한 vault를 기본 대상으로 저장하지 않으므로 명령마다 `--vault`를 지정합니다.

```bash
confluence-sync --version
confluence-sync --help
confluence-sync check --vault '/절대/경로/vault'
confluence-sync status --vault '/절대/경로/vault'
confluence-sync pull-tree --vault '/절대/경로/vault'
confluence-sync pull-page --vault '/절대/경로/vault' --file 'confluence/프로젝트/문서.md'
confluence-sync push-page --vault '/절대/경로/vault' --file 'confluence/프로젝트/문서.md' --yes
```

Windows PowerShell에서도 같은 설치 명령을 사용하며 vault 경로는 `--vault 'C:\Users\사용자\Documents\vault'`처럼 지정합니다.

기존 vault의 `.obsidian/plugins/confluence-obsidian-sync/data.json`에 있는 인증·프로젝트 설정을 그대로 읽고 수정하지 않습니다. CLI로 `init`한 프로젝트는 결과의 `project.localFolderPath`를 `--project`로 지정하세요.

### 업데이트·제거와 설치 문제

새 vault 배포에서 받은 `.tgz`에 같은 설치 명령을 실행하고 `confluence-sync --version`으로 버전을 확인합니다. 전역 CLI는 vault와 독립된 복사본이며, Obsidian의 플러그인 업데이트 버튼은 CLI를 업데이트하지 않습니다.

```bash
npm install --global --engine-strict ./cli/confluence-sync-cli.tgz
confluence-sync --version
npm uninstall --global confluence-obsidian-sync-cli
```

제거해도 vault의 설정·Markdown·백업·로그는 유지됩니다.

- `EBADENGINE`: Node 22 이상으로 실행하세요.
- `EACCES`·`EPERM`: [npm 공식 권한 오류 안내](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally/)에 따라 사용자 전용 Node/npm 환경과 설치 경로를 준비하세요. 관리자 권한·`sudo`·광범위한 `chmod`로 우회하지 마세요.
- 설치 후 명령을 찾지 못함: `npm prefix --global`의 실행 경로가 PATH에 있는지 확인하고 새 터미널을 여세요.
- `EEXIST`: 같은 이름의 명령이 있습니다. 원래 프로그램을 확인하세요. `--force`로 덮어쓰지 마세요.
- Node 버전 관리자로 runtime을 바꿈: 전역 설치 경로가 달라질 수 있으므로 받은 패키지로 다시 설치하세요.

설치 스크립트는 shell 설정이나 npm prefix를 자동 변경하지 않습니다. 설치물에 runtime 의존성을 동봉하므로 설치 시 별도 빌드·의존성 다운로드는 없습니다. macOS에서 설치·실행을 검증했으며 Linux·Windows는 CI 검증 대상으로 두고 결과 확인 전입니다.

### Obsidian 없이 처음 연결하기

호출 환경에 `CONFLUENCE_BASE_URL`(HTTPS 사이트 주소), `CONFLUENCE_USER_EMAIL`(Atlassian 계정 이메일), `CONFLUENCE_API_TOKEN`을 설정합니다. 토큰은 명령 인자에 넣지 않고 Git에 저장하지 마세요. 환경변수는 기존 설정의 연결 필드만 덮어쓰며 CLI가 저장하지 않습니다.

```bash
confluence-sync init --vault '/절대/경로/vault' --root 'https://example.atlassian.net/wiki/spaces/SPACE/pages/123'
confluence-sync pull-tree --vault '/절대/경로/vault' --project 'confluence/프로젝트'
```

`init` 결과의 `project.localFolderPath`를 `--project`에 사용합니다. 페이지와 폴더 루트 URL을 지원합니다. 기존 문서 한 개만 Push할 수 있으며 위험한 작업에는 `--yes`가 필요합니다. JSON 결과·종료 코드·부분 실패 복구는 [플러그인 README](https://github.com/Sharknia/confluence-obsidian-sync#json-결과와-복구)를 확인하세요.

업데이트된 플러그인과 CLI는 `.confluence-sync/operation.lock`을 공유합니다. 동기화 중 같은 파일을 다른 에디터에서 동시에 편집하지 마세요.
