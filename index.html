<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>체감온도 계산기 PRO</title>

<style>
body{
  font-family: Arial;
  background: linear-gradient(135deg,#74ebd5,#ACB6E5);
  margin:0;
  padding:20px;
}

.container{
  max-width:500px;
  margin:auto;
}

.card{
  background:white;
  padding:20px;
  border-radius:15px;
  box-shadow:0 10px 20px rgba(0,0,0,0.15);
}

h2{
  text-align:center;
}

input{
  width:100%;
  padding:12px;
  margin:8px 0;
  border:1px solid #ddd;
  border-radius:10px;
  font-size:16px;
}

.result{
  margin-top:15px;
  padding:15px;
  border-radius:10px;
  font-weight:bold;
  text-align:center;
}

.small{
  font-size:12px;
  color:#666;
  margin-top:5px;
}

.badge{
  display:inline-block;
  padding:5px 10px;
  border-radius:20px;
  font-size:12px;
  margin-top:10px;
}

.safe{background:#d4f8d4;color:#1a7f1a;}
.caution{background:#fff3cd;color:#8a6d3b;}
.danger{background:#ffd6d6;color:#b30000;}
.verydanger{background:#ff4d4d;color:white;}
</style>
</head>

<body>

<div class="container">
<div class="card">

<h2>🌡️ 체감온도 계산기 PRO</h2>

<label>🌡️ 온도 (℃)</label>
<input type="number" id="temp" placeholder="예: 30">

<label>💧 습도 (%)</label>
<input type="number" id="humidity" placeholder="예: 70">

<div class="small">입력하면 자동으로 계산됩니다</div>

<div id="result" class="result">값을 입력해주세요</div>

</div>
</div>

<script>

document.getElementById("temp").addEventListener("input", calc);
document.getElementById("humidity").addEventListener("input", calc);

function calc(){

let T = parseFloat(document.getElementById("temp").value);
let R = parseFloat(document.getElementById("humidity").value);

if(isNaN(T) || isNaN(R)){
  return;
}

// 화씨 변환
let T_F = (T * 9/5) + 32;

// Heat Index 공식
let HI_F =
-42.379 + 2.04901523*T_F + 10.14333127*R
-0.22475541*T_F*R
-0.00683783*T_F*T_F
-0.05481717*R*R
+0.00122874*T_F*T_F*R
+0.00085282*T_F*R*R
-0.00000199*T_F*T_F*R*R;

let HI_C = (HI_F - 32) * 5/9;

// 불쾌지수 (간단 버전)
let DI = (0.81*T) + (0.01*R*(0.99*T - 14.3)) + 46.3;

// 위험도 판단
let level = "";
let cls = "";

if(HI_C < 27){
  level = "🟢 쾌적한 날씨";
  cls = "safe";
}
else if(HI_C < 32){
  level = "🟡 약간 더움";
  cls = "caution";
}
else if(HI_C < 41){
  level = "🟠 매우 더움 (주의)";
  cls = "danger";
}
else{
  level = "🔴 위험 수준 (폭염)";
  cls = "verydanger";
}

// 출력
document.getElementById("result").className = "result " + cls;

document.getElementById("result").innerHTML =
`
🔥 체감온도: ${HI_C.toFixed(1)}℃ <br>
😓 불쾌지수: ${DI.toFixed(1)} <br>
${level}
`;

}

</script>

</body>
</html>
