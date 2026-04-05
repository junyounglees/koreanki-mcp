# koreanki-mcp

한국 전문자격시험 기출문제를 Claude에서 풀 수 있는 MCP 서버입니다.

## 지원 시험

| 시험 | 연도 |
|------|------|
| 세무사 | 2021\~2025 (58\~62회) |
| 관세사 | 2022\~2026 (39\~43회) |
| 행정사 | 2021\~2025 (9\~13회) |
| 감정평가사 | 2021\~2025 (32\~36회) |
| 공인노무사 | 2024\~2025 (33\~34회) |

모두 1차 객관식 문제입니다.

## 설정

### Claude Desktop

1. **Customize > Connectors**로 이동
2. 우측 상단 **+** 버튼 > **Add custom connector** 클릭
3. 아래 내용 입력 후 **Add** 클릭

| 항목 | 값 |
|------|---|
| Name | `koreanki` |
| Remote MCP server URL | `https://koreanki.vercel.app/api/mcp` |

### Claude Code

```bash
claude mcp add koreanki --transport url https://koreanki.vercel.app/api/mcp
```

## 사용법

Claude에게 자연어로 요청하면 됩니다.

- "세무사 시험 기출문제 풀어보자"
- "2024년 61회 세무사 1차 세법학개론 41번 문제 보여줘"
- "관세사 시험 목록 보여줘"

## 도구

| 도구 | 설명 |
|------|------|
| `list_exams` | 사용 가능한 기출문제 목록을 조회합니다 |
| `get_question` | 특정 문제를 조회합니다 (정답 미포함) |
| `check_answer` | 사용자의 답을 확인하고 정답을 반환합니다 |

## 흐름

1. `list_exams`로 시험 목록을 확인합니다
2. `get_question`으로 문제를 조회합니다 (정답은 포함되지 않습니다)
3. 사용자가 답을 선택하면 `check_answer`로 정답을 확인합니다

## 데이터 수집

`check_answer` 호출 시 아래 정보가 서버에 익명으로 저장됩니다:

- 시험 종류, 연도, 회차, 과목, 문제 번호
- 사용자가 선택한 답, 정답 여부
- 사용자의 풀이 근거 (reasoning)

개인 식별 정보는 수집하지 않습니다. 수집된 데이터는 서비스 개선 목적으로만 사용됩니다.
