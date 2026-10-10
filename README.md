# 파수대 연구 해설 조사 도우미

[English](README.en.md) | **한국어**

「파수대」 연구 기사의 항별 해설을 **wol.jw.org에서만** 조사해서 **기본해설 / 부가해설 / 연구해설**로 정리해 주는 AI 스킬입니다.

![조사 과정](docs/images/research-flow.gif)

---

## ⚠️ 먼저 읽어 주세요: 일반 채팅에서는 쓰지 마세요

이 스킬은 **Claude Code** 또는 **Codex** 같은 "에이전트" 도구에서 사용해야 합니다. claude.ai나 ChatGPT의 일반 대화창은 이 스킬에 맞지 않습니다.

![일반 채팅 vs 에이전트](docs/images/chat-vs-agent.png)

일반 채팅은 wol.jw.org를 직접 검색하고 열어 보는 과정이 없거나 제한적입니다. 그래서 출처를 기억에 의존해 그럴듯하게 지어낼 위험이 있습니다. 이 스킬은 **실제로 검색하고, 열어 읽고, 검증하는 과정**이 핵심이기 때문에 에이전트 도구가 필요합니다.

| 도구 | 추천 | 비고 |
|---|---|---|
| **Claude 데스크톱 앱 → Code 탭** | ⭐ 가장 추천 | 내장 브라우저 창에서 조사 과정을 직접 지켜볼 수 있습니다 |
| **Claude Code (터미널)** | ○ | 진행 보고와 조사 과정 표로 확인합니다 |
| **Codex CLI** | ○ | 실시간 웹 검색(`--search`)을 켜야 합니다 |
| claude.ai / ChatGPT 일반 대화 | × | 권장하지 않습니다 |

---

## 어떻게 동작하나요?

사람이 WOL에서 조사하는 순서를 그대로 따라 합니다.

| 단계 | 화면 |
|---|---|
| **① 기사 원문 읽기**<br>항 번호, 연구 질문, 인용 성구, 각주를 정리합니다. | <img src="docs/images/step1.png" width="320"> |
| **② WOL 검색창에 키워드 입력**<br>항마다 키워드 2~3개를 직접 입력합니다. | <img src="docs/images/step2.png" width="320"> |
| **③ 검색 결과 확인**<br>관련성이 높고 최근인 출판물부터 고릅니다. 결과가 0건이면 검색어를 줄여서 다시 검색합니다. | <img src="docs/images/step3.png" width="320"> |
| **④ 자료를 열어 문맥까지 읽기**<br>검색 결과에 보이는 짧은 발췌만 보지 않고, 기사를 열어 앞뒤 문맥을 확인합니다. | <img src="docs/images/step4.png" width="320"> |
| **⑤ 결과 정리**<br>조사 과정 표와 기본·부가·연구해설을 출처와 함께 정리합니다. | <img src="docs/images/step5-result.png" width="320"> |

> 위 ①~④는 실제 wol.jw.org 화면을 캡처한 것입니다.

**지켜지는 규칙**
- **jw.org / wol.jw.org 외의 사이트는 사용하지 않습니다.**
- 확인하지 못한 내용은 "출처 확인 못 함"이라고 표시합니다.
- 개인 경험이 들어가면 좋은 곳에는 `[개인 경험]` 자리만 표시합니다. 내용은 직접 채워 넣으세요.

---

## 설치 방법

### A. Claude Code (데스크톱 앱 Code 탭 / 터미널)

![Claude Code 설치와 사용](docs/images/claude-code.gif)

터미널에서 다음을 차례로 실행합니다.

```bash
git clone https://github.com/suinegyzal/watchtower-comment-research.git
mkdir -p ~/.claude/skills
cp -R watchtower-comment-research/watchtower-comment-research ~/.claude/skills/
```

- `git`이 없다면 저장소 페이지에서 **Code → Download ZIP**으로 내려받아 압축을 풉니다. 그런 다음 `watchtower-comment-research` 폴더를 `~/.claude/skills/` 안에 넣어도 됩니다.
- 설치한 뒤에는 Claude Code를 새로 시작하세요. 데스크톱 앱이라면 새 세션을 열면 됩니다.

### B. Codex CLI

![Codex 설치와 사용](docs/images/codex.png)

```bash
git clone https://github.com/suinegyzal/watchtower-comment-research.git
mkdir -p ~/.codex/skills
cp -R watchtower-comment-research/watchtower-comment-research ~/.codex/skills/
codex --search
```

- `--search`는 실시간 웹 검색을 켜는 옵션입니다. 항상 켜 두려면 `~/.codex/config.toml`에 `web_search = "live"`를 넣으세요.
- Codex가 wol.jw.org에 접속해도 되는지 물어보면 승인해 주세요.
- 스킬이 안 보이면 폴더 안에 `SKILL.md` 파일이 있는지 확인하고 Codex를 다시 시작하세요.

### 업데이트

```bash
cd watchtower-comment-research && git pull
cp -R watchtower-comment-research ~/.claude/skills/   # Codex는 ~/.codex/skills/
```

---

## 사용 방법

새 세션에서 기사 링크와 함께 이렇게 요청하세요.

```
이번 주 파수대 기사야: https://wol.jw.org/ko/wol/d/r8/lp-ko/(기사번호)
1항부터 3항까지 기본해설, 부가해설, 연구해설로 정리해 줘.
```

다음처럼 요청해도 됩니다.
- `4항부터 6항까지 이어서 해 줘`
- `5항 연구해설만 더 깊게 찾아 줘`
- `해설을 더 짧게, 30초 안에 말할 수 있게 줄여 줘`

**결과 예시**

| 순서 | 검색 키워드 | 결과 | 열어 본 자료 | 찾은 내용 |
|---|---|---|---|---|
| 1 | 빛의 천사로 가장 | 38건 | 「통찰」 1권 "사탄" | 사탄은 "본색과 목적을 감추고" 접근함 |
| 2 | 의심 바다 물결 | 33건 | 「파수대」 2021년 2월호 26-31면 | 의심은 닻을 연결하는 쇠사슬의 녹과 같음 |
| 3 | 사탄 사랑받을 가치 | 3건 | 「파수대」 2019년 9월호 15항 | 사탄은 우리가 "사랑받을 가치가 없다"고 믿게 하려 함 |

**1항: 사탄은 우리가 여호와께 등을 돌리게 하기 위해 어떤 방법을 사용합니까?**
- **기본해설**: 사탄은 우리가 여호와와 가까이 지내는 한 이길 수 없다는 걸 압니다. 그래서 여호와와 예수께서 우리를 사랑하신다는 점에 의문을 갖게 만들어 우리가 스스로 등을 돌리게 하려고 합니다.
- **부가해설**: 사탄은 우리가 "사랑받을 가치가 없다"고 믿게 하려 합니다. 하지만 로마 8:38, 39은 어떤 것도 하느님의 사랑에서 우리를 갈라놓을 수 없다고 말합니다. (「파수대」 2019년 9월호 15항)
- **연구해설**: 야고보 1:6은 의심하는 사람을 출렁이는 바다 물결에 비유합니다. 희망이 닻이라면 믿음은 닻에 연결된 쇠사슬인데, 의심을 해결하지 않으면 그 사슬이 녹슬어 약해집니다. (「파수대」 2021년 2월호 15-16항)

**사용 팁**
- **처음에는 2~3항씩** 요청하세요. 한 번에 18항을 모두 요청하면 조사가 얕아집니다.
- **최종 확인은 꼭 직접 하세요.** 표에 적힌 출처를 WOL에서 열어 문맥을 확인한 다음 사용하세요.

---

## 파일 구성

```
README.md / README.en.md            설명서 (한국어 / 영어)
watchtower-comment-research/        스킬 본체 → ~/.claude/skills 또는 ~/.codex/skills에 복사
  ├── SKILL.md                      조사 규칙과 절차
  └── references/wol.md             WOL 주소 형식, 성경 책번호
watchtower-comment-research.skill   스킬 압축 파일 (같은 내용)
prompts/                            참고용 프롬프트 원문
docs/images/                        설명용 이미지
```

## 주의

- 이 도구는 개인의 집회 준비를 돕기 위한 것입니다. 여호와의 증인 또는 Watch Tower Bible and Tract Society의 공식 도구가 아닙니다.
- jw.org 자료와 화면 캡처의 저작권은 Watch Tower Bible and Tract Society of Pennsylvania에 있습니다. 출판물 내용을 대량으로 복사해서 배포하지 마세요.
- 터미널 이미지(Claude Code / Codex)는 이해를 돕기 위한 **예시 화면**입니다. 실제 화면은 버전에 따라 다를 수 있습니다.
