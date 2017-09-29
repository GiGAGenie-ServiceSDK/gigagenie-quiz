# GiGA Genie 단어 퀴즈 게임

GiGA Genie 서비스SDK를 이용한 단어 퀴즈 게임입니다. 

### 사용한 API
음성 필터 API를 이용하여 구현했습니다.

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

 2. `voice.onVoiceFilterMsg`로 음성 필터 적용 메시지 수신을 설정했습니다.
 
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
