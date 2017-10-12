---
layout: post
title: "아이튠즈 폰트 바꾸기"
date: 2016-12-06 21:13:04 +09:00
---

자꾸 승질이 뻗쳐서 바꾸는 김에 미래의 나를 위해 방법을 확실히 정리.

# TextStyles.plist

아이튠즈 설치 폴더의 `iTunes.Resources/ko.lproj`에서 폰트를 바꿔야 한다.
윈도우의 경우에는 맑은 고딕, Segoe UI, Lucida Grande 등이 사용되고 있는데, 맑은 고딕만 바꿔주면 보기 좋아진다.

문제는 이 파일이 바이너리 형태로 되어 있다는 것인데, 맥에서는 `plutil -convert xml1 ~~~.plist`로 변환이 가능하다.
윈도우에도 아이튠즈와 함께 `plutil`이 들어있다. `C:\Program Files\Common Files\Apple\Apple Application Support`에 있다. 64비트라면 `Program Files (x86)`.

관리자 권한 cmd를 열고

```
> copy "C:\Program Files\iTunes\iTunes.Resources\ko.lproj\TextStyles.plist" "C:\Program Files\iTunes\iTunes.Resources\ko.lproj\TextStyles_backup_binary.plist"
> "C:\Program Files (x86)\Common Files\Apple\Apple Application Support\plutil.exe" -convert xml1 "C:\Program Files\iTunes\iTunes.Resources\ko.lproj\TextStyles.plist"
> copy "C:\Program Files\iTunes\iTunes.Resources\ko.lproj\TextStyles.plist" "C:\Program Files\iTunes\iTunes.Resources\ko.lproj\TextStyles_backup_xml.plist"

(편집)

> "C:\Program Files (x86)\Common Files\Apple\Apple Application Support\plutil.exe" -convert binary1 "C:\Program Files\iTunes\iTunes.Resources\ko.lproj\TextStyles.plist"
```

하면 된다. (아마)

# iTunes.css

애플 뮤직이나 아이튠즈 스토어 페이지는 여전히 폰트가 구리고 특히 일본어 페이지는 왕창 깨지는데, `iTunes.Resources/iTunes.css` 를 고쳐야 한다.

파일 맨 밑에 이거 한 줄을 넣으면 깔끔.

```css
* { font-family: "Noto Sans CJK KR", "Segoe UI" !important; }
```

Noto Sans CJK KR가 이미 설치되어 있을 때의 얘기지만.

가장 중요한건 업데이트 한번 하면 이 짓거리를 다시 해줘야 한다 ㅡㅡ
