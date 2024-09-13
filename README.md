# Rodando o Ollama no Docker

Este repositorio tem por finalidade compartilhar a configuração do docker-composer para a execução do Ollama, seja em computadores com ou sem placa de video.

## ⚠️ Versão para PCs sem placa de video: 
```
version: '3'
services:
  ollama:

    image: ollama/ollama:latest
    ports:
      - 11434:11434
    volumes:
      - ./:/root/.ollama
    container_name: ollama
    pull_policy: always
    tty: true
    restart: always
    environment:
      - OLLAMA_KEEP_ALIVE=24h
      - OLLAMA_HOST=0.0.0.0
    networks:
      - ollama-docker


networks:
    ollama-docker:
        driver: bridge
```
## ⚠️ Versão para PCs com placa de video:
```
version: '3'
services:
  ollama:

    image: ollama/ollama:latest
    ports:
      - 11434:11434
    volumes:
      - ./:/root/.ollama
    container_name: ollama
    pull_policy: always
    tty: true
    restart: always
    deploy:
            resources:
                reservations:
                    devices:
                      - driver: nvidia
                        count: 1
                        capabilities: [gpu]
    environment:
      - OLLAMA_KEEP_ALIVE=24h
      - OLLAMA_HOST=0.0.0.0
    networks:
      - ollama-docker


networks:
    ollama-docker:
        driver: bridge
```
