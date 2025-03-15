# Using Docker Services in Personal NAS

## 사용 환경
Synology NAS DS220+

## 사용중인 서비스
| <center>이미지</center>                        | <center>설명</center>      |
| ---------------------------------------------- | -------------------------- |
| ~~Apache Guacamole~~                           | 원격 접속 및 SSH 관리 도구 |
| Authentik                                      | SSO 인증 서비스            |
| Beszel                                         | NAS 모니터링 도구          |
| [Caddy](/services/caddy/README.md)             | 리버스 프록시 서버         |
| ~~Code Server~~                                | 원격 VSCode 환경           |
| Docker Socket Proxy                            | 도커 소켓 보안 연결        |
| Dockge                                         | 도커 컴포즈 관리           |
| Dozzle                                         | 도커 로그 뷰어             |
| Memos                                          | 메모 앱                    |
| Portainer                                      | 도커 관리 도구             |
| Tailscale                                      | 개인 VPN 네트워크          |
| [Uptime Kuma](/services/uptime-kuma/README.md) | 서버 및 웹 서비스 모니터링 |
| Vaultwarden                                    | 비밀번호 관리 도구         |
| Watchtower                                     | 도커 이미지 자동 업데이트  |

## 스택 구조

```bash
.
├── dockge
│   ├── data
│   └── compose.yml
└── stacks
    ├── authentik
    │   ├── certs
    │   ├── custom-templates
    │   ├── media
    │   ├── .env
    │   └── compose.yml
    ├── beszel-agent
    │   └── compose.yml
    ├── beszel-hub
    │   ├── data
    │   └── compose.yml
    ├── caddy
    │   ├── config
    │   ├── data
    │   ├── srv
    │   ├── Caddyfile
    │   └── compose.yml
    ├── code-server
    │   ├── config
    │   └── compose.yml
    ├── docker-socket-proxy
    │   └── compose.yml
    ├── dozzle
    │   └── compose.yml
    ├── guacamole
    │   ├── data
    │   ├── init
    │   │   └── initdb.sql
    │   └── compose.yml
    ├── memos
    │   ├── data
    │   └── compose.yml
    ├── portainer
    │   └── compose.yml
    ├── vaultwarden
    │   ├── vw-data
    │   └── compose.yml
    └── watchtower
        └── compose.yml
```
