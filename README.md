<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>ให้คะแนนความน่ารักแฟน</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      text-align: center;
      margin-top: 100px;
      background-color: #fff0f5;
    }

    button {
      padding: 10px 20px;
      font-size: 18px;
      background-color: #ff69b4;
      color: white;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      margin: 10px;
    }

    #sliderSection {
      margin-top: 30px;
      display: none;
    }

    input[type=range] {
      width: 60%;
    }

    #score {
      font-size: 24px;
      color: #ff1493;
      margin-top: 10px;
    }

    #resultCard {
      display: none;
      background: white;
      width: 300px;
      margin: 30px auto;
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
    }

    #resultText {
      font-size: 22px;
      color: #ff69b4;
    }
  </style>
</head>
<body>

  <h1>💗 แฟนน่ารักขนาดไหน? 💗</h1>
  
  <button onclick="showSlider()">ให้คะแนนความน่ารักแฟน</button>

  <div id="sliderSection">
    <input type="range" min="0" max="100" value="50" id="slider" oninput="updateScore(this.value)">
    <p id="score">คะแนน: 50/100</p>
    <button onclick="showResult()">📋 สรุปคะแนน</button>
  </div>

  <!-- การ์ดสรุปคะแนน -->
  <div id="resultCard">
    <p id="resultText"></p>
    <button onclick="saveCard()">💾 บันทึกภาพ</button>
  </div>

  <!-- JavaScript + html2canvas -->
  <script src="https://html2canvas.hertzen.com/dist/html2canvas.min.js"></script>
  <script>
    function showSlider() {
      document.getElementById('sliderSection').style.display = 'block';
    }

    function updateScore(value) {
      document.getElementById('score').innerText = `คะแนน: ${value}/100`;
    }

    function showResult() {
      const score = document.getElementById('slider').value;
      const resultText = `คุณให้คะแนนความน่ารักแฟน : ${score}/100`;
      document.getElementById('resultText').innerText = resultText;
      document.getElementById('resultCard').style.display = 'block';
    }

    function saveCard() {
      const card = document.getElementById("resultCard");
      const saveButton = card.querySelector("button");

      // ซ่อนปุ่มก่อนถ่ายภาพ
      saveButton.style.display = "none";

      html2canvas(card).then(canvas => {
        // สร้างลิงก์ดาวน์โหลด
        let link = document.createElement('a');
        link.download = 'cute_rating.png';
        link.href = canvas.toDataURL("image/png");
        link.click();

        // แสดงปุ่มกลับมา
        saveButton.style.display = "inline-block";
      });
    }
  </script>

</body>
</html>
