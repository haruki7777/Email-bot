# Email-bot

Discord에서 이메일 인증 코드를 보내고, 사용자가 받은 코드를 입력해야 전체 명령어를 사용할 수 있게 만드는 이메일 인증봇 템플릿입니다.

이 저장소는 같은 기능을 4가지 버전으로 나눠 제공합니다.

| 버전 | 폴더 | 용도 |
|---|---|---|
| JavaScript | `js-discord-bot` | discord.js v14 기반, 가장 빠르게 시작 |
| TypeScript | `ts-discord-bot` | 타입 안정성이 필요한 Node.js 봇 |
| Python | `py-discord-bot` | discord.py 기반 봇 |
| JDA Java | `jda-discord-bot` | Java/JDA 기반 봇 |

## 핵심 흐름

1. 사용자가 `/email-start 이메일주소` 명령어를 입력합니다.
2. 봇이 6자리 인증 코드를 이메일로 보냅니다.
3. 사용자가 `/email-verify 코드`를 입력합니다.
4. 인증 성공 시 역할을 지급하거나, 봇 내부 DB에 인증 완료 상태를 저장합니다.

## Gmail 사용 시 준비

Gmail SMTP를 쓸 경우 일반 비밀번호가 아니라 **Google 앱 비밀번호**를 사용하세요.
앱 비밀번호는 공백 없이 붙여 넣는 것을 권장합니다.

필요한 값:

```env
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_gmail@gmail.com
SMTP_PASS=your_google_app_password_without_spaces
MAIL_FROM="Natsumi Bot <your_gmail@gmail.com>"
```

## 공통 명령어

| 명령어 | 설명 |
|---|---|
| `/email-start email:<주소>` | 인증 코드 발송 |
| `/email-verify code:<6자리>` | 인증 코드 확인 |
| `/email-status` | 내 인증 상태 확인 |

## 보안 주의

- `.env` 파일은 절대 GitHub에 올리지 마세요.
- SMTP 비밀번호, Discord 토큰, API 키는 반드시 환경변수로 관리하세요.
- 인증 코드는 짧은 만료 시간을 두세요. 기본값은 10분입니다.
- 같은 사용자가 너무 자주 코드를 요청하지 못하도록 쿨다운을 두세요.

## 빠른 선택

모바일이나 VPS에서 가장 쉽게 돌릴 거면 `js-discord-bot`을 추천합니다.
타입까지 잡고 장기 운영할 거면 `ts-discord-bot`, 파이썬이 편하면 `py-discord-bot`, Java 생태계가 필요하면 `jda-discord-bot`을 쓰면 됩니다.

자세한 공통 API 규격은 [`docs/API_SPEC.md`](docs/API_SPEC.md)를 참고하세요.
