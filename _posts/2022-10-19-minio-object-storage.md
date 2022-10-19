---
layout: post
title: "minio object storage"
date: 2022-10-19 11:00:00 -0000
categories: docker
tags: homelab minio docker s3
---

docker compose for configuring a minio object server
```yml
version: '3'

services:
  minio:
    image: minio/minio
    ports:
      - "9000:9000"
      - "9001:9001"
    volumes:
      - minio_storage:/data
    environment:
      MINIO_ROOT_USER: masoud
      MINIO_ROOT_PASSWORD: Strong#Pass#2022
    command: server --console-address ":9001" /data

volumes:
  minio_storage: {}
```