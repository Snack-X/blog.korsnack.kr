---
layout: post
title: "UHD BD 리핑하기"
date: 2018-07-29 00:00:00 +09:00
---

일반 BD와 다르게 UHD BD를 리핑하는 것은 굉장히 어려운 일이다.

리핑이 가능한 소프트웨어가 나온 것도 얼마 되지 않았고, 특정 블루레이 드라이브와 특정 펌웨어 등 다양한 조건을 맞춰야 한다.

# 사용 가능한 드라이브

아래 링크를 참조하면 공식적으로 UHD를 지원하는 드라이브와 UHD를 간접적으로 지원하는 드라이브들의 목록을 확인할 수 있다.

* https://www.deuhd.ru/supported.html
* http://makemkv.com/forum2/viewtopic.php?f=16&t=16832

내가 사용할 드라이브는 **LG WH16NS40**으로, 공식적으로 지원되진 않지만 UHD 리핑에 사용할 수 있다고 판명된 드라이브이다.

* [How to tell if WH16NS40 is UHD friendly](https://forum.redfox.bz/threads/how-to-tell-if-wh16ns40-is-uhd-friendly.74467)

이 링크에 따르면 같은 드라이브여도 사용이 가능한 종류가 있고, 사용할 수 없는 종류가 있는데, 나는 다행히도 사용 가능한 종류이다.

문제는 이 드라이브로 UHD-BD를 리핑하기 위해서는 지원이 삭제된 1.03 펌웨어가 아닌 1.02 이하의 펌웨어를 사용해야 하는데, 내가 이 드라이브를 받았을 때는 이미 1.03 펌웨어가 설치된 상태였다.

# 펌웨어 다운그레이드

**아래 과정을 따라하다가 발생하는 모든 문제는 해당 사용자의 책임입니다.**

아래 글을 따라 진행한다.

* [100% Firmware Downgrade for ASUS BW-16D1HT and LG BH16NS55](http://makemkv.com/forum2/viewtopic.php?p=60423)

## 펌웨어 백업

1. 글의 내용 중 `Download the Windows 7 Live (Portable Edition) ISO from here.` 에서 `here`를 클릭해 Windows 7 Live ISO 이미지를 다운 받는다.
2. [Rufus](https://rufus.akeo.ie/)를 다운 받아, 적절한 USB 드라이브에 위 ISO를 선택해 부팅 가능한 USB로 만든다.
3. 글에 첨부된 파일 중 `Dosflash_Windows7.zip`를 다운 받아 USB에 압축을 해제한다.
4. 컴퓨터를 재시작해, BIOS 설정으로 진입한다.
5. CSM (Compatibility Support Module) 을 활성화 한 뒤, 스토리지 컨트롤러를 IDE, 혹은 Legacy로 설정한다.
6. 설정을 저장하고 USB로 부팅하되, UEFI를 사용하지 않고 부팅한다.
7. Windows 7로 부팅이 되면 USB에서 `DOSFLASH32_BH16NS40.exe`를 실행한다.
8. 드라이브가 안식됐다면 `Read Flash`를 클릭해 펌웨어를 백업한다.
  * 드라이브가 인식되지 않았다면 해당 드라이브가 메인보드의 SATA 0번, 혹은 1번에 꽃혀있는지 확인한다.
9. BIOS를 원래 설정으로 돌려놓은 뒤, 본래 OS로 부팅한다.

## 펌웨어 개조

드라이브에서 백업한 펌웨어에는 해당 드라이브의 고유한 값들이 저장되어 있다. 이 값들을 1.02 펌웨어에 옮긴다.

* [Crossflash Blu-Ray LG serii NS50/NS51/NS55/NS58](https://forum.cdrinfo.pl/f29/crossflash-blu-ray-lg-serii-ns50-ns51-ns55-ns58-96313)

1. 위 포럼의 중간쯤에 있는 `zippyshare` 링크를 클릭해 파일을 다운 받는다.
2. 다운 받은 파일을 열어보면 `.exe` 파일 한개와 여러개의 `.bin` 파일이 있다. `flash_HL-DT-ST_BD-RE_WH16NS40_1.02.bin` 파일을 기반으로 작업한다.
3. 적절한 헥스 에디터를 이용해 백업한 펌웨어와 이전 펌웨어를 연다. 글에 적혀있는 [WinHex](https://www.x-ways.net/winhex/), 내가 사용하는 [HxD](https://mh-nexus.de/en/hxd/), 어떤 것이든 좋다.
4. 백업한 펌웨어의 `0x1E8000 - 0x1E84FF` 영역을 복사해 이전 펌웨어의 같은 영역에 붙여넣는다.
5. 백업한 펌웨어의 `0x1E9000 - 0x1FFFFF` 영역을 복사해 이전 펌웨어의 같은 영역에 붙여넣는다.
6. 수정된 이전 펌웨어를 다른 이름으로 저장하고, USB에 복사한다.
7. BIOS를 다시 설정한 뒤, 동일한 방식으로 USB로 부팅한다.

## 펌웨어 올리기

1. Windows 7로 부팅이 되면 USB에서 `DOSFLASH32_BH16NS40.exe`를 실행한다.
2. `Erase Flash`를 선택한 후 버튼을 클릭하여 펌웨어를 지운 뒤, `Write Flash`를 선택한 뒤 버튼을 클릭 후 위에서 개조한 1.02 펌웨어를 선택해 해당 펌웨어를 올린다.
3. BIOS를 원래 설정으로 돌려놓은 뒤, 본래 OS로 부팅한다.

위 과정이 문제가 없었다면 [MakeMKV](http://makemkv.com/)에서 `WH16NS40 1.02`로 인식될 것이다.
문제가 있었다면? 잘 모르겠다. 나는 문제가 없었거든.

원 글에서는 문제가 생겼을 경우 해당 드라이브는 벽돌이 되고 쓰레기장에 던져져야 하는 운명이 된다고 경고하고 있다.

# MakeMKV 설정

* [UHD FAQ](http://makemkv.com/forum2/viewtopic.php?f=12&t=16883)
* [Hashed Keys](http://makemkv.com/forum2/viewtopic.php?f=12&t=16959)

위 두 글을 따라 MakeMKV에서 데이터 디렉토리를 설정한 뒤, `keys_hashed.txt`를 해당 디렉토리에 복사한다.
이후 가지고 있는 UHD BD를 해당 드라이브에 집어 넣고 MakeMKV를 이용해 백업한다.

![](https://upup.host/zTGdyM9.png)

**행운을 빈다.**
