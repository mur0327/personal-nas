# <img src="https://cdn.jsdelivr.net/gh/selfhst/icons/svg/uptime-kuma.svg" width="32px" height="32px"> Uptime Kuma
잘 작동하던 NAS가 꺼졌다. 꺼진 줄도 모르고 하루가 지났다.

자체 알림 기능까지 멈춰버려서 외부 모니터링을 사용하기로 했다.

사용할 서비스는 Uptime Kuma이다. 외부 모니터링이니 외부 서버가 필요하다.

오라클 클라우드에서 항상 무료 인스턴스를 제공하므로, 이걸 사용하기로 했다.

## 인스턴스 생성
![instance](https://github.com/user-attachments/assets/b45ae7f9-4fd5-46f8-95bd-9096325df1d4)

## <img src="https://cdn.jsdelivr.net/gh/selfhst/icons/svg/docker.svg" width="32px" height="32px"> Docker 설치
Docker가 편리하므로 Docker를 사용하기로 했다.

[⚙️ Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
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
[⚙️ 🔧 How to Install](https://github.com/louislam/uptime-kuma/wiki/%F0%9F%94%A7-How-to-Install)
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
>
> ```
> docker compose up -d
> ```

Uptime Kuma는 자체 대시보드를 제공한다. 클라우드 서버는 내부 아이피 접속이 불가능하고

공용 아이피로 접속하려면 포트 개방을 해야 하므로

포트 개방을 하지 않기 위해 안전하게 VPN을 사용해서 접속하기로 했다.

## <img src="https://cdn.jsdelivr.net/gh/selfhst/icons/svg/tailscale-light.svg" width="32px" height="32px"> Tailscale 설치
처음에는 WireGuard나 Netbird를 사용하려고 했지만, Tailscale이 쉽고 편해서 이걸 사용하기로 했다.

1. [Tailscale 계정 생성](https://login.tailscale.com/start)

2. Synology NAS에 Tailscale 패키지 설치<br>
[⚙️ Access Synology NAS from anywhere](https://tailscale.com/kb/1131/synology?q=synology)

3. Oracle VM에 Tailscale 설치<br>
[⚙️ Access Oracle Cloud VMs privately using Tailscale](https://tailscale.com/kb/1149/cloud-oracle)

4. [Tailscale 어드민 페이지 접속](https://login.tailscale.com/admin)

연결이 잘 되었는지 확인하기 위해 NAS SSH에 접속해서 ping을 보내보자 ```ping 오라클VPN아이피```

대시보드에 접속하려면 접속할 컴퓨터에도 VPN을 연결해야 한다.

하지만, VPN을 항상 켜놓을 필요는 없으므로 리버스 프록시를 사용하여 접속하기로 했다.

## <img src="https://cdn.jsdelivr.net/gh/selfhst/icons/svg/caddy.svg" width="32px" height="32px"> [Caddy 설치](/services/caddy/README.md)

## <img src="https://cdn.jsdelivr.net/gh/selfhst/icons/svg/uptime-kuma.svg" width="32px" height="32px"> Uptime Kuma 사용법
![Monitoring](https://github.com/user-attachments/assets/8605d539-008e-4414-90aa-01980418a4e9)

새로운 모니터링 추가하기 버튼을 눌러 모니터링을 추가하면 된다.

모니터링을 추가할 때 ```http://나스VPN아이피:포트```로 지정하면 된다.

같은 서버가 아니기 때문에 도커 컨테이너를 모니터링 하기 위해서는 [Docker Socket Proxy](/services/docker-socket-proxy/README.md)를 사용해야 한다.

알람 설정도 가능하며, 본인은 디스코드 웹훅으로 설정해놨다.
