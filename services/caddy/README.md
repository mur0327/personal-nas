# <img src="https://cdn.jsdelivr.net/gh/selfhst/icons/svg/caddy.svg" width="32px" height="32px"> Caddy
Caddy는 리버스 프록시를 사용하는 방법이 매우 간단하다.

## 설치하기
[⚙️ Caddy Docker Compose](https://caddyserver.com/docs/running#docker-compose)
> [!NOTE]
> ```yml
> services:
>   caddy:
>     image: caddy:latest
>     restart: unless-stopped
>     ports:
>       - "임의포트1:80"
>       - "임의포트2:443"
>       - "임의포트2:443/udp"
>     volumes:
>       - ./Caddyfile:/etc/caddy/Caddyfile
>       - ./site:/srv
>       - caddy_data:/data
>       - caddy_config:/config
>
> volumes:
>   caddy_data:
>   caddy_config:
> ```
>
> ```
> docker compose up -d
> ```

같은 위치에 Caddyfile 파일과 site 폴더를 생성해주자.

Synology NAS는 80, 443 포트를 사용 중이기 때문에 다른 포트를 지정해야 한다.

## 포트 포워딩
KT GiGA WiFi 기준 다음과 같이 설정한다.

<img src="https://github.com/user-attachments/assets/0ea56e5b-1d83-462c-a7a1-4e070660113b">

## Caddyfile 설정하기
[📃 reverse_proxy (Caddyfile directive)](https://caddyserver.com/docs/caddyfile/directives/reverse_proxy)

```
example.com {
	reverse_proxy localhost:5000
}

sub.example.com {
	reverse_proxy localhost:5050
}
```
