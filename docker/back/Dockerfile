FROM python:3.12-slim-bookworm

# pipのバージョンチェックを無効化
ENV PIP_DISABLE_PIP_VERSION_CHECK="1"

WORKDIR /app

# 依存のインストールを行うために、`pipenv lock`を実行してrequirements.txtを生成
RUN --mount=type=cache,target=/root/.cache/pip \
  pip install pipenv
COPY back/Pipfile back/Pipfile.lock ./
RUN pipenv requirements > requirements.txt

# 依存のインストール
RUN --mount=type=cache,target=/root/.cache/pip \
  pip install -r requirements.txt

# アプリケーションのコードをコピー
COPY back/src/ ./src/

# アプリケーションの起動
CMD ["uvicorn", "src.main:app", "--proxy-headers", "--host", "0.0.0.0", "--port", "80", "--reload"]
