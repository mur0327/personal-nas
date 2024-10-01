# Docker Services Install & Troubleshooting

## 사용 환경
Synology NAS DS220+

## 현재 사용중인 서비스
| 이미지              | 설명                      |
| ------------------- | ------------------------- |
| authentik           | SSO                       |
| caddy               | 리버스 프록시             |
| code-server         | 원격 VSCode               |
| docker-socket-proxy | docker.sock 프록시        |
| dozzle              | 도커 컨테이너 로그 뷰어   |
| guacamole           | 원격 SSH                  |
| memos               | 메모 앱                   |
| netdata             | NAS 모니터링              |
| portainer           | 도커 컨테이너 관리        |
| vaultwarden         | 비밀번호 관리             |
| watchtower          | 도커 이미지 자동 업데이트 |

## + Oracle VMs
| 이미지                                    | 설명               |
| ----------------------------------------- | ------------------ |
| [Uptime Kuma](uptime-kuma/uptime-kuma.md) | NAS 작동 상태 확인 |
