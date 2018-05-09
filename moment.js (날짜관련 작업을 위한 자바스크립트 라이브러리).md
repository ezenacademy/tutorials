## moment.js (날짜관련 작업을 위한 자바스크립트 라이브러리)

**Moment.JS** 는 날짜(Date)형식의 데이터의 파싱, 검증, 조작 그리고 화면에 출력하는 작업을 위해 만들어진 아주 유용한 라이브러리이다. 

■ 인스톨  
<http://momentjs.com/> 에서 다운로드 하여 사용할 페이지에 로드시켜 준다.

 ■ 준비

```
// moment를 초기화 한다
var m = moment();
 
// format으로 출력한다
var output = m.format("YYYY년MM월DD일 HH:mm:ss dddd");
console.log(output);  // => 2016년07월12일 12:34:56 Wednesday 
```

■ 사용 방법

moment 개체에는 많은 초기화 방법이 준비되어 있다. 특히 두 번째 인수로 입력 값의 포맷을 지정하는 기능 덕분에 어떠한 날짜 형식에서도 유연하게 객체를 생성 할 수 있도록 되어있다.

```
// 현재시각
moment();
 
// 밀리 초로 지정
moment(1368543600000); 
 
// 타임스탬프(초)로 지정
moment.unix(1368543600);
 
// Date.parse에서 해석 가능한 문자열로 지정
moment("June 12, 2016");
 
// Date오브젝트로부터 초기화
moment(new Date(2016, 7, 12));
 
// 배열로부터 초기화
moment([2016, 7, 12]); // ※month는 -1한 값을 지정
 
// 다른 moment오브젝트로부터 초기화
moment(moment([2016, 7, 12]));
  
// 제2 인수로 입력값 포맷을 지정하여 초기화
moment("12-07-2016", "DD-MM-YYYY");
moment("20160712", "YYYYMMDD");
moment("2016년07월12일", "YYYY년MM월DD일"); // 실제로는"YYYYMMDD"만으로 지정해도 된다.
moment(1368543600 + "", "X");
```

※더 자세한 포맷 지정 방법에 대해서는 [이곳](http://momentjs.com/docs/#/parsing/string-format/)을 참조.

■ 출력 방법

```
var m = moment();
 
// format을 지정하여 출력
m.format("YYYY년MM월DD일 ddd");
 
// 각 단위 메소드
m.year();    // 년
m.month();   // 월 ※ 0〜11의 값
m.date();   // 일
m.day();    // 요일
m.hours();    // 시
m.minutes();  // 분
m.seconds();  // 초
m.milliseconds();  // 밀리 초  
각 단위 당 메서드는 값을 취득하거나 설정하여 사용된다. 인수를 넘겨주면 setter, 인수가 없으면 getter로 취급한다. 또한 예에 따라 month은 0~11의 값을 취급한다. 
m.month (4)을 set하면 5월의 moment 객체가지만,그 m.month ()를 get 을 취하면 현재 달의 수치가 반환된다.
 
var m = moment("2016-07-12", "YYYYMMDD");
m.month(); // => 0
m.month(10).format("YYYY-MM-DD"); // => 2016-07-12
```

 ■ 사용 방법 (응용편)  
 
 **▷ 요일을 한글로 출력하고 싶을 경우**

```
// lang:ko를 등록한다. 한번 지정하면 자동적으로 사용된다.
moment.lang('ko', {
    weekdays: ["일요일","월요일","화요일","수요일","목요일","금요일","토요일"],
    weekdaysShort: ["일","월","화","수","목","금","토"],
});
 
// moment를 생성
var m = moment("May 15, 2013");
 
// 한국어로 출력
m.format("MM/DD (ddd) dddd"); // => 07/12 (수) 수요일
 
// 다시 영어로 출력하고 싶을 때
m.lang("en").format("MM/DD (ddd) dddd"); // => 07/12 (Wed) Wednesday
```

 

**▷ 이번달 1일의 요일을 수값으로 얻기**

```
// day메소드가「요일」(0〜6) 으로 반환되며 date 메소드에서는 「일」 (1〜31)로 반환된다. 
moment().date(1).day(); // => 3  （수요일）
```

**▷ 이번주 월요일의 정확한 타임스탬프 취득**

```
moment()
  .day(1)     // day로 요일 지정. 0:일요일 〜 6:토요일
  .hours(12)  // 12시를 지정
  .minutes(0).seconds(0).milliseconds(0) // 이걸 지정하지 않으면 현재 시각의 분,초가 지정된다.
  .format("X"); // => 1368414000
```

**▷ 지정한 날이 존재하는지 확인**

```
moment("2016-02-30", "YYYY-MM-DD").isValid(); // => false
```

**▷ 오늘부터 30일 후의 날짜 취득**

```
moment().add("days", 30).format("YYYY년MM월DD일"); // => 2016년08월11일
```

**▷ 이번 달은 며칠까지 있는지 확인**

```
moment().daysInMonth() // => 31
```

**▷ 특정일로부터 며칠 지났는지 확인**

```
moment().diff(moment([2016, 3, 1]), "days");
```

**▷ 날짜A가 날짜B보다 미래인지 체크**

```
var momentA = moment([2016, 3, 1]);
var momentB = moment([2016, 5, 1]);
momentA.isAfter(momentB); // => false
```

**▷ moment 오브젝트의 클론 생성**

```
var baseMoment = moment();
var cloneMoment = baseMoment.clone();
```

 이상 개발에 특히 도움이 될만한 것들을 모아보았다. 이외에도 많은 기능이 moment.js에 구현되어 있으므로 다음의 문서를 참고하면 된다. [Docs](http://momentjs.com/docs/)

```html
<!doctype html>
<html lang="ko">
 <head>
  <title>Document</title>
  <meta charSet='UTF-8'>
  <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/moment@2.22.1/moment.min.js"></script>
  <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/moment@2.22.1/locale/ko.js"></script>
  <script type="text/javascript">
  <!--
	var d= new Date(); 		 				 
	var ISOData = d.toISOString();           
	var ISODate = ISOData.split("T",1);      
	document.write("<hr>");
	document.write("일반날짜 사용");
	document.write("<br><hr>");
	document.write(d + "<br>");
	document.write(ISOData + "<br>");
	document.write(ISODate + "<br>");
	document.write("<hr>");
	document.write("moment 사용");
	document.write("<br><hr>");
	document.write(moment().format('MMMM Do YYYY, h:mm:ss a') + "<br>");
	document.write(moment().format('dddd') + "<br>");
	document.write(moment().format("MMM Do YY") + "<br>");
	document.write(moment().format('YYYY [escaped] YYYY') + "<br>");
	document.write(moment().format('YYYY[-]MM[-]DD') + "<br>");
	document.write(moment().format('YYYY년 MM월 DD일 dddd (a) hh시 mm분 ss초 ') + "<br>");
  //-->
  </script>
 </head>
 <body>
  
 </body>
</html>
```

```html
<!doctype html>
<html lang="ko">
 <head>
  <title>Document</title>
  <meta charSet='UTF-8'>
  <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/moment@2.22.1/moment.min.js"></script>
  <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/moment@2.22.1/locale/ko.js"></script>
  <script type="text/javascript">
  <!--
	var time1 = "2017-02-01T12:25:00Z"
	var time2 = "2017-02-04T12:20:00Z"
	function dateFromISO(isostr) {
		var parts = isostr.match(/\d+/g);
		return new Date(parts[0], parts[1] - 1, parts[2], parts[3], parts[4], parts[5]);
	};

	document.write("<hr>");
	document.write("문자열에서 날짜데이터 구하기");
	document.write("<br><hr>");
	document.write(time1 + "<br>");
	var parts = time1.match(/\d+/g);
	for(var i in parts){
		document.write(parts[i] + "<br>");
	}

	document.write("<hr>");
	document.write("일반날짜 사용하여 시간 간격구하기");
	document.write("<br><hr>");
	var ParsedTime1= dateFromISO(time1);
	var ParsedTime2= dateFromISO(time2);
	var timeDifference = ParsedTime2-ParsedTime1 ;  // 출력 단위 밀리초(ms)

	document.write(ParsedTime1 + "<br>");
	document.write(ParsedTime2 + "<br>");
	document.write("ParsedTime2-ParsedTime1<br>");
	document.write(timeDifference + "<br>");

	document.write("<hr>");
	document.write("moment 사용하여 시간 간격구하기");
	document.write("<br><hr>");
	var ms = moment(time2,"YYYY-MM-DDTHH:mm:ssZ").diff(moment(time1,"YYYY-MM-DDTHH:mm:ssZ"));
	// 출력 단위 밀리초(ms)
	document.write("moment(time2,'YYYY-MM-DDTHH:mm:ssZ').diff(moment(time1,'YYYY-MM-DDTHH:mm:ssZ')<br>");
	document.write(ms + "<br>");
  //-->
  </script>
 </head>
 <body>
  
 </body>
</html>
```

```html
<!doctype html>
<html lang="ko">
 <head>
	<title>Document</title>
	<meta charSet='UTF-8'>
	<title>Bootstrap 3 Datepicker</title>

	<link rel="stylesheet" type="text/css" media="screen" href="http://maxcdn.bootstrapcdn.com/bootstrap/3.3.1/css/bootstrap.min.css" />
	<link rel="stylesheet" href="http://maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
	<link href="http://cdn.rawgit.com/Eonasdan/bootstrap-datetimepicker/e8bddc60e73c1ec2475f827be36e1957af72e2ea/build/css/bootstrap-datetimepicker.css" rel="stylesheet">

	<!-- HTML5 shim and Respond.js IE8 support of HTML5 elements and media queries -->
	<!--[if lt IE 9]>
	<script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
	<script src="https://oss.maxcdn.com/libs/respond.js/1.3.0/respond.min.js"></script>
	<![endif]-->
	<script type="text/javascript" src="http://code.jquery.com/jquery-2.1.1.min.js"></script>
	<script type="text/javascript" src="http://maxcdn.bootstrapcdn.com/bootstrap/3.3.1/js/bootstrap.min.js"></script>
	<script type="text/javascript" src="https://cdn.jsdelivr.net/npm/moment@2.22.1/moment.min.js"></script>
	<script type="text/javascript" src="https://cdn.jsdelivr.net/npm/moment@2.22.1/locale/ko.js"></script>
	<script src="http://cdn.rawgit.com/Eonasdan/bootstrap-datetimepicker/e8bddc60e73c1ec2475f827be36e1957af72e2ea/src/js/bootstrap-datetimepicker.js"></script>
 </head>
 <body>
  <div class="row">
	<div class="col-xs-4">
		<input type="text" id="test_input" class="form-control">
	</div>
</div>
<script type="text/javascript">
	$('#test_input').datetimepicker({
		format:"YYYY-MM-DD H:m:s"
		,defaultDate: moment().add(-7, 'day')
	});
</script>
 </body>
</html>
```

