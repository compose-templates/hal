# Hal demo (for GenAI Stack)

# How to use it
> requirement: you need to use Ollama
## Setup

First, clone GenAI Stack
```bash
git clone git@github.com:docker/genai-stack.git
```

Then, enter the directory
```bash
cd genai-stack
```

Then, clone the hal demo (the AI app):
```bash
git clone git@github.com:compose-templates/hal.git
```

Add this dependency to the `requirements.txt` file:
```
chromadb
```

## Compose update

```yaml
# by k33g_org
  hal:
    container_name: hal-container
    build:
      context: .
      dockerfile: api.Dockerfile
    volumes: # create a hal directory
      - $PWD/hal:/hal
    environment: *env # add this anchor to the api service: &env
    networks:
      - net
    depends_on:
      pull-model:
        condition: service_completed_successfully

```
> 👋 don't forget to add the `&env` anchor to the `api` service

## Run

```bash
docker compose up
```

## Python examples

- `question.py`: ask Ollama what you want
- `hal.py`: how to enrich the model with a document
