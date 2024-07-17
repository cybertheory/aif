# AI IPASS Setup Guide

## 1. Prerequisites

- Docker
- Vector database (e.g., Pinecone, Faiss, or Weaviate)
- AI model for schema analysis and mapping generation

## 2. Configuration

Create a `config.yaml` file with the following structure:

```yaml
ai_ipass:
  host: 0.0.0.0
  port: 8080

vector_store:
  type: pinecone
  api_key: YOUR_API_KEY
  environment: production

ai_model:
  type: openai
  api_key: YOUR_API_KEY
  model: gpt-4

systems:
  - name: System A
    url: https://systema.example.com
    auth:
      type: oauth2
      client_id: CLIENT_ID
      client_secret: CLIENT_SECRET
  - name: System B
    url: https://systemb.example.com
    auth:
      type: api_key
      key: API_KEY
```

## 3. Docker Setup
## Create a Dockerfile:
```
FROM python:3.9

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

CMD ["python", "main.py"]
```

## 4. Running AI IPASS

- Build the Docker image:
```
docker build -t ai-ipass .
```

- Run the container:
```
docker run -p 8080:8080 -v $(pwd)/config.yaml:/app/config.yaml ai-ipass
```


# 5. Verify Setup
- Access the AI IPASS status endpoint:

GET http://localhost:8080/status

- Expected response:
```
jsonCopy{
  "status": "ok",
  "version": "1.0.0",
  "connected_systems": ["System A", "System B"]
}
```