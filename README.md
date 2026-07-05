<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>체감온도 계산기</title>
</head>
<body style="font-family:Arial;max-width:400px;margin:50px auto;">

  <h2>🌡️ 체감온도 계산기</h2>

  <label>기온 (℃)</label><br>
  <input type="number" id="temp" style="width:100%;padding:5px;"><br><br>

  <label>습도 (%)</label><br>
  <input type="number" id="humidity" style="width:100%;padding:5px;"><br><br>

  <button onclick="calc()">계산하기</button>

  <h3 id="result"></h3>

<script>
function calc() {
  let T = parseFloat(document.getElementById("temp").value);
  let R = parseFloat(document.getElementById("humidity").value);

  if (isNaN(T) || isNaN(R)) {
    document.getElementById("result").innerText = "값을 입력하세요.";
    return;
  }

  let T_F = (T * 9/5) + 32;

  let HI_F = -42.379 + 2.04901523*T_F + 10.14333127*R
            - 0.22475541*T_F*R - 0.00683783*T_F*T_F
            - 0.05481717*R*R + 0.00122874*T_F*T_F*R
            + 0.00085282*T_F*R*R - 0.00000199*T_F*T_F*R*R;

  let HI_C = (HI_F - 32) * 5/9;

  document.getElementById("result").innerText =
    "체감온도: " + HI_C.toFixed(1) + " ℃";
}
</script>

</body>
</html>
