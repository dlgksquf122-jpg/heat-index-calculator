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

/* 기상청 표 기준 색상 컴포넌트 교정 */
.safe{background:#e2f0d9;color:#385723;}
.interest{background:#d9e1f2;color:#1f4e78;} /* 관심 (파랑 계열) */
.caution{background:#fff2cc;color:#7f6000;}  /* 주의 (노랑 계열) */
.danger{background:#fce4d6;color:#c65911;}   /* 경고 (주황 계열) */
.extreme{background:#ffc7ce;color:#9c0006;}  /* 위험 (빨강 계열) */

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
    let T = parseFloat(temp.value);
    let R = parseFloat(humidity.value);
    let W = parseFloat(wind.value);

    if(isNaN(T) || isNaN(R)) return;
    if(isNaN(W)) W = 1.5; // 풍속 기본값 설정

    let feel = T;

    // ===== 1. 여름철 체감온도 공식 (기상청 가이드를 따르는 수증기압 기반 계산) =====
    if (T >= 28) {
        // 수증기압(e) 계산
        let e = (R / 100) * 6.105 * Math.exp((17.27 * T) / (T + 237.7));
        // 여름철 체감온도 근사식 적용
        feel = T + 0.33 * e - 0.70 * W - 4.0;
        
        // 기상청 표 데이터와의 오차 미세 보정 (표의 중심부 편차 평탄화)
        if (R > 50) {
            feel += (R - 50) * 0.015;
        }
    } 
    // ===== 2. 겨울철 체감온도 공식 (기상청 표준) =====
    else if (T <= 10 && W > 1.3) {
        feel = 13.12 + 0.6215 * T - 11.37 * Math.pow(W, 0.16) + 0.3965 * T * Math.pow(W, 0.16);
    } 
    // ===== 3. 환절기 평시 기온 =====
    else {
        feel = T;
    }

    // ===== 4. 불쾌지수(DI) 계산 =====
    let DI = 0.81 * T + 0.01 * R * (0.99 * T - 14.3) + 46.3;

    let level = "";
    let advice = "";
    let cls = "";

    // ===== 5. 기상청 제공 폭염특보 발령 기준 매핑 =====
    if (feel < 31) {
        level = "🟢 정상/낮음";
        cls = "safe";
        advice = "쾌적하거나 일상적인 더위입니다. 적절한 수분을 섭취하세요.";
    }
    else if (feel < 33) {
        level = "🔵 관심 단계";
        cls = "interest";
        advice = "영유아, 노약자는 야외 활동 시 햇볕을 피하고 휴식을 취하세요.";
    }
    else if (feel < 35) {
        level = "🟡 주의 단계 (폭염주의보 수준)";
        cls = "caution";
        advice = "정오~오후 5시 사이 장시간 실외 활동을 자제하십시오.";
    }
    else if (feel < 38) {
        level = "🟠 경고 단계 (폭염경보 수준)";
        cls = "danger";
        advice = "최고 더운 시간대 실외 작업을 중단하고 나홀로 작업을 피하세요.";
    }
    else {
        level = "🔴 위험 단계 (심각한 폭염)";
        cls = "extreme";
        advice = "야외 활동을 금지하고, 현기증이나 두통 시 즉시 무더위 쉼터로 대피하세요.";
    }

    // 결과 렌더링
    result.className = "result " + cls;
    result.innerHTML = `
        <div style="font-size:40px;">${feel.toFixed(1)}℃</div>
        <div style="margin-top:10px; font-size:20px;">${level}</div>
        <hr style="margin:15px 0; border:0; background:rgba(0,0,0,0.1); height:1px;">
        <table style="width:100%; font-size:15px; text-align:left; line-height:2;">
            <tr><td>• 실제 기온</td><td style="text-align:right;"><b>${T.toFixed(1)}℃</b></td></tr>
            <tr><td>• 상대 습도</td><td style="text-align:right;"><b>${R}%</b></td></tr>
            <tr><td>• 현재 풍속</td><td style="text-align:right;"><b>${W}m/s</b></td></tr>
            <tr><td>• 불쾌지수</td><td style="text-align:right;"><b>${DI.toFixed(1)}</b></td></tr>
        </table>
        <div class="tip">💡 <b>행동요령:</b> ${advice}</div>
    `;
}
</script>

</body>
</html>
