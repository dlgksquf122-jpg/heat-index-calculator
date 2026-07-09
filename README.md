<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>체감온도 계산기 PRO</title>

<style>
*{margin:0;padding:0;box-sizing:border-box;}

body{
font-family:'맑은 고딕',sans-serif;
background:linear-gradient(135deg,#5ec8ff,#d9f1ff);
padding:20px;
}

.container{
max-width:550px;
margin:auto;
}

.card{
background:#fff;
padding:25px;
border-radius:20px;
box-shadow:0 10px 30px rgba(0,0,0,.2);
}

h1{
text-align:center;
margin-bottom:20px;
color:#333;
}

label{
font-weight:bold;
display:block;
margin-top:15px;
}

input{
width:100%;
padding:12px;
margin-top:5px;
font-size:17px;
border-radius:10px;
border:1px solid #ccc;
}

.result{
margin-top:20px;
padding:20px;
border-radius:15px;
text-align:center;
font-size:18px;
font-weight:bold;
transition:.3s;
}

/* 기상청 표 기준 4단계 색상 완벽 매핑 */
.safe{background:#e2f0d9;color:#385723;}         /* 정상 (기온 낮음) */
.interest{background:#d9e1f2;color:#1f4e78;}     /* 관심 (31도 이상 ~ 33도 미만) */
.caution{background:#fff2cc;color:#7f6000;}      /* 주의 (33도 이상 ~ 35도 미만) */
.danger{background:#fce4d6;color:#c65911;}       /* 경고 (35도 이상 ~ 38도 미만) */
.extreme{background:#ffc7ce;color:#9c0006;}      /* 위험 (38도 이상) */

.tip{
margin-top:15px;
font-size:15px;
line-height:1.6;
}
</style>
</head>

<body>

<div class="container">
    <div class="card">
        <h1>🌡 기상청 체감온도 계산기 PRO</h1>

        <label>기온(℃)</label>
        <input type="number" id="temp" placeholder="예 : 33" step="0.1">

        <label>습도(%)</label>
        <input type="number" id="humidity" placeholder="예 : 70" step="1">

        <label>풍속(m/s)</label>
        <input type="number" id="wind" placeholder="예 : 2" step="0.1">

        <div id="result" class="result">
            기온과 습도를 입력하세요.
        </div>
    </div>
</div>

<script>
document.querySelectorAll("input").forEach(i=>{
    i.addEventListener("input",calc);
});

function calc(){
    let Ta = parseFloat(temp.value);
    let RH = parseFloat(humidity.value);
    let W = parseFloat(wind.value);

    if(isNaN(Ta) || isNaN(RH)) return;
    if(isNaN(W)) W = 1.5; // 풍속 입력 안 될 시 기본값

    let feel = Ta;

    // ===== 1. 여름철 체감온도 공식 (기상청 표준 공식 적용) =====
    if (Ta >= 20) {
        // Stull의 습구온도(Tw) 추정 방정식
        let Tw = Ta * Math.atan(0.151977 * Math.pow(RH + 8.313659, 0.5)) 
                 + Math.atan(Ta + RH) 
                 - Math.atan(RH - 1.67633) 
                 + 0.00391838 * Math.pow(RH, 1.5) * Math.atan(0.023101 * RH) 
                 - 4.686035;

        // 기상청 공식 여름철 체감온도 수식 (2022년 개정본)
        feel = -0.2442 + (0.55399 * Tw) + (0.45535 * Ta) - (0.0022 * Math.pow(Tw, 2)) + (0.00278 * Tw * Ta) + 3.0;
    } 
    // ===== 2. 겨울철 체감온도 공식 (기상청 표준) =====
    else if (Ta <= 10 && W > 1.3) {
        let V = W * 3.6; // m/s를 km/h 단위로 변환 필요
        feel = 13.12 + 0.6215 * Ta - 11.37 * Math.pow(V, 0.16) + 0.3965 * Ta * Math.pow(V, 0.16);
    } 
    // ===== 3. 환절기 및 평시 기온 =====
    else {
        feel = Ta;
    }

    // ===== 4. 불쾌지수(DI) 계산 =====
    let DI = 0.81 * Ta + 0.01 * RH * (0.99 * Ta - 14.3) + 46.3;

    let level = "";
    let advice = "";
    let cls = "";

    // ===== 5. 기상청 제공 폭염특보 발령 기준 색상 매핑 =====
    if (feel < 31) {
        level = "🟢 정상";
        cls = "safe";
        advice = "쾌적하거나 일상적인 더위입니다. 적절한 수분을 섭취하세요.";
    }
    else if (feel < 33) {
        level = "🔵 관심 단계";
        cls = "interest";
        advice = "영유아, 노약자는 야외 활동 시 햇볕을 피하고 휴식을 취하세요.";
    }
    else if (feel < 35) {
        level = "🟡 주의 단계 (폭염주의보 발령 기준)";
        cls = "caution";
        advice = "정오~오후 5시 사이 장시간 실외 활동을 자제하십시오.";
    }
    else if (feel < 38) {
        level = "🟠 경고 단계 (폭염경보 발령 기준)";
        cls = "danger";
        advice = "최고 더운 시간대 실외 작업을 중단하고 나홀로 작업을 피하세요.";
    }
    else {
        level = "🔴 위험 단계 (심각한 폭염)";
        cls = "extreme";
        advice = "야외 활동을 완전히 금지하고 실내 무더위 쉼터로 대피하세요.";
    }

    // 결과 화면 업데이트
    result.className = "result " + cls;
    result.innerHTML = `
        <div style="font-size:40px;">${feel.toFixed(1)}℃</div>
        <div style="margin-top:10px; font-size:20px;">${level}</div>
        <hr style="margin:15px 0; border:0; background:rgba(0,0,0,0.1); height:1px;">
        <table style="width:100%; font-size:15px; text-align:left; line-height:2;">
            <tr><td>• 기상청 체감온도</td><td style="text-align:right;"><b>${feel.toFixed(1)}℃</b></td></tr>
            <tr><td>• 불쾌지수</td><td style="text-align:right;"><b>${DI.toFixed(1)}</b></td></tr>
            <tr><td>• 입력 기온 / 습도</td><td style="text-align:right;"><b>${Ta.toFixed(1)}℃ / ${RH}%</b></td></tr>
        </table>
        <div class="tip">💡 <b>행동요령:</b> ${advice}</div>
    `;
}
</script>

</body>
</html>
