---
layout: post
author: me
title: "Unity Text 바이트 파일 역공학 분석"
category: [Unity, Reverse Engineering]
---
Unity Text 바이트 파일을 분석한 내용<br>
분석한 게임: [Diaries of a Spaceport Janitor]

|Text (Script)|4 bytes (hex)|유형|
|------|------|------|------|
|01 |00 00 00 00    |아직 파악 불가|
|01	|00 00 00 00	|아직 파악 불가|
|02	|xx xx 00 00	|Object Number (255 이하 byte / 256 이상 short or int)|
|03	|00 00 00 00	|아직 파악 불가	|
|04	|0x 00 00 00	|activeself (bool)|
|05	|0x 00 00 00	|아직 파악 불가	|
|06	|xx 00 00 00	|아직 파악 불가	|
|07	|xx 00 00 00	|아직 파악 불가	|
|08	|xx 00 00 00	|아직 파악 불가	|
|09	|xx 00 00 00	|Material	|
|10	|xx 00 00 00	||
|11	|00 00 00 00	||
|12	|xx xx xx xx	|Color R (변수형 파악 못함. 아마도 바이트플롭된 float)	|255 == 00 00 80 3F |
|13	|xx xx xx xx	|Color G (변수형 파악 못함)	|50 == C9 C8 48 3E  |
|14	|xx xx xx xx	|Color B (변수형 파악 못함)	|100 == C9 C8 C8 3E |
|15	|xx xx xx xx	|Color A (변수형 파악 못함)	|
|16	|0x 00 00 00	|Raycast Target (bool)	|
|17	|00 00 00 00	|아직 파악 불가	|
|18	|7B 00 00 00	|아래 Text의 Size	|
|Text||`text1`|
|19	|xx 00 00 00	|아직 파악 불가	|
|20	|xx xx 00 00	|아직 파악 불가	|
|21	|00 00 00 00	|아직 파악 불가	|
|22	|xx xx 00 00	|Font Size (255 이하 byte / 256 이상 short or int)	|
|23	|00 00 00 00	|아직 파악 불가	|
|24	|0x 00 00 00	|Best Fit (bool)	|
|25	|xx xx 00 00	|Best Fit Min Size (255 이하 byte / 256 이상 short or int)	|
|26	|xx xx 00 00	|Best Fit Max Size (255 이하 byte / 256 이상 short or int)	|
|27	|0x 00 00 00	|Horizontal Alignment (0+1+2: 좌중우)<br>Vertical Alignment (0+3+6: 상중하)|
|28	|0x 00 00 00	|Align by Geometry (bool)	|
|29	|0x 00 00 00	|Rich Text (bool)	|
|30	|0x 00 00 00	|Horizontal Overflow (bool)	|
|31	|0x 00 00 00	|Vertical Overflow (bool)	|
|32	|xx xx xx xx	|Line Spacing (float)	|
|33	|xx xx 00 00	|Text Size (255 이하 byte / 256 이상 short or int)	|
|Text|	Text Line.  |Text 내용이 들어가는 공간.<br>뒤 첫 byte는 00으로 채워지고<br> 4byte를 덜채웠으면 00으로 채워짐.||

`text1` 내용: UnityEngine.UI.MaskableGraphic+CullStateChangedEvent, UnityEngine.UI, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null

Unity Object의 Component로 들어가는 Text (Script) 분석.<br>
byte 표기는 16진수(hex)이며, 4byte씩 처리하는 유니티의 특징 상 4byte 단위로 번호를 매겼다.<br>
같거나 비슷한 기능을 할 것으로 생각되는 단위는 색으로 묶어서 표시했다.<br>
아직 파악되지 않은 단위는 추후 추가할 것이다.

 02는 소속된 Object의 번호값을 unsigned byte형으로 갖는다. 번호가 256 이상이 되면 unsigned short 또는 unsigned int32형으로 바뀌게 된다.<br>
 04는 Object가 아닌 Text (Script) 자신의 Active 상태를 bool형 값으로 갖는다.<br>
이 값이 false, 즉 0이면 Object가 Active 상태더라도 텍스트를 출력하지 않는다.<br>
 09 ~ 11은 확실하진 않으나 Material의 fileID에 따라서 값이 변하는 걸로 파악된다. Material이 None이면 모두 0값을 갖는다.<br>
 12 ~ 15는 Color RGB 그리고 명도의 A 값을 받는다. 하지만 '255'가 float형의 '1'값인 00 00 80 3F을 갖고 '50'이 C9 C8 48 3E (float형으로 0.1960784)을, '100'이 C9 C8 C8 3E을 가져서 변수형을 파악하려면 조금 더 분석이 필요하다.<br>
 16 은 Raycast Target의 Active 상태를 bool 형 값으로 갖는다.<br>
 18 밑의 Text는 숨겨진 속성의 m_Typename으로 보이며 18은 m_Typename 내용의 byte size를 갖는 것으로 보인다. ([참고])<br>
 22는 폰트의 크기 값을, 24 ~ 26은 Best Fit 관련 값을 갖는다.<br>
 27은 텍스트의 정렬 형식을 정한다. Horizontal은 왼쪽, 가운데, 오른쪽 정렬을, Vertical은 위쪽, 가운데, 밑쪽 정렬을 정한다. 정해진 형식에 따라 값에 각각 0, 1, 2, 0, 3, 6을 더한다. 예를 들어 가운데, 가운데 정렬은 +1 +3으로 4, 오른쪽, 밑 정렬은 +2 + 6으로 8 값을 갖는다.<br>
 28은 Align by Geometry, 29는 Rich Text를 사용하는가를 묻는 bool값을 갖는다.<br>
 30 ~ 31은 각각 text box의 가로, 세로 범위를 넘을 수 있는가 없는가를 결정한다. false라면 넘어간 text 내용은 잘리게된다.<br>
 32는 text의 줄을 띄웠을 때 띄워지는 줄 수를 의미한다. 기본값은 00 00 80 3F (float 1)이다.<br>
 33은 text 내용의 전체 byte size를 가진다.<br>
 34는 text안에 들어갈 내용으로 마지막 byte뒤엔 00 byte가 하나 따라붙으며, 만약 4 byte 단위를 모두 채우지 못했다면 나머지도 00으로 채워진다.<br>
 예를 들어서 'const'를 넣는다고 한다면 33는 [ 05 00 00 00 ]이 되고,<br>
 34는 [ 63 6F 6E 73 | 74 00 00 00 ]이 된다.<br>
 'byte'라면 33은 [ 04 00 00 00], 34는 [ 62 79 74 65 | 00 00 00 00 ] 이 된다.

 텍스트 내용을 처음 정해진 단위 이상으로 번역하면 crash가 뜬다. 만약 text내용 주소가 19 40h에서 19 4Bh까지였다면 아무리 size값을 변경해도 19 4Bh 이상 작성하면 asset파일 전체가 망가지게 된다. asset파일의 전체 byte값을 수정해도 안되는 걸로 보아, 더 깊게 분석해봐야 할 것 같다.

[Diaries of a Spaceport Janitor]: https://store.steampowered.com/app/436500/Diaries_of_a_Spaceport_Janitor/
[참고]: https://github.com/neuecc/UniRx/blob/master/Assets/Plugins/UniRx/Examples/Sample12Scene.unity