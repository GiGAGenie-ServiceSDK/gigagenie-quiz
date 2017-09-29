# GiGA Genie 단어 퀴즈 게임

GiGA Genie 서비스SDK를 이용한 단어 퀴즈 게임입니다. 
8초 간격으로 힌트를 보여주고 퀴즈 정답을 맞추는 게임입니다.

![quiz](https://user-images.githubusercontent.com/32326946/31002221-3a035f92-a524-11e7-9f1e-1e8b25130654.png)

### 사용한 API
음성 필터 API를 이용하여 발화로 '정답', '힌트'를 할 수 있도록 구현했습니다.

 1. `voice.setVoiceFilter`로 음성 필터를 적용할 단어를 등록합니다.

        function setVoiceFilter() {
		      options = {};
		      options.keyword = [ "정답", "힌트", "다시" ];
		      gigagenie.voice.setVoiceFilter(options, function(result_cd, result_msg, extra) {
			      if (result_cd === 200) {
				        //alert(result_cd);
			    }
			    console.log("gigagenie.voice.setVoiceFilter - result_cd:" + result_cd);
			    console.log("gigagenie.voice.setVoiceFilter - result_msg:" + result_msg);
			    console.log("gigagenie.voice.setVoiceFilter - extra:" + JSON.stringify(extra));
		});
	    };

 2. `voice.onVoiceFilterMsg`로 음성 필터 적용 메시지 수신을 설정합니다.
 
        gigagenie.voice.onVoiceFilterMsg = function(message) {
		      var msg = "음성인식 결과 : " + message;
		      //다시하기
		      if (message.indexOf("다시") >= 0) {
			      refresh();//다시
		      }
		      //정답 확인 시도
		      else if (message.indexOf("정답") >= 0) {
			      var answer_txt = message.replace("정답", "").replace(/ /gi, "");
			
			      var strArray = message.split(" ");
			      var extractAnswer = strArray[1];
			
			      $("#input_answer").val(extractAnswer);//텍스트 입력
			      go();//정답확인
		      }
	      };
## License

Copyright 2017 KT corp.

Licensed to the Apache Software Foundation (ASF) under one or more contributor
license agreements.  See the NOTICE file distributed with this work for
additional information regarding copyright ownership.  The ASF licenses this
file to you under the Apache License, Version 2.0 (the "License"); you may not
use this file except in compliance with the License.  You may obtain a copy of
the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  See the
License for the specific language governing permissions and limitations under
the License.