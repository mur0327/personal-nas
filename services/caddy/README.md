# <img src="https://cdn.jsdelivr.net/gh/selfhst/icons/svg/caddy.svg" width="32px" height="32px"> Caddy
Caddy는 리버스 프록시를 사용하는 방법이 매우 간단하다.

[⚙️ Caddy Docker Compose](https://caddyserver.com/docs/running#docker-compose)
> [!NOTE]
> ```yml
> services:
>   caddy:
>     image: caddy:latest
>     restart: unless-stopped
>     ports:
>       - "80:80"
>       - "443:443"
>       - "443:443/udp"
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

예시로, 다음과 같이 설정하면 된다.
```yml
"8080:80"
"8443:443"
"8443:443/udp"
```

그 다음에는 공유기에 접속해서 포트 포워딩을 해야 한다.

TCP 80번 포트는 8080으로, TCP/UDP 443 포트는 8443번으로 설정한다.

- [ ] Caddyfile 설정법 작성하기
