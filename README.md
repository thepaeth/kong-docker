# KONG Docker Deployment with docker-compse
---

Kong API Gateway deployment with docker and docker-compose


## Status

This deployment is production ready.

## Change Default value

Copy `default.env` to `.env`

```
cp default.env .env
```

then edit the `.env` file to change default value

Default values

| Variable name | Defaule value |
|---------------|---------------|
| POSTGRES_VERSION  | 13-alpine |
| POSTGRES_USER     | kong |
| POSTGRES_PASSWORD | kong |
| POSTGRES_DB       | kong |
| KONG_VERSION      | 2.2 |
| KONG_ADMIN_LISTEN | 0.0.0.0:8001 |
| KONG_PROXY_LISTEN | 0.0.0.0:8000, 0.0.0.0:8443 ssl http2 |
| KONG_NGINX_HTTP_RESOLVER | 8.8.8.8 |
| KONG_PG_HOST      | kong-database |
| KONG_PG_USER      | kong == `env POSTGRES_USER` |
| KONG_PG_PASSWORD  | kong == `env POSTGRES_PASSWORD`|
| KONG_PG_DATABASE  | kong == `env POSTGRES_DB`   |


## Quick start

```
time ./quick-start.sh
```

## Deploy Kong step by step

### Deploy kong-database

```
docker-compose up -d kong-database
```

### Run kong-database migrations

```
docker-compose run --rm kong kong migrations bootstrap --vv
```

### Start Kong

```
docker-compose up -d kong
```

**Now Kong is running**

- Kong Admin API http://127.0.0.1:8001
- Kong Proxy http://127.0.0.1

### Start Konga

```
docker-compose up -d konga
```

**Now Konga is running**

- Konga http://127.0.0.1:1337

### Acccess Konga securely

If you deploy Kong on remote host we can access konga via ssh tunnel

```
ssh -L 1337:127.0.0.1:1337 username@kong.example.com
```

Now you can access konga on [localhost](http://localhost:1337)

### Postman Admin API
[Kong CE Admin API V2.0](https://documenter.getpostman.com/view/10587735/SzS7QS2c?version=latest#b5c37285-0e71-411a-b44d-f06fea8e6b24)

