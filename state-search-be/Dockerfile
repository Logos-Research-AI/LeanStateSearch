FROM ghcr.io/astral-sh/uv:python3.12-trixie-slim

RUN apt-get update && \
  apt-get install --no-install-suggests --no-install-recommends --yes libatomic1

ENV PATH="/root/.local/bin:${PATH}"
ENV MODEL_NAME_OR_PATH="/code/model/"

RUN mkdir -p /code

WORKDIR /code

COPY . /code

RUN uv sync --locked

RUN uv run prisma generate

ENV MODE="docker"
ENV BACKEND_PORT="7720"

CMD ["uv", "run", "main.py"]
