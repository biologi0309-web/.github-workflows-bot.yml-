name: Upbit Golden Cross Bot

on:
  schedule:
    - cron: '*/10 * * * *' # 10분마다 자동 실행
  workflow_dispatch:       # 수동 즉시 실행 버튼 활성화

permissions:
  contents: write          # 중복 알림 방지 기록(sent_history.json) 저장 권한

jobs:
  run-bot:
    runs-on: ubuntu-latest
    steps:
      - name: 코드 가져오기
        uses: actions/checkout@v4

      - name: Python 설정
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'

      - name: requests 설치
        run: pip install requests

      - name: 업비트 스캔 실행
        run: python run_once.py

      - name: 발송 기록 저장
        run: |
          git config --local user.email "action@github.com"
          git config --local user.name "GitHub Action"
          git add -A
          git diff --quiet && git diff --staged --quiet || (git commit -m "Update sent history" && git push)
