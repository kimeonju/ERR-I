<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>ERR · Eco Rapid Rail (오프라인 전용)</title>
<style>
:root{color-scheme:dark;--bg:#0b1018;--panel:#151e2b;--line:#304154;--text:#edf4fc;--muted:#a7b8cb;--green:#47e59b;--yellow:#ffd166;--red:#ff6474;--blue:#5bb9ff}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
body{margin:0;background:var(--bg);color:var(--text);font:14px/1.5 system-ui,-apple-system,sans-serif;user-select:none}
header{padding:14px 18px;background:#111b29;border-bottom:1px solid var(--line);display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:10px}
header h1{font-size:20px;margin:0}header p{color:var(--muted);margin:3px 0 0;font-size:12px}
.route-selector{display:flex;align-items:center;gap:6px}
main{max-width:1450px;margin:auto;padding:12px;display:grid;grid-template-columns:repeat(12,minmax(0,1fr));gap:10px}
.panel{background:var(--panel);border:1px solid var(--line);border-radius:10px;padding:12px;min-width:0}
.s12{grid-column:span 12}.s8{grid-column:span 8}.s6{grid-column:span 6}.s4{grid-column:span 4}
h2{font-size:15px;margin:0 0 10px}h3{font-size:13px;margin:10px 0 6px}
.muted,small{color:var(--muted)}
.row{display:flex;align-items:center;gap:6px;flex-wrap:wrap}.between{justify-content:space-between}
.g2{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:6px}
.g3{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:6px}
.stat{background:#0d1520;border:1px solid var(--line);padding:8px 10px;border-radius:8px;min-width:0}
.stat small{display:block;font-size:11px}.stat strong{font-size:16px}
.big{font-size:38px;font-weight:800;line-height:1.1}.unit{color:var(--muted)}
button,input,select{background:#0b1420;color:var(--text);border:1px solid #41566d;border-radius:6px;padding:8px 10px;font:inherit}
button{cursor:pointer;touch-action:manipulation}button:active{border-color:var(--blue);background:#18283b}
button.active{background:#174b3a;border-color:var(--green)}
button.danger{border-color:#943947;background:#2a1216}button.warn{border-color:#8a5d25}
input[type=number]{width:100%;min-width:50px}select{max-width:100%}
label{display:block;color:var(--muted);margin:5px 0 3px;font-size:12px}
.progress{height:10px;background:#08101a;border-radius:99px;overflow:hidden;border:1px solid var(--line);margin-top:4px}
.progress span{display:block;height:100%;background:var(--green);width:0%}
.badge{display:inline-block;padding:2px 8px;border-radius:99px;background:#27364a;font-size:12px;font-weight:bold}
.good{color:var(--green)}.warntext{color:var(--yellow)}.bad{color:var(--red)}
.track{height:80px;position:relative;background:linear-gradient(#17283a,#0b121d);border-radius:99px;overflow:hidden;border:1px solid var(--line);margin-top:6px}
.rail{position:absolute;left:0;right:0;top:53%;border-top:3px solid #72869c}
.mark{position:absolute;top:25%;width:10px;height:22px;background:var(--blue);border:2px solid #e7f6ff;border-radius:3px;transform:translateX(-50%)}
.mark.user{background:var(--green)}.mark.target{background:var(--yellow)}
.tracklabel{position:absolute;top:4px;font-size:10px;color:var(--muted);transform:translateX(-50%);white-space:nowrap}
table{width:100%;border-collapse:collapse;font-size:11px}
th,td{text-align:left;padding:6px 4px;border-bottom:1px solid var(--line);white-space:nowrap}
th{color:var(--muted)}.scroll{overflow:auto;max-height:250px}
.log{height:120px;overflow:auto;background:#080e16;border:1px solid var(--line);border-radius:6px;padding:6px;font:11px/1.5 monospace}
.log div{border-bottom:1px solid #1b2838;padding:2px 0}
hr{border:0;border-top:1px solid var(--line);margin:10px 0}
#timetable tr.running,#timetable tr.running td{color:#47e59b}
#timetable tr.completed,#timetable tr.completed td{color:#ff6474}
#timetable tr.pending,#timetable tr.pending td{color:#ffd166}
#otherTrains tr.running,#otherTrains tr.running td{color:#47e59b}
#otherTrains tr.completed,#otherTrains tr.completed td{color:#ff6474}
#otherTrains tr.pending,#otherTrains tr.pending td{color:#ffd166}
@media(max-width:850px){.s8,.s6,.s4{grid-column:span 12}.big{font-size:32px}}
</style>
</head>
<body>
<header>
<div>
<h1>ERR · Eco Rapid Rail</h1>
<p id="headerSub">오프라인 완전 호환 철도 시뮬레이터</p>
</div>
<div class="row">
<button id="saveGame" class="active">💾 저장</button>
<button id="loadGame">📂 불러오기</button>
<div class="route-selector" style="margin-left:6px;">
<label for="routeSelect" style="margin:0;font-weight:bold;">노선:</label>
<select id="routeSelect">
<option value="gyeongbu">경부선 (서울 ~ 부산센텀)</option>
<option value="honam">호남선 (서울 ~ 목포)</option>
<option value="jeolla">전라선 (서울 ~ 여수엑스포)</option>
<option value="gyeongjeon">경전선 (서울 ~ 진주)</option>
<option value="donghae">동해선 (서울 ~ 포항)</option>
</select>
</div>
</div>
</header>
<main>
<section class="panel s8">
<div class="row between"><h2>운전실 · ERR 001</h2><span id="clock" class="badge">--:--:--</span></div>
<div class="g2">
<div class="stat"><small>현재 속도</small><span id="speed" class="big">0</span> km/h<div class="progress"><span id="speedbar"></span></div></div>
<div class="stat"><small>현재 위치</small><strong id="station">서울</strong><div id="distance" class="muted">0.0 km</div>다음 역: <strong id="next">광명</strong></div>
</div>
<div class="g3" style="margin-top:6px">
<div class="stat"><small>노치</small><strong id="notch">N</strong></div>
<div class="stat"><small>선로 제한속도</small><strong id="limit">330 km/h</strong></div>
<div class="stat"><small>목표속도</small><strong id="targetSpeed">330 km/h</strong></div>
<div class="stat"><small>VCB</small><strong id="vcb">OFF</strong></div>
<div class="stat"><small>팬터그래프</small><strong id="pant">하강</strong></div>
<div class="stat"><small>상태</small><strong id="status">정차</strong></div>
</div>
<h3>운전 제어</h3>
<div class="row">
<button id="forward">F · 전진</button><button id="reverse">R · 후진</button>
<button id="vcbButton">O · VCB</button><button id="pantButton">P · 팬터그래프</button>
<button id="coast">C · 타행</button><button id="eb" class="danger">비상제동</button><button id="release">제동 해제</button>
</div>
<h3>역행 / 제동 노치</h3>
<div class="row">
<button data-notch="P1">P1</button><button data-notch="P2">P2</button><button data-notch="P3">P3</button><button data-notch="P4">P4</button><button data-notch="P5">P5</button><button data-notch="N">N</button>
<button data-notch="B1">B1</button><button data-notch="B2">B2</button><button data-notch="B3">B3</button><button data-notch="B4">B4</button><button data-notch="B5">B5</button>
</div>
<p class="muted" style="font-size:11px">P5: +1.8 km/h/s · B5: −1.8 km/h/s · Space: 경계 페달 · T: 추월 모드</p>
</section>

<section class="panel s4">
<h2>추월 모드 · 앞앞차 기준</h2>
<button id="overtake" class="warn">추월 모드 OFF</button>
<label for="baseTrain">기준 열차</label><select id="baseTrain" style="width:100%"></select>
<div class="g2" style="margin-top:6px">
<div class="stat"><small>앞앞차</small><strong id="frontFront">미검출</strong></div>
<div class="stat"><small>간격</small><strong id="gap">- km</strong></div>
<div class="stat"><small>목표 간격</small><strong id="gapSetting">2.0 km</strong></div>
<div class="stat"><small>간격 제어</small><strong id="gapStatus">대기</strong></div>
</div>
<label for="gapInput">목표 간격 (km)</label>
<div class="row"><input id="gapInput" type="number" min=".5" max="20" step=".5" value="2"><button id="setGap">적용</button></div>
<p id="autoExplanation" class="muted" style="font-size:11px">추월 모드 OFF</p>
<div class="stat"><small>목표 제한속도</small><strong id="autoLimit">330 km/h</strong></div>
</section>

<section class="panel s12">
<h2>노선 및 열차 위치</h2><div class="track" id="track"><div class="rail"></div><div id="trackMarks"></div></div>
<div class="row between" id="trackTerminals"><span class="muted">서울 0 km</span><span class="muted">부산센텀 417.4 km</span></div>
</section>

<section class="panel s6">
<h2>안전 · 경계장치</h2>
<div class="g2">
<div class="stat"><small>감속 예고</small><strong id="speedWarning" class="good">정상</strong></div>
<div class="stat"><small>속도 초과</small><strong id="overspeed" class="good">정상</strong></div>
<div class="stat"><small>경계장치</small><strong id="vigilance" class="good">정상</strong></div>
<div class="stat"><small>비상제동</small><strong id="emergencyStatus">해제</strong></div>
</div>
<p class="muted" style="font-size:11px">55초 동안 입력이 없으면 경고음, 추가 15초 동안 응답이 없으면 비상제동합니다.</p>
<button id="pedal" style="width:100%;padding:10px;font-weight:bold">Space · 경계 페달</button>
<span id="pedalTime" class="muted" style="display:block;margin-top:4px;font-size:11px">입력 대기</span>
</section>

<section class="panel s6">
<h2>진로 · 출입문</h2>
<div class="g3"><button id="turnL">4 · 좌측</button><button id="turnS" class="active">5 · 직진</button><button id="turnR">6 · 우측</button></div>
<p style="margin:6px 0">현재 진로: <strong id="turnout">직진</strong></p><hr>
<div class="g2">
<div class="stat"><strong>좌측 출입문</strong><p id="leftStatus" class="muted" style="font-size:11px;margin:4px 0">닫힘 · 허가 없음</p><button id="permitL">2 · 허가</button> <button id="leftDoor">W · 문</button></div>
<div class="stat"><strong>우측 출입문</strong><p id="rightStatus" class="muted" style="font-size:11px;margin:4px 0">닫힘 · 허가 없음</p><button id="permitR">3 · 허가</button> <button id="rightDoor">E · 문</button></div>
</div>
</section>

<section class="panel s6">
<h2>시간표 · ERR 001</h2>
<div class="scroll"><table><thead><tr><th>역</th><th>도착</th><th>출발</th><th>거리</th><th>상태</th></tr></thead><tbody id="timetable"></tbody></table></div>
</section>

<section class="panel s6">
<h2>다른 KTX 운행 현황</h2>
<div class="scroll"><table><thead><tr><th>열차</th><th>상태</th><th>위치</th><th>속도</th><th>ERR와 거리</th></tr></thead><tbody id="otherTrains"></tbody></table></div>
</section>

<section class="panel s12"><h2>운행 기록</h2><div id="log" class="log"></div></section>
</main>

<script>
function $(id){ return document.getElementById(id); }
var DAY = 86400;

var memStorage = {};
function safeSave(key, val){
 try {
  if (window.localStorage) { localStorage.setItem(key, val); }
  else { memStorage[key] = val; }
 } catch(e) { memStorage[key] = val; }
}
function safeLoad(key){
 try {
  if (window.localStorage) { return localStorage.getItem(key) || memStorage[key] || null; }
  return memStorage[key] || null;
 } catch(e) { return memStorage[key] || null; }
}

var audioCtx = null;
function initAudio() {
 try {
  if (!audioCtx) {
   var AudioClass = window.AudioContext || window.webkitAudioContext;
   if (AudioClass) { audioCtx = new AudioClass(); }
  }
  if (audioCtx && audioCtx.state === 'suspended') {
   audioCtx.resume();
  }
 } catch(e) {}
}

var routes = {
 gyeongbu: {
  name: "경부선", startName: "서울", endName: "부산센텀", len: 417.4, startHour: 5, startMinute: 0,
  stations: [
   {name:"서울",km:0,limit:330,arr:"",dep:5*3600},
   {name:"광명",km:17,limit:330,arr:5*3600+20*60,dep:5*3600+23*60},
   {name:"천안아산",km:96.5,limit:330,arr:5*3600+50*60,dep:5*3600+53*60},
   {name:"오송",km:131.5,limit:330,arr:6*3600+10*60,dep:6*3600+13*60},
   {name:"대전",km:166.3,limit:330,arr:6*3600+30*60,dep:6*3600+35*60},
   {name:"김천(구미)",km:227.3,limit:330,arr:7*3600+0*60,dep:7*3600+3*60},
   {name:"동대구",km:293.1,limit:330,arr:7*3600+20*60,dep:7*3600+25*60},
   {name:"경주",km:346.8,limit:330,arr:7*3600+43*60,dep:7*3600+46*60},
   {name:"태화강",km:380,limit:330,arr:8*3600+0*60,dep:8*3600+3*60},
   {name:"부산센텀",km:417.4,limit:330,arr:8*3600+23*60,dep:""}
  ],
  majorMarks: [{n:"서울",k:0},{n:"광명",k:17},{n:"대전",k:166.3},{n:"동대구",k:293.1},{n:"부산센텀",k:417.4}]
 },
 honam: {
  name: "호남선", startName: "서울", endName: "목포", len: 373.8, startHour: 5, startMinute: 10,
  stations: [
   {name:"서울",km:0,limit:330,arr:"",dep:5*3600+10*60},
   {name:"용산",km:3.2,limit:330,arr:5*3600+15*60,dep:5*3600+17*60},
   {name:"광명",km:17.7,limit:330,arr:5*3600+27*60,dep:5*3600+30*60},
   {name:"오송",km:132.6,limit:330,arr:6*3600+18*60,dep:6*3600+21*60},
   {name:"공주",km:164.8,limit:330,arr:6*3600+32*60,dep:6*3600+35*60},
   {name:"익산",km:208.6,limit:330,arr:6*3600+51*60,dep:6*3600+56*60},
   {name:"정읍",km:254.0,limit:330,arr:7*3600+15*60,dep:7*3600+18*60},
   {name:"광주송정",km:307.0,limit:330,arr:7*3600+38*60,dep:7*3600+43*60},
   {name:"나주",km:326.0,limit:330,arr:7*3600+53*60,dep:7*3600+56*60},
   {name:"목포",km:373.8,limit:330,arr:8*3600+18*60,dep:""}
  ],
  majorMarks: [{n:"서울",k:0},{n:"광명",k:17.7},{n:"오송",k:132.6},{n:"익산",k:208.6},{n:"광주송정",k:307.0},{n:"목포",k:373.8}]
 },
 jeolla: {
  name: "전라선", startName: "서울", endName: "여수엑스포", len: 389.0, startHour: 5, startMinute: 15,
  stations: [
   {name:"서울",km:0,limit:330,arr:"",dep:5*3600+15*60},
   {name:"용산",km:3.2,limit:330,arr:5*3600+20*60,dep:5*3600+22*60},
   {name:"광명",km:17.7,limit:330,arr:5*3600+32*60,dep:5*3600+35*60},
   {name:"오송",km:132.6,limit:330,arr:6*3600+23*60,dep:6*3600+26*60},
   {name:"익산",km:208.6,limit:330,arr:6*3600+56*60,dep:7*3600+1*60},
   {name:"전주",km:234.1,limit:330,arr:7*3600+15*60,dep:7*3600+20*60},
   {name:"남원",km:288.1,limit:330,arr:7*3600+47*60,dep:7*3600+50*60},
   {name:"곡성",km:305.7,limit:330,arr:8*3600+0*60,dep:8*3600+3*60},
   {name:"순천",km:338.9,limit:330,arr:8*3600+22*60,dep:8*3600+27*60},
   {name:"여천",km:377.9,limit:330,arr:8*3600+47*60,dep:8*3600+50*60},
   {name:"여수엑스포",km:389.0,limit:330,arr:9*3600+0*60,dep:""}
  ],
  majorMarks: [{n:"서울",k:0},{n:"오송",k:132.6},{n:"익산",k:208.6},{n:"전주",k:234.1},{n:"순천",k:338.9},{n:"여수엑스포",k:389.0}]
 },
 gyeongjeon: {
  name: "경전선", startName: "서울", endName: "진주", len: 452.0, startHour: 5, startMinute: 20,
  stations: [
   {name:"서울",km:0,limit:330,arr:"",dep:5*3600+20*60},
   {name:"광명",km:17,limit:330,arr:5*3600+37*60,dep:5*3600+40*60},
   {name:"천안아산",km:96.5,limit:330,arr:6*3600+10*60,dep:6*3600+13*60},
   {name:"오송",km:131.5,limit:330,arr:6*3600+30*60,dep:6*3600+33*60},
   {name:"대전",km:166.3,limit:330,arr:6*3600+50*60,dep:6*3600+55*60},
   {name:"동대구",km:293.1,limit:330,arr:7*3600+40*60,dep:7*3600+45*60},
   {name:"밀양",km:381.6,limit:330,arr:8*3600+23*60,dep:8*3600+28*60},
   {name:"창원중앙",km:417.2,limit:330,arr:8*3600+50*60,dep:8*3600+53*60},
   {name:"창원",km:420.8,limit:330,arr:8*3600+56*60,dep:8*3600+59*60},
   {name:"마산",km:426.4,limit:330,arr:9*3600+8*60,dep:9*3600+13*60},
   {name:"진주",km:452.0,limit:330,arr:9*3600+32*60,dep:""}
  ],
  majorMarks: [{n:"서울",k:0},{n:"대전",k:166.3},{n:"동대구",k:293.1},{n:"밀양",k:381.6},{n:"마산",k:426.4},{n:"진주",k:452.0}]
 },
 donghae: {
  name: "동해선", startName: "서울", endName: "포항", len: 365.0, startHour: 5, startMinute: 25,
  stations: [
   {name:"서울",km:0,limit:330,arr:"",dep:5*3600+25*60},
   {name:"광명",km:17,limit:330,arr:5*3600+42*60,dep:5*3600+45*60},
   {name:"천안아산",km:96.5,limit:330,arr:6*3600+15*60,dep:6*3600+18*60},
   {name:"오송",km:131.5,limit:330,arr:6*3600+35*60,dep:6*3600+38*60},
   {name:"대전",km:166.3,limit:330,arr:6*3600+55*60,dep:7*3600+0*60},
   {name:"동대구",km:293.1,limit:330,arr:7*3600+45*60,dep:7*3600+50*60},
   {name:"서경주",km:342.3,limit:330,arr:8*3600+20*60,dep:8*3600+23*60},
   {name:"포항",km:365.0,limit:330,arr:8*3600+40*60,dep:""}
  ],
  majorMarks: [{n:"서울",k:0},{n:"대전",k:166.3},{n:"동대구",k:293.1},{n:"포항",k:365.0}]
 }
};

var currentRouteKey = "gyeongbu";
var activeRoute = routes[currentRouteKey];
var LEN = activeRoute.len;
var stations = activeRoute.stations;

var speed=0, distance=0, direction=0, power=0, vcb=false, pantograph=false;
var emergency=false, leftDoor=false, rightDoor=false, allowL=false, allowR=false;
var turnout="직진", stationIndex=0, arrived=false;
var lastFrame=Date.now(), vigilanceLast=Date.now(), warningStart=null;
var overtakeMode=false, targetGap=2, targetSpeed=330, notchLabel="N";
var trains=[], heldKeys={};
var warningSoundInterval = null;

function saveGameData(){
 var data = {
  currentRouteKey: currentRouteKey, speed: speed, distance: distance, direction: direction, power: power,
  vcb: vcb, pantograph: pantograph, emergency: emergency, leftDoor: leftDoor, rightDoor: rightDoor,
  allowL: allowL, allowR: allowR, turnout: turnout, stationIndex: stationIndex, arrived: arrived,
  overtakeMode: overtakeMode, targetGap: targetGap, notchLabel: notchLabel
 };
 safeSave("err_save_data", JSON.stringify(data));
 log("게임이 성공적으로 저장되었습니다.");
 alert("게임 상태가 저장되었습니다!");
}

function loadGameData(){
 var saved = safeLoad("err_save_data");
 if(!saved){
  alert("저장된 게임 데이터가 없습니다.");
  return;
 }
 try {
  var data = JSON.parse(saved);
  currentRouteKey = data.currentRouteKey;
  activeRoute = routes[currentRouteKey];
  LEN = activeRoute.len;
  stations = activeRoute.stations;
  $("routeSelect").value = currentRouteKey;
  
  speed = data.speed;
  distance = data.distance;
  direction = data.direction;
  power = data.power;
  vcb = data.vcb;
  pantograph = data.pantograph;
  emergency = data.emergency;
  leftDoor = data.leftDoor;
  rightDoor = data.rightDoor;
  allowL = data.allowL;
  allowR = data.allowR;
  turnout = data.turnout;
  stationIndex = data.stationIndex;
  arrived = data.arrived;
  overtakeMode = data.overtakeMode;
  targetGap = data.targetGap;
  notchLabel = data.notchLabel;

  $("headerSub").textContent = activeRoute.name + " (" + activeRoute.startName + " ~ " + activeRoute.endName + ") · 오프라인 모드";
  var termEl = $("trackTerminals");
  if(termEl) termEl.innerHTML = '<span class="muted">' + activeRoute.startName + ' 0 km</span><span class="muted">' + activeRoute.endName + ' ' + LEN + ' km</span>';
  $("gapInput").value = targetGap;
  
  initTrains();
  updateTimetable();
  updateOtherTable();
  updateTrack();
  render();
  log("저장된 게임을 불러왔습니다.");
  alert("게임을 성공적으로 불러왔습니다!");
 } catch(e){
  alert("저장된 데이터를 불러오는 중 오류가 발생했습니다.");
 }
}

function changeRoute(key){
 currentRouteKey = key;
 activeRoute = routes[key];
 LEN = activeRoute.len;
 stations = activeRoute.stations;
 
 if(distance > LEN) distance = LEN;
 arrived = (distance >= LEN);
 
 stationIndex = 0;
 for(var i=0; i<stations.length; i++){
  if(stations[i].km <= distance) stationIndex = i;
 }
 
 $("headerSub").textContent = activeRoute.name + " (" + activeRoute.startName + " ~ " + activeRoute.endName + ") · 오프라인 모드";
 var termEl = $("trackTerminals");
 if(termEl) termEl.innerHTML = '<span class="muted">' + activeRoute.startName + ' 0 km</span><span class="muted">' + activeRoute.endName + ' ' + LEN + ' km</span>';
 
 initTrains();
 updateTimetable();
 updateOtherTable();
 updateTrack();
 render();
 log(activeRoute.name + " 노선으로 변경되었습니다. (속력·위치·상태 유지)");
}

function playWarningSound() {
 initAudio();
 try {
  if (!audioCtx) return;
  var osc = audioCtx.createOscillator();
  var gain = audioCtx.createGain();
  osc.type = 'sine';
  osc.frequency.setValueAtTime(880, audioCtx.currentTime);
  gain.gain.setValueAtTime(0.3, audioCtx.currentTime);
  osc.connect(gain);
  gain.connect(audioCtx.destination);
  osc.start();
  osc.stop(audioCtx.currentTime + 0.4);
 } catch(e) {}
}

function startWarningSound() {
 if (warningSoundInterval) return;
 playWarningSound();
 warningSoundInterval = setInterval(function() {
  if (warningStart !== null && !emergency) {
   playWarningSound();
  } else {
   stopWarningSound();
  }
 }, 1000);
}

function stopWarningSound() {
 if (warningSoundInterval) {
  clearInterval(warningSoundInterval);
  warningSoundInterval = null;
 }
}

function deviceSeconds(){
 var d=new Date();
 return d.getHours()*3600 + d.getMinutes()*60 + d.getSeconds() + d.getMilliseconds()/1000;
}
function pad2(n){ return (n < 10 ? '0' : '') + n; }
function deviceTimeText(){
 var d=new Date();
 return pad2(d.getHours()) + ":" + pad2(d.getMinutes()) + ":" + pad2(d.getSeconds());
}
function formatSec(sec){
 if(isNaN(sec)||sec===""||sec===null) return "-";
 var h = Math.floor(sec/3600);
 var m = Math.floor((sec%3600)/60);
 return pad2(h) + ":" + pad2(m);
}
function syncClock(){
 var el = $("clock");
 if(el) el.textContent = deviceTimeText();
}
function log(msg){
 var el = document.createElement("div");
 el.textContent = "[" + deviceTimeText() + "] " + msg;
 var logEl = $("log");
 if(logEl){
  logEl.insertBefore(el, logEl.firstChild);
  while(logEl.children.length > 100){ logEl.removeChild(logEl.lastChild); }
 }
}
function currentStationName(){
 var result = stations[0].name;
 for(var i=0; i<stations.length; i++){
  if(stations[i].km <= distance + 0.02) result = stations[i].name;
 }
 return result;
}
function nextStationIndex(){
 for(var i=0; i<stations.length; i++){
  if(stations[i].km > distance + 0.02) return i;
 }
 return -1;
}
function setNotch(v){
 initAudio();
 if(emergency && v.indexOf("B")!==0 && v!=="N") return;
 if(/^P[1-5]$/.test(v)){
  if(!vcb || !pantograph || direction===0){
   power=0; notchLabel="N"; log("역행 불가: 방향·VCB·팬터그래프 확인"); render(); return;
  }
  power = Number(v.slice(1)); notchLabel = v; emergency = false;
 }else if(/^B[1-5]$/.test(v)){
  power = -Number(v.slice(1)); notchLabel = v;
 }else{ power=0; notchLabel="N"; }
 render();
}
function setDirection(d){
 initAudio();
 if(speed > 0.1){ log("정차 후 방향 변경 필요"); return; }
 direction = d; log(d===1 ? "전진 설정" : "후진 설정"); render();
}
function applyEmergency(){
 initAudio();
 emergency = true; power = -5; notchLabel = "EB";
 stopWarningSound();
 log("비상제동 작동");
 render();
}
function releaseBrake(){
 initAudio();
 emergency = false; power = 0; notchLabel = "N"; log("비상제동 해제"); render();
}
function toggleVCB(){ initAudio(); vcb = !vcb; if(!vcb){ power=0; notchLabel="N"; } log("VCB " + (vcb ? "ON" : "OFF")); render(); }
function togglePantograph(){ initAudio(); pantograph = !pantograph; if(!pantograph){ power=0; notchLabel="N"; } log("팬터그래프 " + (pantograph ? "올림" : "내림")); render(); }
function setTurnout(v){ initAudio(); turnout = v; render(); log("진로 설정: " + v); }
function togglePermission(side){
 initAudio();
 if(side === "L"){ allowL = !allowL; if(!allowL) leftDoor = false; }
 else { allowR = !allowR; if(!allowR) rightDoor = false; }
 render();
}
function toggleDoor(side){
 initAudio();
 if(speed > 0.1){ log("주행 중 출입문 조작 불가"); return; }
 if(side === "L"){
  if(!allowL){ log("좌측 출입문 허가가 필요합니다"); return; }
  leftDoor = !leftDoor;
 }else{
  if(!allowR){ log("우측 출입문 허가가 필요합니다"); return; }
  rightDoor = !rightDoor;
 }
 log((side==="L"?"좌측":"우측") + " 출입문 " + ((side==="L"?leftDoor:rightDoor) ? "열림" : "닫힘")); render();
}

function initTrains(){
 trains = [];
 var baseEl = $("baseTrain");
 if(baseEl) baseEl.innerHTML = "";
 var baseStartSec = activeRoute.startHour * 3600 + activeRoute.startMinute * 60;
 for(var n=1; n<=109; n+=2){
  var id = "KTX" + (n < 10 ? "00" : n < 100 ? "0" : "") + n;
  trains.push({id: id, km: -1, speed: 0, active: false, departure: baseStartSec + ((n-1)/2)*1200});
  if(baseEl){
   var opt = document.createElement("option"); opt.value = id; opt.textContent = id;
   baseEl.appendChild(opt);
  }
 }
 if(baseEl) baseEl.value = "KTX001";
}

function getTrainState(t, nowSec){
 var elapsed = (nowSec - t.departure + DAY) % DAY;
 if(elapsed < 0 || elapsed > 25000) return {active:false, km:-1, speed:0};
 
 var currentT = 0;
 for(var i=0; i<stations.length-1; i++){
  var startKm = stations[i].km;
  var endKm = stations[i+1].km;
  var dist = endKm - startKm;
  
  var sName = stations[i].name;
  var isLongStop = (sName==="대전" || sName==="동대구" || sName==="익산" || sName==="광주송정" || sName==="전주" || sName==="순천" || sName==="밀양" || sName==="마산");
  var stopTime = (i===0) ? 0 : (isLongStop ? 300 : 180);
  
  var a = 1.0; 
  var vPeak = Math.min(300, Math.sqrt(dist * a * 3600));
  
  var accelTime = vPeak / a;
  var accelDist = 0.5 * a * (accelTime * accelTime) / 3600;
  var decelTime = vPeak / a;
  var decelDist = 0.5 * a * (decelTime * decelTime) / 3600;
  
  var cruiseDist = Math.max(0, dist - accelDist - decelDist);
  var cruiseTime = cruiseDist / (vPeak / 3600);
  
  var sectionTime = accelTime + cruiseTime + decelTime + stopTime;
  
  if(elapsed >= currentT && elapsed < currentT + sectionTime){
   var relT = elapsed - currentT;
   var curSpd = 0; var currentKm = startKm;
   
   if(relT < accelTime){
    curSpd = relT * a;
    currentKm = startKm + 0.5 * a * (relT * relT) / 3600;
   }else if(relT < accelTime + cruiseTime){
    curSpd = vPeak;
    currentKm = startKm + accelDist + (relT - accelTime) * (vPeak / 3600);
   }else if(relT < accelTime + cruiseTime + decelTime){
    var dt = relT - (accelTime + cruiseTime);
    curSpd = Math.max(0, vPeak - dt * a);
    currentKm = endKm - decelDist + curSpd * (dt / 3600) + 0.5 * a * (dt * dt) / 3600;
   }else{
    curSpd = 0; currentKm = endKm;
   }
   return {active:true, km:currentKm, speed:curSpd};
  }
  currentT += sectionTime;
 }
 if(elapsed >= currentT) return {active:true, km:LEN, speed:0};
 return {active:false, km:-1, speed:0};
}

function updateOtherTrains(){
 var now = deviceSeconds();
 for(var i=0; i<trains.length; i++){
  var st = getTrainState(trains[i], now);
  trains[i].active = st.active; trains[i].km = st.km; trains[i].speed = st.speed;
 }
}

function getTrain(id){
 for(var i=0; i<trains.length; i++){ if(trains[i].id === id) return trains[i]; }
 return null;
}
function getAheadAhead(){
 var baseEl = $("baseTrain");
 var base = getTrain(baseEl ? baseEl.value : "KTX001");
 if(!base || !base.active) return {base:base, front:null, gap:null};
 var ahead = [];
 for(var i=0; i<trains.length; i++){
  if(trains[i].active && trains[i].id !== base.id && trains[i].km > base.km){
   ahead.push(trains[i]);
  }
 }
 ahead.sort(function(a,b){ return a.km - b.km; });
 var front = ahead[1] || ahead[0] || null;
 return {base:base, front:front, gap:front ? (front.km - distance) : null};
}

function calculateTargetSpeed(){
 var limit = 330;
 if(!overtakeMode){
  $("autoExplanation").textContent = "추월 모드 OFF · 수동 운전";
  $("autoLimit").textContent = limit + " km/h"; return limit;
 }
 var info = getAheadAhead();
 if(!info.front){
  $("autoExplanation").textContent = "앞앞차 미검출 · 선로 제한속도 적용";
  $("autoLimit").textContent = limit + " km/h"; return limit;
 }
 var g = info.gap; var allowed = limit;
 if(g <= 0.2) allowed = 0;
 else if(g < targetGap * 0.5) allowed = Math.min(limit, 60);
 else if(g < targetGap * 0.75) allowed = Math.min(limit, 120);
 else if(g < targetGap) allowed = Math.min(limit, 180);
 else if(g < targetGap + 1) allowed = Math.min(limit, 260);
 $("autoExplanation").textContent = info.front.id + " 기준 · 간격 " + g.toFixed(2) + " km";
 $("autoLimit").textContent = Math.round(allowed) + " km/h";
 return allowed;
}

function updateTimetable(){
 var body = $("timetable");
 if(!body) return;
 body.innerHTML = "";
 for(var i=0; i<stations.length; i++){
  var s = stations[i];
  var state, cls;
  if(arrived || distance > s.km + 0.15){ state="운행 완료"; cls="completed"; }
  else if(Math.abs(distance - s.km) <= 0.15){
   if(i === 0 && distance === 0 && speed === 0){ state="운행 전"; cls="pending"; }
   else { state="운행 중"; cls="running"; }
  }
  else if(distance > s.km){ state="운행 완료"; cls="completed"; }
  else { state="운행 전"; cls="pending"; }
  
  var tr = document.createElement("tr"); tr.className = cls;
  var vals = [s.name, formatSec(s.arr), formatSec(s.dep), s.km.toFixed(1)+" km", state];
  for(var j=0; j<vals.length; j++){
   var td = document.createElement("td"); td.textContent = vals[j]; tr.appendChild(td);
  }
  body.appendChild(tr);
 }
}

function updateOtherTable(){
 var body = $("otherTrains");
 if(!body) return;
 body.innerHTML = "";
 var now = deviceSeconds();
 for(var i=0; i<trains.length; i++){
  var t = trains[i];
  var st = getTrainState(t, now);
  var actualStatus, cls;
  if(st.km >= LEN - 0.1){ actualStatus="운행 완료"; cls="completed"; }
  else if(st.active){ actualStatus="운행 중"; cls="running"; }
  else if(now < t.departure){ actualStatus="운행 전"; cls="pending"; }
  else { actualStatus="운행 완료"; cls="completed"; }

  var row = document.createElement("tr"); row.className = cls;
  var diff = (st.km - distance).toFixed(1);
  var vals = [
   t.id, actualStatus,
   st.active ? st.km.toFixed(1) + " km" : "-",
   st.active ? Math.round(st.speed) + " km/h" : "-",
   st.active ? ((st.km - distance >= 0 ? "+" : "") + diff + " km") : "-"
  ];
  for(var j=0; j<vals.length; j++){
   var td = document.createElement("td"); td.textContent = vals[j]; row.appendChild(td);
  }
  body.appendChild(row);
 }
}

function updateTrack(){
 var box = $("trackMarks");
 if(!box) return;
 box.innerHTML = "";
 for(var i=0; i<activeRoute.majorMarks.length; i++){
  var p = activeRoute.majorMarks[i];
  var l = document.createElement("div"); l.className = "tracklabel";
  l.style.left = (p.k/LEN*100) + "%"; l.textContent = p.n; box.appendChild(l);
 }
 var u = document.createElement("div"); u.className = "mark user";
 u.style.left = Math.max(0, Math.min(100, distance/LEN*100)) + "%"; u.title = "ERR 001"; box.appendChild(u);
 for(var i=0; i<trains.length; i++){
  var t = trains[i];
  if(t.km >= 0 && t.km <= LEN){
   var m = document.createElement("div"); m.className = "mark";
   m.style.left = (t.km/LEN*100) + "%"; m.title = t.id; box.appendChild(m);
  }
 }
 var info = getAheadAhead();
 if(overtakeMode && info.front){
  var m = document.createElement("div"); m.className = "mark target";
  m.style.left = (info.front.km/LEN*100) + "%"; m.title = "앞앞차"; box.appendChild(m);
 }
}

function render(){
 $("speed").textContent = Math.round(speed);
 $("speedbar").style.width = Math.min(100, speed/330*100) + "%";
 $("distance").textContent = distance.toFixed(1) + " km";
 $("station").textContent = currentStationName();
 var ni = nextStationIndex();
 $("next").textContent = ni < 0 ? "종착역" : stations[ni].name;
 $("notch").textContent = notchLabel;
 $("limit").textContent = "330 km/h";
 $("targetSpeed").textContent = Math.round(targetSpeed) + " km/h";
 $("vcb").textContent = vcb ? "ON" : "OFF";
 $("pant").textContent = pantograph ? "상승" : "하강";
 $("status").textContent = arrived ? "운행 완료" : emergency ? "비상제동" : speed > 0.1 ? "주행" : "정차";
 $("turnout").textContent = turnout;
 $("leftStatus").textContent = (leftDoor ? "열림" : "닫힘") + " · " + (allowL ? "허가" : "허가 없음");
 $("rightStatus").textContent = (rightDoor ? "열림" : "닫힘") + " · " + (allowR ? "허가" : "허가 없음");
 
 var otBtn = $("overtake");
 otBtn.textContent = "추월 모드 " + (overtakeMode ? "ON" : "OFF");
 if(overtakeMode) otBtn.className = "warn active"; else otBtn.className = "warn";
 
 $("gapSetting").textContent = targetGap.toFixed(1) + " km";
 $("emergencyStatus").textContent = emergency ? "작동" : "해제";
 
 var over = speed > 331;
 $("overspeed").textContent = over ? "초과" : "정상";
 $("overspeed").className = over ? "bad" : "good";
 
 $("vigilance").textContent = warningStart !== null ? "경고" : "정상";
 $("vigilance").className = warningStart !== null ? "bad" : "good";
 
 var info = getAheadAhead();
 $("frontFront").textContent = info.front ? info.front.id : "미검출";
 $("gap").textContent = info.gap === null ? "- km" : info.gap.toFixed(2) + " km";
 $("gapStatus").textContent = !overtakeMode ? "대기" : !info.front ? "기준 열차 대기" : info.gap <= targetGap ? "간격 조절" : "간격 확보";
 syncClock();
}

function passStations(){
 while(stationIndex < stations.length && distance >= stations[stationIndex].km){
  if(stationIndex === 0){ stationIndex++; continue; }
  var s = stations[stationIndex];
  if(stationIndex === stations.length - 1){
   if(distance >= LEN){ distance = LEN; speed = 0; power = 0; notchLabel = "N"; arrived = true; log(activeRoute.endName + " 도착"); }
   break;
  }
  if(overtakeMode){ stationIndex++; continue; }
  if(distance > s.km + 0.2){ stationIndex++; continue; }
  break;
 }
}

function tick(){
 var now = Date.now();
 var dt = Math.min((now - lastFrame)/1000, 0.1);
 lastFrame = now;
 
 syncClock();
 updateOtherTrains();
 
 var limit = 330;
 targetSpeed = calculateTargetSpeed();
 var acceleration = 0;
 
 if(emergency) acceleration = -5;
 else if(power > 0){
  if(vcb && pantograph && direction !== 0) acceleration = power * 0.36; 
  else { power = 0; notchLabel = "N"; }
 } else if(power < 0) acceleration = power * 0.36;

 if(overtakeMode && !emergency){
  var info = getAheadAhead();
  if(info.front && info.gap !== null){
   var g = info.gap;
   if(g <= 0.2) acceleration = Math.min(acceleration, -1.8);
   else if(g < targetGap * 0.5) acceleration = Math.min(acceleration, -1.4);
   else if(g < targetGap * 0.75) acceleration = Math.min(acceleration, -0.9);
   else if(g < targetGap) acceleration = Math.min(acceleration, -0.36);
  }
  if(speed > targetSpeed + 1) acceleration = Math.min(acceleration, -1.8);
 }
 
 speed = Math.max(0, Math.min(330, speed + acceleration * dt));
 if(speed > limit){ speed = Math.max(limit, speed - 1.8 * dt); if(speed > limit + 5 && !emergency) applyEmergency(); }
 if(speed > 0.05 && direction !== 0 && !arrived){
  distance += direction * speed / 3600 * dt;
  distance = Math.max(0, Math.min(LEN, distance));
 }
 if(distance >= LEN && direction === 1 && !arrived){ distance = LEN; speed = 0; power = 0; notchLabel = "N"; arrived = true; log(activeRoute.endName + " 도착"); }
 if(distance <= 0 && direction === -1){ distance = 0; speed = 0; }

 var since = now - vigilanceLast;
 if(since > 55000 && warningStart === null){
  warningStart = now;
  startWarningSound();
  log("경계장치 경고");
 }
 if(warningStart !== null && now - warningStart > 15000 && !emergency){
  applyEmergency();
  log("경계장치 응답 없음 · 비상제동");
 }

 passStations();
 render();
 updateTimetable();
 updateOtherTable();
 updateTrack();
}

function pedalPress(){
 initAudio();
 vigilanceLast = Date.now();
 warningStart = null;
 stopWarningSound();
 $("pedalTime").textContent = "최근 입력: " + deviceTimeText();
}
function toggleOvertake(){ initAudio(); overtakeMode = !overtakeMode; log("추월 모드 " + (overtakeMode ? "ON · 앞앞차 기준" : "OFF")); render(); updateTrack(); }

function notchUp(){
 initAudio();
 if(power < 0){ setNotch(power === -1 ? "N" : "B" + (Math.abs(power) - 1)); }
 else if(power === 0){ setNotch("P1"); }
 else { setNotch("P" + Math.min(5, power + 1)); }
}

function notchDown(){
 initAudio();
 if(power > 0){ setNotch(power === 1 ? "N" : "P" + (power - 1)); }
 else if(power === 0){ setNotch("B1"); }
 else { setNotch("B" + Math.min(5, Math.abs(power) + 1)); }
}

function bindEvent(id, ev, fn){
 var el = $(id);
 if(el) el.addEventListener(ev, fn, false);
}

window.onload = function(){
 bindEvent("routeSelect", "change", function(e){ initAudio(); changeRoute(e.target.value); });
 bindEvent("saveGame", "click", saveGameData);
 bindEvent("loadGame", "click", loadGameData);
 bindEvent("forward", "click", function(){ setDirection(1); });
 bindEvent("reverse", "click", function(){ setDirection(-1); });
 bindEvent("vcbButton", "click", toggleVCB);
 bindEvent("pantButton", "click", togglePantograph);
 bindEvent("coast", "click", function(){ setNotch("N"); });
 bindEvent("eb", "click", applyEmergency);
 bindEvent("release", "click", releaseBrake);
 bindEvent("turnL", "click", function(){ setTurnout("좌측"); });
 bindEvent("turnS", "click", function(){ setTurnout("직진"); });
 bindEvent("turnR", "click", function(){ setTurnout("우측"); });
 bindEvent("permitL", "click", function(){ togglePermission("L"); });
 bindEvent("permitR", "click", function(){ togglePermission("R"); });
 bindEvent("leftDoor", "click", function(){ toggleDoor("L"); });
 bindEvent("rightDoor", "click", function(){ toggleDoor("R"); });
 bindEvent("pedal", "click", pedalPress);
 bindEvent("overtake", "click", toggleOvertake);
 bindEvent("setGap", "click", function(){
  initAudio();
  var v = Number($("gapInput").value);
  if(!isNaN(v) && v >= 0.5 && v <= 20){ targetGap = v; log("목표 간격 " + v.toFixed(1) + " km"); render(); }
  else alert("목표 간격은 0.5~20km로 입력하세요.");
 });
 bindEvent("baseTrain", "change", function(){ render(); updateTrack(); });

 var notchBtns = document.querySelectorAll("[data-notch]");
 for(var i=0; i<notchBtns.length; i++){
  (function(btn){
   btn.addEventListener("click", function(){ setNotch(btn.getAttribute("data-notch")); }, false);
  })(notchBtns[i]);
 }

 document.addEventListener("keydown", function(e){
  initAudio();
  var tag = document.activeElement ? document.activeElement.tagName : "";
  if(tag === "INPUT" || tag === "SELECT" || tag === "TEXTAREA") return;
  if(e.code === "Space" || e.keyCode === 32){
   if(e.preventDefault) e.preventDefault();
   if(!heldKeys["Space"]) pedalPress();
   heldKeys["Space"] = true; return;
  }
  if(heldKeys[e.code || e.keyCode]) return;
  heldKeys[e.code || e.keyCode] = true;
  var k = (e.key || "").toLowerCase();
  if(k === "f") setDirection(1); else if(k === "r") setDirection(-1);
  else if(k === "o") toggleVCB(); else if(k === "p") togglePantograph();
  else if(k === "c") setNotch("N"); else if(k === "t") toggleOvertake();
  else if(k === "w") toggleDoor("L"); else if(k === "e") toggleDoor("R");
  else if(k === "a") togglePermission("L"); else if(k === "d") togglePermission("R");
  else if(k === "4") setTurnout("좌측"); else if(k === "5") setTurnout("직진"); else if(k === "6") setTurnout("우측");
  else if(e.keyCode === 38) notchUp();
  else if(e.keyCode === 40) notchDown();
 }, false);

 document.addEventListener("keyup", function(e){ delete heldKeys[e.code || e.keyCode]; }, false);
 document.addEventListener("touchstart", initAudio, false);

 changeRoute("gyeongbu");
 log("오프라인 전용 시뮬레이터 구동 시작");
 setInterval(tick, 1000/60);
};
</script>
</body>
</html>
