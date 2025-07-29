<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Hành Trình Lịch Sử</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      margin: 0;
      background: url('https://i.imgur.com/I9Xn3yo.jpg');
      background-size: cover;
      background-attachment: fixed;
      color: #333;
    }
    .page {
      display: none;
      padding: 2rem;
      background-color: rgba(255, 255, 255, 0.95);
      border-radius: 15px;
      margin: 20px auto;
      width: 90%;
      max-width: 800px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    }
    .active {
      display: block;
    }
    .btn {
      padding: 10px 20px;
      background: #8B4513;
      color: white;
      border: none;
      border-radius: 12px;
      cursor: pointer;
      margin: 10px 5px;
      font-weight: bold;
    }
    .btn:hover {
      background: #5c3311;
    }
    .btn-sword {
      border-radius: 20px;
      background: linear-gradient(to right, #b5651d, #8b0000);
    }
    .minigame-option {
      display: block;
      margin: 10px 0;
      padding: 10px;
      background: #ffe4b5;
      border-left: 5px solid #ff8c00;
      border-radius: 10px;
      cursor: pointer;
    }
    .minigame-option:hover {
      background: #ffdead;
    }
    .drag-container, .image-quiz, .crossword-container {
      margin-top: 20px;
    }
    .draggable {
      padding: 5px 10px;
      margin: 5px;
      background: #d2b48c;
      display: inline-block;
      cursor: grab;
      border-radius: 5px;
    }
    .droptarget {
      border: 2px dashed #8b0000;
      padding: 10px;
      margin: 10px 0;
      min-height: 40px;
    }
  </style>
</head>
<body>

<div id="intro" class="page active">
  <h2>📜 Giới thiệu chặng: Cải cách thời Lê sơ</h2>
  <p>Trong lịch sử Việt Nam, thời Lê sơ dưới triều vua Lê Thánh Tông được xem là giai đoạn có nhiều cải cách sâu rộng, đặc biệt trong hành chính, giáo dục và pháp luật.</p>
  <p>Hãy cùng trả lời một số câu hỏi nhỏ trước khi bước vào các minigame thú vị nhé!</p>
  <button class="btn" onclick="goToPage('quiz')">Bắt đầu câu hỏi</button>
</div>

<div id="quiz" class="page">
  <h2>🧠 Câu hỏi ôn tập</h2>
  <p>1. Ai là người thực hiện nhiều cải cách vào thời Lê sơ?</p>
  <input type="text" id="q1" placeholder="Nhập đáp án..." /><br><br>

  <p>2. Một trong những cải cách nổi bật của vua Lê Thánh Tông là gì?</p>
  <input type="text" id="q2" placeholder="Nhập đáp án..." /><br><br>

  <button class="btn" onclick="checkQuizAnswers()">Kiểm tra đáp án</button>
  <p id="quizResult"></p>
</div>

<div id="minigame" class="page">
  <h2>🎮 Minigame - Đảo 1</h2>
  <p>Chọn minigame bạn muốn chơi để ôn tập kiến thức:</p>
  <div class="minigame-option" onclick="showDragDrop()">🧩 Kéo thả</div>
  <div class="minigame-option" onclick="showImageQuiz()">🖼️ Đuổi hình bắt chữ</div>
  <div class="minigame-option" onclick="showCrossword()">🧠 Ô chữ</div>

  <div class="drag-container" id="dragGame" style="display:none;">
    <h3>Ghép đúng các thời kỳ với cải cách:</h3>
    <div>
      <div class="draggable" draggable="true" ondragstart="drag(event)" id="drag1">Thời Lê Thánh Tông</div>
      <div class="draggable" draggable="true" ondragstart="drag(event)" id="drag2">Thời Hồ Quý Ly</div>
    </div>
    <div>
      <p>📜 Cải cách hành chính:</p>
      <div class="droptarget" ondrop="drop(event)" ondragover="allowDrop(event)"></div>
    </div>
    <div>
      <p>💰 Cải cách kinh tế:</p>
      <div class="droptarget" ondrop="drop(event)" ondragover="allowDrop(event)"></div>
    </div>
  </div>

  <div class="image-quiz" id="imageQuiz" style="display:none;">
    <h3>Đuổi hình bắt chữ</h3>
    <p><img src="https://i.imgur.com/KNRwJcC.png" alt="hint image" style="width:200px;"/><br>Đây là ai?</p>
    <input type="text" id="guessName" placeholder="Nhập tên..." />
    <button class="btn" onclick="checkImageGuess()">Trả lời</button>
    <p id="resultImage"></p>
  </div>

  <div class="crossword-container" id="crossword" style="display:none;">
    <h3>Ô chữ lịch sử</h3>
    <p>Câu hỏi: Vị vua nổi tiếng với cải cách lớn trong triều Lê sơ?</p>
    <input type="text" id="crosswordAnswer" placeholder="Nhập đáp án..." />
    <button class="btn" onclick="checkCrossword()">Kiểm tra</button>
    <p id="resultCrossword"></p>
  </div>

  <button class="btn" onclick="goToPage('intro')">🔙 Quay lại bản đồ</button>
</div>

<script>
  function goToPage(id) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
  }
  function showDragDrop() {
    hideAllMini();
    document.getElementById('dragGame').style.display = 'block';
  }
  function showImageQuiz() {
    hideAllMini();
    document.getElementById('imageQuiz').style.display = 'block';
  }
  function showCrossword() {
    hideAllMini();
    document.getElementById('crossword').style.display = 'block';
  }
  function hideAllMini() {
    document.getElementById('dragGame').style.display = 'none';
    document.getElementById('imageQuiz').style.display = 'none';
    document.getElementById('crossword').style.display = 'none';
  }
  function allowDrop(ev) {
    ev.preventDefault();
  }
  function drag(ev) {
    ev.dataTransfer.setData("text", ev.target.id);
  }
  function drop(ev) {
    ev.preventDefault();
    var data = ev.dataTransfer.getData("text");
    ev.target.appendChild(document.getElementById(data));
  }
  function checkImageGuess() {
    const answer = document.getElementById("guessName").value.trim().toLowerCase();
    document.getElementById("resultImage").innerText = (answer === "nguyen trai") ? "✅ Chính xác!" : "❌ Sai rồi, thử lại!";
  }
  function checkCrossword() {
    const answer = document.getElementById("crosswordAnswer").value.trim().toLowerCase();
    document.getElementById("resultCrossword").innerText = (answer === "le thanh tong") ? "🎉 Chính xác!" : "❌ Chưa đúng, thử lại nào!";
  }
  function checkQuizAnswers() {
    const a1 = document.getElementById("q1").value.trim().toLowerCase();
    const a2 = document.getElementById("q2").value.trim().toLowerCase();
    if (a1.includes("le thanh tong") && a2.includes("phap luat")) {
      document.getElementById("quizResult").innerHTML = "🎯 Tuyệt vời! Bạn đã nắm kiến thức cơ bản. Tiến đến minigame thôi!<br><button class='btn' onclick=\"goToPage('minigame')\">🎮 Vào minigame</button>";
    } else {
      document.getElementById("quizResult").innerText = "❌ Có vẻ bạn chưa nắm rõ. Hãy xem lại bài học nhé!";
    }
  }
</script>

</body>
</html>
