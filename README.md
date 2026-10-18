# PIC Loss Evaluation Course

Photonic integrated circuit (PIC)의 insertion loss를 측정하고, least squares로 coupling loss, propagation loss, S-bend loss를 분리하는 온라인 강의입니다 (English / 한국어).

강의 전체가 정적 웹페이지 하나입니다: `index.html`과 그림 폴더 `img/`. 수식(MathJax)과 글꼴(Google Fonts)은 인터넷에서 불러오므로, GitHub에서 따로 build할 것은 없습니다.

```
github-page/
├─ index.html     강의 페이지
├─ img/           그림
├─ .nojekyll      GitHub이 파일을 그대로 올리도록 하는 빈 파일
└─ README.md      이 문서
```

---

## 1. GitHub 계정과 repository 만들기 (처음 한 번)

1. https://github.com 에서 계정을 만들고 로그인합니다.
2. 오른쪽 위 **+** → **New repository**를 누릅니다.
3. **Repository name**에 이름을 적습니다 (예: `pic-loss-course`). 이 이름이 웹 주소에 들어갑니다.
4. **Public**을 선택합니다. 무료 계정에서 GitHub Pages를 쓰려면 Public이어야 합니다.
5. "Add a README file" 등은 **체크하지 말고** **Create repository**를 누릅니다.

---

## 2. 파일 올리기

둘 중 편한 방법 하나를 고르세요.

### 방법 A: 웹 브라우저로 올리기 (git 설치 필요 없음, 가장 쉬움)

1. 방금 만든 repository 페이지에서 **uploading an existing file** 링크를 누릅니다
   (이미 파일이 있다면 **Add file → Upload files**).
2. Windows 탐색기에서 `github-page` 폴더를 열고, **안에 있는 것 전부**(`index.html`, `README.md`, `img` 폴더)를 선택해 브라우저 창으로 끌어다 놓습니다.
   - `github-page` 폴더 자체가 아니라 **그 안의 내용**을 올려야 합니다. `index.html`이 repository 맨 위에 있어야 합니다.
   - `.nojekyll`은 숨김 파일이라 탐색기에서 안 보일 수 있습니다. 없어도 이 강의는 정상 동작합니다.
3. 아래 **Commit changes** 버튼을 누릅니다.

**수정한 뒤 다시 올릴 때:** 같은 방법으로 **Add file → Upload files**에 바뀐 파일을 끌어다 놓으면 같은 이름의 파일이 덮어써집니다. 그림을 지운 경우에는 GitHub에서 해당 파일을 열고 휴지통 아이콘(Delete file)으로 지웁니다.

### 방법 B: git 명령어로 올리기

#### B-1. 처음 한 번만 하는 준비

1. https://git-scm.com/download/win 에서 **Git for Windows**를 설치합니다 (설치 옵션은 기본값 그대로).
2. **Git Bash**(또는 PowerShell)를 열고 이름과 이메일을 등록합니다. 이메일은 GitHub 계정 이메일을 쓰세요.

```bash
git config --global user.name "홍길동"
```

```bash
git config --global user.email "you@example.com"
```

#### B-2. 처음 올리기

1. `github-page` 폴더로 이동합니다 (경로에 공백이 있으므로 따옴표를 붙입니다).

```bash
cd "D:/Claude Code/Lecture/PIC Loss Evaluation/github-page"
```

2. 이 폴더를 git 저장소로 만들고, 모든 파일을 기록(commit)합니다.

```bash
git init -b main
```

```bash
git add .
```

```bash
git commit -m "First version of the course"
```

3. GitHub repository와 연결합니다. 주소는 repository 페이지의 초록색 **Code** 버튼에서 HTTPS 주소를 복사해 붙여 넣으세요.

```bash
git remote add origin https://github.com/<사용자명>/<repository이름>.git
```

4. 올립니다.

```bash
git push -u origin main
```

처음 push할 때 GitHub 로그인 창이 뜹니다. 브라우저로 로그인하면 이후에는 다시 묻지 않습니다.

#### B-3. 수정한 뒤 다시 올리기

```bash
cd "D:/Claude Code/Lecture/PIC Loss Evaluation/github-page"
```

```bash
git add -A
```

```bash
git commit -m "Update course"
```

```bash
git push
```

`git add -A`는 새로 생긴 파일, 바뀐 파일, 지워진 파일을 모두 반영합니다.

#### 자주 보는 메시지

| 메시지 | 뜻과 해결 |
|---|:---|
| `nothing to commit, working tree clean` | 바뀐 파일이 없습니다. 강의를 다시 export했는지 확인하세요. |
| `remote origin already exists` | 이미 연결되어 있습니다. B-2의 3번은 건너뛰세요. |
| `failed to push some refs` / `rejected` | GitHub 쪽에 내 컴퓨터에 없는 변경(웹에서 직접 올린 파일 등)이 있습니다. `git pull --rebase origin main`을 실행한 뒤 다시 `git push` 하세요. |
| `Authentication failed` | 로그인이 안 된 상태입니다. 다시 `git push` 하면 로그인 창이 뜹니다. |

방법 A와 B를 섞어 쓰면 위의 `rejected`가 생기기 쉬우니, 한 가지 방법을 정해서 쓰는 것이 좋습니다.

---

## 3. GitHub Pages 켜기 (처음 한 번)

1. repository 페이지에서 **Settings** → 왼쪽 메뉴 **Pages**로 갑니다.
2. **Build and deployment → Source**를 **Deploy from a branch**로 둡니다.
3. **Branch**를 `main`, 폴더를 `/ (root)`로 고르고 **Save**를 누릅니다.
4. 1–2분 뒤 같은 페이지 위쪽에 주소가 표시됩니다:
   `https://<사용자명>.github.io/<repository이름>/`

이후에는 파일을 올릴 때마다 1–2분 안에 사이트가 자동으로 갱신됩니다. 바로 반영되지 않으면 브라우저에서 새로고침(Ctrl+F5)을 해 보세요.

---

## 4. 강의 내용 수정하기

`index.html`을 직접 고치지 마세요. 강의 원본은 `4_Online_Course/` 폴더의 `pic-loss-course.md`(영문)와 `pic-loss-course.ko.md`(한국어)입니다. 원본을 고친 뒤 아래 두 명령을 실행하면 이 `github-page` 폴더가 다시 만들어지고, 그다음 2장의 방법으로 다시 올리면 됩니다.

```bash
python "D:/Claude Code/Lecture/PIC Loss Evaluation/4_Online_Course/_build/md2html.py"
```

```bash
python "D:/Claude Code/Lecture/PIC Loss Evaluation/4_Online_Course/_build/export_site.py"
```

---

학습 진도(완료한 Part, 푼 문제, 언어, 테마)는 방문자 각자의 브라우저(`localStorage`)에만 저장되며 서버로 전송되지 않습니다.
