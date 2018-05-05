---
layout: post
title: "DNS over HTTPS 적용시키기"
date: 2018-05-05 22:10:00 +09:00
---

# Windows

1. [링크](https://developers.cloudflare.com/argo-tunnel/downloads/)를 참조하여 `cloudflared`를 다운받는다.
2. 압축을 해제해 적절한 폴더에 `cloudflared.exe`를 위치시키고 `PATH` 환경 변수에 적절히 경로를 추가한다.
  * 명령 프롬프트에서 `cloudflared`를 입력했을 때 에러가 발생하지 않아야 한다.
3. 관리자 권한으로 명령 프롬프트를 실행한다.
4. 다음 명령을 실행한다.

```
C:\Windows\System32>mkdir C:\Windows\System32\config\systemprofile\.cloudflared

C:\Windows\System32>(
echo proxy-dns: true
echo proxy-dns-upstream:
echo  - https://1.1.1.1/dns-query
echo  - https://1.0.0.1/dns-query
) > C:\Windows\System32\config\systemprofile\.cloudflared\config.yaml

C:\Windows\System32>cloudflared service install
INFO[0000] Installing Argo Tunnel Windows service

- INFO[0000] Cannot establish a connection to the service control manager  error="Access is denied." 와 같은 에러 메시지가 출력되지 않아야 한다.
```

5. `services.msc`를 실행하여 `Argo Tunnel agent` 서비스를 시작시킨다.
6. 네트워크 어댑터 설정에서 DNS를 `127.0.0.1`, `1.1.1.1`로 설정한다.
7. 명령 프롬프트에서 `nslookup example.com`을 입력하여 테스트 해본다.

```
C:\Users\Snack>nslookup example.com
서버:    localhost
Address:  127.0.0.1

권한 없는 응답:
이름:    example.com
Addresses:  2606:2800:220:1:248:1893:25c8:1946
          93.184.216.34
```

# macOS

```
$ brew install cloudflare/cloudflare/cloudflared
==> Tapping cloudflare/cloudflare
(...)

$ cloudflared --version
cloudflared version 2018.4.8 (built 2018-04-26-1815 UTC)

$ sudo mkdir /etc/cloudflared

$ sudo bash -c 'cat << EOF > ~/.cloudflared/config.yaml
proxy-dns: true
proxy-dns-upstream:
 - https://1.1.1.1/dns-query
 - https://1.0.0.1/dns-query
EOF'

$ sudo cloudflared service install
Password:
INFO[0000] Installing Argo Tunnel client as a system launch daemon. Argo Tunnel client will run at boot

$ sudo launchctl start com.cloudflare.cloudflared

$ dig @127.0.0.1 example.com A

; <<>> DiG 9.10.6 <<>> @127.0.0.1 example.com A
; (1 server found)

(...)

;; ANSWER SECTION:
example.com.            3534    IN      A       93.184.216.34

;; Query time: 56 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Sat May 05 22:42:29 KST 2018
;; MSG SIZE  rcvd: 67
```

* 네트워크 설정에서 DNS 설정을 `127.0.0.1`, `1.1.1.1`, `1.0.0.1`로 설정
