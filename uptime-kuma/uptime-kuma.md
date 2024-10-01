# Uptime Kuma Install & Troubleshooting
사용하던 NAS가 갑자기 안 될 때, 자체 알림 기능까지 멈춰버려서 외부 모니터링을 사용하기로 했다.

사용할 서비스는 Uptime Kuma라는 모니터링 서비스다. 예전에도 사용을 했었지만, NAS가 거의 멀쩡하길래 그냥 없애버렸는데 다시 사용하기로 했다.

오라클 클라우드에서 항상 무료 인스턴스를 제공하므로, 이걸 사용하기로 했다.

## 인스턴스 생성
![instance](https://github.com/user-attachments/assets/b45ae7f9-4fd5-46f8-95bd-9096325df1d4)

인스턴스가 잘 생성되었다 OS는 Ubuntu 22.04를 설치했다.

## <img src="https://cdn.jsdelivr.net/gh/selfhst/icons/svg/docker.svg" width="32px" height="32px"> Docker 설치
Docker가 편리하므로 Docker를 사용하기로 했다.

[Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
> [!NOTE]
> ```bash
> # Add Docker's official GPG key:
> sudo apt-get update
> sudo apt-get install ca-certificates curl
> sudo install -m 0755 -d /etc/apt/keyrings
> sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
> sudo chmod a+r /etc/apt/keyrings/docker.asc
>
> # Add the repository to Apt sources:
> echo \
>   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
>   $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
> sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
> sudo apt-get update
> ```
>
> ```bash
> sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
> ```

## <img src="https://cdn.jsdelivr.net/gh/selfhst/icons/svg/uptime-kuma.svg" width="32px" height="32px"> Uptime Kuma 설치
[🔧 How to Install](https://github.com/louislam/uptime-kuma/wiki/%F0%9F%94%A7-How-to-Install)
> [!NOTE]
> ```yml
> # Simple docker-compose.yml
> # You can change your port or volume location
>
> version: '3.3'
>
> services:
>   uptime-kuma:
>     image: louislam/uptime-kuma:1
>     container_name: uptime-kuma
>     volumes:
>       - ./uptime-kuma-data:/app/data
>     ports:
>       - 3001:3001  # <Host Port>:<Container Port>
>     restart: always
> ```

## <img src="https://cdn.jsdelivr.net/gh/selfhst/icons/svg/uptime-kuma.svg" width="32px" height="32px"> Uptime Kuma 사용법

Uptime Kuma는 자체 대시보드를 제공한다.

내부 아이피로는 접속할 수 없으니 ```http://공용아이피:3001```로 접속할 수 있다.

하지만, 공용 아이피로 접속하기 위해서는 포트 포워딩을 해줘야 한다.

리버스 프록시 서버는 NAS에 설치돼 있기 때문에, 포트를 개방하지 않고 통신하기 위해 VPN을 사용하기로 했다.

## <img src="https://cdn.jsdelivr.net/gh/selfhst/icons/svg/tailscale-light.svg" width="32px" height="32px"> Tailscale 설치
처음에는 WireGuard와 Netbird를 사용하려고 했으나, 실패하고 Tailscale이 더 쉽게 바로 돼서 사용하게 됐다.
