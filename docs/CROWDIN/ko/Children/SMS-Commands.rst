SMS 명령어
**************************************************
안전유의사항
==================================================
* AndroidAPS는 SMS 문자를 통해 아이의 폰을 원격으로 조정할 수 있습니다. SMS 통신기를 활성화 했다면, 원격 명령어를 사용하기 위해 설정된 폰(부모폰)이 도난 될 수도 있는 경우도 발생할 수 있다는것을 항상 유념하세요. 따라서 최소한 PIN 코드이상의 보안으로 본인의 폰을 보호하세요.
* Bolus 혹은 프로파일 변경 등의 원격 명령들이 수행되었다면 AndroidAPS 역시 SMS 문자로 항상 알려줄 것입니다. 수신 폰 중 하나가 도난당한 경우를 대비하여 적어도 2개 이상의 폰에 확인 SMS 문자가 전송될 수 있도록 설정해놓는 것이 좋습니다.
* **SMS 원격명령을 통해 Bolus를 주입한 경우 Nightscout (NSClient, 웹사이트...)를 통해 탄수화물양을 항상 입력하여야 합니다!** 그러지 않으면 너무 낮은 COB인 상태에서 IOB가 계산될 것이고 AAPS가 당신이 너무 많은 활성 인슐린을 가지고 있다고 가정하게 되기 때문에 적절한 보정 주입이 되지 않을 수 있습니다.

사용 방법
==================================================
* AAPS와 작동하는 임시 목표와 관련된 대부분의 조정들은 인터넷에 연결된 폰에서 'NSclient 앱 <../Children/Children.html>` _ 을 통해 원격 조종이 가능합니다.
Bolus는 Nightscout를 통해 원격 주입되지 않지만, SMS 명령으로 가능합니다.
* 팔로워폰으로 아이폰(iPhone)을 사용한다면 NSClient를 사용할 수 없고 SMS 명령으로 가능합니다.

* 당신의 안드로이드폰의 환경설정에서 애플리케이션 > AndroidAPS > 권한에 들어간 뒤 SMS를 활성화하세요
* AndroidAPS의 설정 > SMS 통신기 > 허가된 전화번호에 SMS 명령을 사용할 폰번호를 입력하세요. (두개 이상의 폰번호를 입력하려면 세미콜론으로 구분해야합니다 - 예. 01012345678;01012345679) 그리고 'SMS 원격 명령 사용하기'를 활성화하세요.
* 하나 이상의 전화번호 사용을 원한다면:

  * 하나의 번호만 입력하세요.
  * SMS 명령을 보내고 확인하여 해당 전화번호가 올바르게 작동하는지 확인하십시오.
  * 다른 번호를 입력하세요. 세미콜론으로 구분하고 공백이 있으면 안됩니다.
  
    .. image:: ../images/SMSCommandsSetupSpace.png
      :alt: SMS 명령 설정


* 아래 명령어 중 하나를 선택하여 허가된 폰에서 AndroidAPS가 설치된 폰으로 SMS를 보내어봅니다. 명령어 성공 혹은 상태와 관련된 답 문자를 받게될것입니다. 필요한 경우 AndroidAPS 에서 보낸 확인 코드를 답장하여 명령을 진행하세요.

**힌트**: 많은 SMS를 사용한다면 SMS 제한없는 요금제를 사용하면 좋습니다.

명령어
==================================================

SMS 명령을 전송할때 대문자와 소문자는 구별하지 않습니다.

SMS 명령어는 영어로만 전송하여야 하며, 응답이 `번역 <../translations.html#translate-strings-for-androidaps-app>`된 경우 번역문으로 응답을 받게 됩니다.

.. image:: ../images/SMSCommands.png
  :alt: SMS Commands Example

Loop
--------------------------------------------------
* LOOP STOP/DISABLE
   * 응답: Loop가 중지되었습니다
* LOOP START/ENABLE
   * 응답: Loop가 실행되었습니다
* LOOP STATUS
   * 현재의 Loop의 상태에 따라 응답됩니다
      * Loop가 중지중입니다
      * Loop가 실행중입니다
      * 일시중지중 (10분)
* LOOP SUSPEND 20
   * 응답: Loop가 20분동안 일시중지되었습니다
* LOOP RESUME
   * 응답: Loop가 재실행되었습니다

CGM 데이터
--------------------------------------------------
* BG
   * 응답: Last BG: 5.6 4min ago, Delta: -0,2 mmol, IOB: 0.20U (Bolus: 0.10U Basal: 0.10U)
* CAL 120
   * 응답: 보정값 120을 전송하려면 Rrt 를 입력하고 답장하세요
   * 코드 전송 후 응답: 보정 전송됨 (**xDrip이 설치되었다면 xDrip+에서 Accept Calibrations가 활성화 되어 있어야만 합니다**)

Basal
--------------------------------------------------
* BASAL STOP/CANCEL
   * 응답: 임시Basal을 중지하려면 EmF 를 입력하고 답장하세요 [참고: 코드 EmF는 단순 예시일 뿐입니다]
* BASAL 0.3
   * 응답: 30분 동안 Basal 0.3U/h 주입하려면 Swe 를 입력하고 답장하세요
* BASAL 0.3 20
   * 응답: 20분 동안 Basal 0.3U/h 주입하려면 Swe 를 입력하고 답장하세요
* BASAL 30%
   * 응답: 30 분 동안 Basal 30% 주입하려면 Swe을 입력하고 답장하세요
* BASAL 30% 50
   * 응답: 50 분 동안 Basal 30% 주입하려면 Swe을 입력하고 답장하세요

Bolus
--------------------------------------------------
원격 Bolus 주입은 15분 내에 허용되지 않습니다 - 이 값은 2개의 폰번호가 추가되었을 시만 수정가능합니다. 따라서 응답은 최근 Bolus 주입시간에 따라 달라지게 됩니다.

* BOLUS 1.2
   * 응답 A: Bolus 1.2U을 주입하려면 Rrt를 입력하고 답장하세요
   * 응답 B: 원격 주입이 불가능합니다. 나중에 다시 시도해주세요.
* BOLUS 0.60 MEAL
   * MEAL 옵션을 지정하는 경우 MEAL 임시목표가 설정됩니다 (기본값은 45분동안 목표값 90 mg/dL입니다).
   * 응답 A: MEAL Bolus 0.6U을 주입하려면 Rrt를 입력하고 답장하세요
   * 응답 B: 원격 주입이 불가능합니다. 
* CARBS 5
   * 응답: 12:45에 5g을 입력하려면 EmF를 입력하고 답장하세요
* CARBS 5 17:35/5:35PM
   * 응답: 17:35에 5g을 입력하려면 EmF를 입력하고 답장하세요
* EXTENDED STOP/CANCEL
   * 응답: 확장 Bolus를 중지하려면 EmF 를 입력하고 답장하세요
* EXTENDED 2 120
   * 응답: 120분 동안 확장 Bolus 2U 주입하려면 EmF 를 입력하고 답장하세요

프로파일
--------------------------------------------------
* PROFILE STATUS
   * 응답: Profile1
* PROFILE LIST
   * 응답: 1.`Profile1` 2.`Profile2`
* PROFILE 1
   * 응답: 프로파일 Profile1 100%로 변경하려면 Any 를 입력하고 답장하세요
* PROFILE 2 30
   * 응답: 프로파일 Profile2 30%로 변경하려면 Any 를 입력하고 답장하세요

기타
--------------------------------------------------
* TREATMENTS REFRESH
   * 응답: NS에서 관리 새로고침
* NSCLIENT RESTART
   * 응답: NSCLIENT RESTART 1 receivers
* PUMP
   * 응답: Last conn: 1 minago Temp: 0.00U/h @11:38 5/30min IOB: 0.5U Reserv: 34U Batt: 100
* SMS DISABLE/STOP
   * 응답: SMS 원격 기능을 비활성화려면 Any를 입력하고 답장하세요. AAPS 마스터폰을 통해서만 다시 활성화할 수 있습니다.
* TARGET MEAL/ACTIVITY/HYPO   
   * 응답: 임시목표 MEAL/ACTIVITY/HYPO를 설정하려면 Any를 입력하고 답장하세요
* TARGET STOP/CANCEL   
   * 응답: 임시목표를 취소하려면 Any를 입력하고 답장하세요
* HELP
   * 응답: BG, LOOP, TREATMENTS, .....
* HELP BOLUS
   * 응답: BOLUS 1.2 BOLUS 1.2 MEAL

문제해결
==================================================
무한 SMS
--------------------------------------------------
동일한 메세지를 끊임없이 계속 수신하는 경우 (예. 프로파일 변경) 아마도 다른 앱과 무한루프가 되게 설정되었을 가능성이 있습니다. 예를 들면 그 앱이 xDrip+일 수가 있습니다. 따라서 그런경우엔, xDrip+(또는 다른앱)이 treatments를 NS에 업로드하지 않도록 하세요. 

다른 앱이 여러 휴대 전화에 설치된 경우 모든 휴대 전화에서 업로드를 비활성화해야합니다.

삼성폰에서 SMS 명령어가 작동하지 않을 경우
--------------------------------------------------
갤럭시 S10 폰 업데이트 이후 SMS 명령어가 작동하지 않는다는 문제가 보고되었습니다. '채팅 메세지로 보내기'를 비활성화하면 해결될 수 있습니다.

.. image:: ../images/SMSdisableChat.png
  :alt: 채팅 메세지로 보내기 비활성화하기
