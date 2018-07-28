---
layout: post
title: "CD / DVD / BD 리핑하기"
date: 2018-07-28 00:00:00 +09:00
---

CD나 DVD, 혹은 BD와 같은 광디스크 매체를 많이 구입하면서 개인적으로 가장 중요하게 여기는 것은 보존이다. 원본과 가장 유사한 형태로 백업해 다양한 방식을 통해 보존하는 것이 나에게는 가장 중요하다.

오디오 CD라면 무손실 음원으로. DVD나 BD같은 영상 매체라면 리핑 소프트웨어를 이용해 RAW 영상 파일로.

개인적으로 사용하는 리핑 방식을 정리해보고자 한다.

# CD

오디오 CD에는 [Exact Audio Copy](http://www.exactaudiocopy.de/)를 사용해서 리핑한다.

이 소프트웨어를 설정하는 것은 굉장히 까다롭다. 내가 사용하는 설정 방식은 WhatCD 등지에서 사용되는 이른바 '로그 100%' 설정.

아래 가이드를 따라하면 설정이 가능하다.

* [EAC(Exact Audio Copy) 리핑 가이드 1 - 리핑을 위한 설정](http://royalmilk.pe.kr/23)
* [EAC(Exact Audio Copy) 리핑 가이드 2 - 리핑시 언제나 해야만 하는 것들](http://royalmilk.pe.kr/24)

FLAC 파일로 리핑한 뒤에는 태그를 다시 한번 정리한 뒤 MP3로 변환해 듣는다. FLAC은 그저 보존용일 뿐이다. 일반인은 FLAC이랑 320Kbps MP3를 구별 못한다!

# DVD

비디오 DVD에는 [DVD Decrypter](http://www.dvddecrypter.org.uk/)를 사용한다.

DVD에는 설정하기 귀찮고 복잡한 지역코드가 걸려있지만, 이 소프트웨어를 이용하면 DVD에 걸려있는 암호화나 지역코드 등을 무시하고 깔끔하게 원본 파일을 얻을 수 있다.

`.IFO`, `.BUP`, `.VOB` 파일 등의 결과물이 나오고, `VIDEO_TS.IFO` 파일을 이용하면 DVD 메뉴 등이 나오는 형식으로 재생이 가능하다.

# BD

BD에는 [MakeMKV](https://www.makemkv.com/)를 사용한다.

30일동안 모든 기능을 사용할 수 있는 프로그램으로, BD 리핑할 일이 많다면 구입해두는게 좋은 프로그램이다.

블루레이를 넣고 상단 툴바에서 'Backup Disc'를 클릭한 뒤 'Decrypt video files'를 체크하고 OK를 누르면 수십GB의 BD 원본 파일이 복사된다.

복사된 폴더의 `BDMV/PLAYLIST` 폴더와 `BDMV/STREAM` 폴더를 확인해보면 `.mpls`와 `.m2ts` 파일을 확인할 수 있다.

# 영상 인코딩

DVD와 BD에서 리핑된 원본 파일을 보기 쉬운 영상 파일로 만드는 데에는 [HandBrake](https://handbrake.fr/)만큼 좋은 프로그램이 없다.

나는 이 방면의 전문가가 아니기 때문에 어떤 프리셋과 어떤 설정값을 사용하라는 말을 할 수가 없다.
