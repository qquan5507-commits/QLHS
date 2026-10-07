<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="mobile-web-app-capable" content="yes">
<title>🏫 Quản Lý Lớp Tiểu Học</title>
<style>
* { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
html { touch-action: manipulation; }
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Arial, sans-serif;
  background: linear-gradient(180deg, #FFFEF7 0%, #FFF8E1 100%);
  min-height: 100vh;
  padding: 12px;
  padding-bottom: 120px;
  color: #37474F;
}
.container { max-width: 100%; margin: 0 auto; }

/* === TIÊU ĐỀ === */
.header {
  text-align: center;
  padding: 15px 10px;
  margin-bottom: 15px;
  position: relative;
}
.header h1 {
  font-size: 20px;
  font-weight: 800;
  color: #4A90E2;
}
.sound-toggle {
  position: absolute;
  right: 5px;
  top: 50%;
  transform: translateY(-50%);
  background: white;
  border: none;
  font-size: 22px;
  padding: 10px 12px;
  border-radius: 50%;
  cursor: pointer;
  box-shadow: 0 3px 10px rgba(0,0,0,0.1);
}

/* === TOP 3 === */
.awards-title {
  text-align: center;
  font-size: 20px;
  font-weight: bold;
  color: #FF9F1C;
  margin-bottom: 15px;
}
.section-label {
  text-align: center;
  font-size: 15px;
  color: #4A90E2;
  margin: 15px 0 8px;
  font-weight: 600;
}
.top-row {
  display: flex;
  justify-content: center;
  align-items: flex-end;
  gap: 8px;
  margin-bottom: 20px;
}
.card {
  background: white;
  border-radius: 16px;
  padding: 12px 8px;
  text-align: center;
  box-shadow: 0 4px 12px rgba(0,0,0,0.08);
  width: 30%;
  opacity: 0;
  transform: translateY(20px);
  animation: slideIn 0.5s ease forwards;
}
@keyframes slideIn { to { opacity:1; transform: translateY(0); } }
.card-2 { animation-delay: 0.1s; }
.card-3 { animation-delay: 0.2s; }
.card-1 {
  background: linear-gradient(180deg, #FDD835, #FBC02D);
  transform: scale(1.1);
  animation-delay: 0.05s, glow 2s infinite 0.4s;
}
@keyframes glow {
  0%,100% { box-shadow: 0 6px 18px rgba(253,216,53,0.4); }
  50% { box-shadow: 0 6px 25px rgba(253,216,53,0.6); }
}
.card-rank { font-size: 22px; }
.card-name { font-weight: bold; margin: 4px 0; font-size: 12px; line-height: 1.3; }
.card-score {
  font-size: 13px;
  font-weight: bold;
  background: rgba(255,255,255,0.5);
  border-radius: 12px;
  padding: 2px 8px;
  display: inline-block;
}
.card-empty {
  background: #F5F5F5;
  border: 2px dashed #E0E0E0;
  color: #999;
  padding: 15px 5px;
}

/* === NÚT CHỨC NĂNG === */
.nav-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 12px;
  margin-top: 5px;
}
.nav-btn {
  border: none;
  border-radius: 16px;
  padding: 16px 10px;
  font-size: 15px;
  font-weight: bold;
  color: white;
  cursor: pointer;
  min-height: 60px;
  box-shadow: 0 4px 10px rgba(0,0,0,0.1);
}
.nav-btn:active { transform: scale(0.97); }
.btn-student { background: linear-gradient(135deg, #4A90E2, #357ABD); }
.btn-team    { background: linear-gradient(135deg, #F06292, #EC407A); }
.btn-random  { background: linear-gradient(135deg, #9C27B0, #7B1FA2); }
.btn-timer   { background: linear-gradient(135deg, #26A69A, #00897B); }
.btn-history { background: linear-gradient(135deg, #FF9F1C, #FB8C00); grid-column: span 2; }

/* === KHỐI NỘI DUNG === */
.panel {
  background: white;
  border-radius: 16px;
  padding: 18px;
  margin-top: 15px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.06);
  display: none;
  animation: fadeIn 0.3s ease;
}
@keyframes fadeIn { from { opacity:0; transform: translateY(10px); } to { opacity:1; } }
.panel.show { display: block; }
.panel h3 { color: #4A90E2; margin-bottom: 15px; text-align: center; font-size: 18px; }
h4 { color: #546E7A; margin: 18px 0 8px; font-size: 14px; }

/* === FORM === */
input, select {
  width: 100%;
  padding: 14px 12px;
  margin: 5px 0;
  border: 2px solid #ECEFF1;
  border-radius: 12px;
  font-size: 16px;
  background: white;
  -webkit-appearance: none;
  appearance: none;
}
input:focus, select:focus {
  outline: none;
  border-color: #4A90E2;
}
.btn-row { display: flex; gap: 8px; margin-top: 5px; }
.btn {
  flex: 1;
  padding: 14px 10px;
  border: none;
  border-radius: 12px;
  font-size: 15px;
  font-weight: bold;
  cursor: pointer;
  min-height: 50px;
}
.btn-add { background: #2ECC71; color: white; }
.btn-sub { background: #EF5350; color: white; }
.btn-back { background: #78909C; color: white; margin-top: 15px; width: 100%; }
.btn-delete { background: #EF5350; color: white; }

/* === DANH SÁCH === */
.list-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 8px;
  border-bottom: 1px solid #F5F5F5;
}
.score-val { font-weight: bold; font-size: 18px; color: #4A90E2; }
.del-btn {
  background: rgba(239,83,80,0.1);
  color: #EF5350;
  border: none;
  border-radius: 8px;
  padding: 8px 10px;
  font-size: 14px;
  margin-left: 8px;
}

/* === GỌI NGẪU NHIÊN === */
.random-display {
  font-size: 28px;
  font-weight: bold;
  text-align: center;
  padding: 30px 15px;
  color: #7B1FA2;
  background: linear-gradient(135deg, #F3E5F5, #EDE7F6);
  border-radius: 16px;
  margin-bottom: 12px;
  min-height: 110px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.random-display.rolling {
  animation: shake 0.08s infinite;
}
@keyframes shake {
  0%,100% { transform: translateX(0); }
  25% { transform: translateX(-4px); }
  75% { transform: translateX(4px); }
}
.random-btn {
  width: 100%;
  padding: 15px;
  border: none;
  border-radius: 12px;
  background: linear-gradient(135deg, #9C27B0, #7B1FA2);
  color: white;
  font-size: 17px;
  font-weight: bold;
  min-height: 56px;
}

/* === ĐẾM NGƯỢC === */
.timer-display {
  font-size: 44px;
  font-weight: bold;
  text-align: center;
  color: #2ECC71;
  background: linear-gradient(135deg, #E0F2F1, #B2DFDB);
  border-radius: 16px;
  padding: 20px;
  margin-bottom: 12px;
  font-variant-numeric: tabular-nums;
}
.timer-display.warning { color: #FF9F1C; }
.timer-display.danger {
  color: #EF5350;
  animation: pulseDanger 0.5s infinite;
}
@keyframes pulseDanger {
  0%,100% { opacity: 1; }
  50% { opacity: 0.6; }
}
.timer-quick {
  display: grid;
  grid-template-columns: repeat(4,1fr);
  gap: 8px;
  margin-bottom: 10px;
}
.timer-quick button {
  padding: 12px 8px;
  border: none;
  border-radius: 10px;
  background: #E0F2F1;
  color: #00897B;
  font-weight: bold;
  font-size: 15px;
}
.timer-row { display: flex; gap: 8px; margin-bottom: 10px; }
.timer-row input { flex: 1; text-align: center; }
.timer-buttons { display: flex; gap: 10px; }
.timer-btn {
  flex: 1;
  padding: 14px;
  border: none;
  border-radius: 12px;
  font-size: 16px;
  font-weight: bold;
  min-height: 54px;
}
.timer-start { background: #2ECC71; color: white; }
.timer-pause { background: #FF9F1C; color: white; }
.timer-reset { background: #EF5350; color: white; }

/* === LỊCH SỬ === */
.history-item {
  padding: 10px;
  border-bottom: 1px solid #F5F5F5;
  font-size: 14px;
  line-height: 1.5;
}
.history-item.plus { border-left: 4px solid #2ECC71; padding-left: 10px; }
.history-item.minus { border-left: 4px solid #EF5350; padding-left: 10px; }
.history-time { color: #90A4AE; font-size: 12px; margin-top: 2px; display: block; }

/* === THÔNG BÁO === */
.toast {
  position: fixed;
  top: 15px;
  left: 50%;
  transform: translateX(-50%) translateY(-10px);
  background: rgba(0,0,0,0.75);
  color: white;
  padding: 12px 20px;
  border-radius: 50px;
  font-weight: bold;
  font-size: 14px;
  opacity: 0;
  transition: all 0.3s ease;
  z-index: 9999;
  max-width: 90%;
  text-align: center;
}
.toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }

/* === SAO BAY === */
@keyframes floatUp {
  0% { opacity: 1; transform: translateY(0) scale(1); }
  100% { opacity: 0; transform: translateY(-50px) scale(0.5); }
}
</style>
</head>
<body>
<div class="toast" id="toast"></div>
<div class="container">
  <div class="header">
    <h1>🏫 Quản Lý Lớp Tiểu Học</h1>
    <button class="sound-toggle" id="soundBtn" onclick="toggleSound()">🔊</button>
  </div>

  <!-- MÀN HÌNH CHÍNH -->
  <div id="screen-home">
    <h2 class="awards-title">🏆 VINH DANH TUẦN 🏆</h2>
    
    <div class="section-label">👤 Cá Nhân Xuất Sắc</div>
    <div class="top-row" id="top-students"></div>

    <div class="section-label">👥 Tổ Xuất Sắc</div>
    <div class="top-row" id="top-teams"></div>

    <div class="nav-grid">
      <button class="nav-btn btn-student" onclick="showScreen('screen-student')">👤 Học Sinh</button>
      <button class="nav-btn btn-team" onclick="showScreen('screen-team')">👥 Tổ Nhóm</button>
      <button class="nav-btn btn-random" onclick="showScreen('screen-random')">🎲 Gọi Ngẫu Nhiên</button>
      <button class="nav-btn btn-timer" onclick="showScreen('screen-timer')">⏱️ Đếm Ngược</button>
      <button class="nav-btn btn-history" onclick="showScreen('screen-history')">📜 Lịch Sử Điểm</button>
    </div>
  </div>

  <!-- QUẢN LÝ HỌC SINH -->
  <div id="screen-student" class="panel">
    <h3>👤 Quản Lý Học Sinh</h3>
    <input type="text" id="new-student-name" placeholder="Nhập tên học sinh...">
    <select id="new-student-team"></select>
    <button class="btn btn-add" onclick="addStudent()">✅ Thêm Học Sinh</button>

    <h4>🎯 Cộng / Trừ Điểm</h4>
    <select id="sel-student"></select>
    <div class="btn-row">
      <input type="number" id="score-val" value="1" min="1" inputmode="numeric" style="flex:1;">
      <button class="btn btn-add" onclick="changeScore(true)">+</button>
      <button class="btn btn-sub" onclick="changeScore(false)">−</button>
    </div>
    <input type="text" id="score-reason" placeholder="Lý do...">

    <h4>📋 Danh Sách</h4>
    <div id="student-list"></div>
    <button class="btn btn-back" onclick="showScreen('screen-home')">← Trở lại Trang Chủ</button>
  </div>

  <!-- QUẢN LÝ TỔ -->
  <div id="screen-team" class="panel">
    <h3>👥 Quản Lý Tổ</h3>
    <input type="text" id="new-team-name" placeholder="Nhập tên tổ...">
    <button class="btn btn-add" onclick="addTeam()">✅ Tạo Tổ Mới</button>

    <h4>🎯 Cộng / Trừ Điểm Tổ</h4>
    <select id="sel-team"></select>
    <div class="btn-row">
      <input type="number" id="team-score-val" value="5" min="1" inputmode="numeric" style="flex:1;">
      <button class="btn btn-add" onclick="changeTeamScore(true)">+</button>
      <button class="btn btn-sub" onclick="changeTeamScore(false)">−</button>
    </div>
    <input type="text" id="team-score-reason" placeholder="Lý do...">

    <h4>📋 Danh Sách Tổ</h4>
    <div id="team-list"></div>
    <button class="btn btn-back" onclick="showScreen('screen-home')">← Trở lại Trang Chủ</button>
  </div>

  <!-- GỌI NGẪU NHIÊN -->
  <div id="screen-random" class="panel">
    <h3>🎲 Gọi Ngẫu Nhiên</h3>
    <select id="random-filter" onchange="updateRandomFilter()">
      <option value="all">Tất cả học sinh</option>
      <option value="team">Theo Tổ</option>
    </select>
    <select id="random-team" style="display:none;"></select>
    <div class="random-display" id="random-result">Nhấn nút bên dưới ↓</div>
    <button class="random-btn" id="random-btn" onclick="pickRandom()">🎯 Bốc thăm ngay!</button>
    <button class="btn btn-back" onclick="showScreen('screen-home')">← Trở lại Trang Chủ</button>
  </div>

  <!-- ĐẾM NGƯỢC -->
  <div id="screen-timer" class="panel">
    <h3>⏱️ Đồng Hồ Đếm Ngược</h3>
    <div class="timer-display" id="timer-display">05:00</div>
    <div class="timer-quick">
      <button onclick="setQuick(1)">1'</button>
      <button onclick="setQuick(3)">3'</button>
      <button onclick="setQuick(5)">5'</button>
      <button onclick="setQuick(10)">10'</button>
    </div>
    <div class="timer-row">
      <input type="number" id="timer-min" placeholder="Phút" min="0" max="60" value="5" inputmode="numeric">
      <input type="number" id="timer-sec" placeholder="Giây" min="0" max="59" value="0" inputmode="numeric">
    </div>
    <div class="timer-buttons">
      <button class="timer-btn timer-start" id="timer-toggle" onclick="toggleTimer()">▶️ Bắt đầu</button>
      <button class="timer-btn timer-reset" onclick="resetTimer()">🔄 Đặt lại</button>
    </div>
    <button class="btn btn-back" onclick="showScreen('screen-home')">← Trở lại Trang Chủ</button>
  </div>

  <!-- LỊCH SỬ -->
  <div id="screen-history" class="panel">
    <h3>📜 Lịch Sử Thay Đổi Điểm</h3>
    <div id="history-list"></div>
    <button class="btn btn-delete" style="margin-top:15px;" onclick="clearHistory()">🗑️ Xóa Lịch Sử</button>
    <button class="btn btn-back" onclick="showScreen('screen-home')">← Trở lại Trang Chủ</button>
  </div>
</div>

<script>
// === ÂM THANH TỐI ƯU ĐIỆN THOẠI ===
let soundEnabled = true;
let audioCtx = null;

function initAudio() {
  if (!audioCtx && (window.AudioContext || window.webkitAudioContext)) {
    try {
      audioCtx = new (window.AudioContext || window.webkitAudioContext)();
      if (audioCtx.state === 'suspended') audioCtx.resume();
    } catch (e) { /* bỏ qua nếu không hỗ trợ */ }
  }
}

function playSound(type) {
  if (!soundEnabled || !audioCtx) return;
  if (audioCtx.state === 'suspended') audioCtx.resume();

  function playTone(freq, dur, vol) {
    try {
      const o = audioCtx.createOscillator();
      const g = audioCtx.createGain();
      o.connect(g); g.connect(audioCtx.destination);
      o.frequency.value = freq;
      o.type = 'sine';
      g.gain.value = vol * 0.25;
      o.start();
      g.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + dur);
      o.stop(audioCtx.currentTime + dur);
    } catch(e) {}
  }

  switch(type) {
    case 'click': playTone(700, 0.06, 0.15); break;
    case 'add': 
      playTone(523, 0.15, 0.2);
      setTimeout(() => playTone(659, 0.15, 0.2), 80);
      setTimeout(() => playTone(784, 0.2, 0.2), 160);
      break;
    case 'sub':
      playTone(400, 0.12, 0.15);
      setTimeout(() => playTone(350, 0.15, 0.12), 80);
      break;
    case 'win':
      [523, 659, 784, 1047].forEach((f,i) => setTimeout(() => playTone(f, 0.25, 0.2), i*100));
      break;
    case 'tick': playTone(880, 0.04, 0.12); break;
    case 'bell':
      playTone(784, 0.3, 0.25);
      setTimeout(() => playTone(988, 0.3, 0.2), 150);
      break;
    case 'roll':
      playTone(500 + Math.random()*300, 0.06, 0.1);
      break;
  }
}

function toggleSound() {
  soundEnabled = !soundEnabled;
  document.getElementById('soundBtn').textContent = soundEnabled ? '🔊' : '🔇';
  if (soundEnabled) {
    initAudio();
    setTimeout(() => playSound('click'), 50);
  }
}

// === HIỆU ỨNG SAO BAY ===
function showStars(containerEl, count=6) {
  const rect = containerEl.getBoundingClientRect();
  for (let i=0; i<count; i++) {
    const s = document.createElement('span');
    s.textContent = '⭐';
    s.style.cssText = `
      position: fixed; font-size: 20px; pointer-events: none; z-index: 9999;
      left: ${rect.left + Math.random()*rect.width}px;
      top: ${rect.top + 10}px;
      animation: floatUp 1s ease-out forwards;
    `;
    document.body.appendChild(s);
    setTimeout(() => s.remove(), 1000);
  }
}

// === DỮ LIỆU ===
let teams = JSON.parse(localStorage.getItem('teams')) || [];
let students = JSON.parse(localStorage.getItem('students')) || [];
let history = JSON.parse(localStorage.getItem('history')) || [];
let prevTopIds = [];

function saveData() {
  localStorage.setItem('teams', JSON.stringify(teams));
  localStorage.setItem('students', JSON.stringify(students));
  localStorage.setItem('history', JSON.stringify(history));
}

function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg; t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 2500);
}

// === CHUYỂN MÀN HÌNH ===
function showScreen(id) {
  initAudio(); // chuẩn bị âm thanh khi nhấn nút
  playSound('click');
  document.querySelectorAll('.panel').forEach(p => p.classList.remove('show'));
  document.getElementById('screen-home').style.display = 'none';
  if (id === 'screen-home') {
    document.getElementById('screen-home').style.display = 'block';
  } else {
    document.getElementById(id).classList.add('show');
  }
  updateAll();
}

// === TỔ ===
function addTeam() {
  const name = document.getElementById('new-team-name').value.trim();
  if (!name) return showToast('Nhập tên tổ!');
  if (teams.find(t => t.name === name)) return showToast('Tên tổ đã tồn tại!');
  teams.push({ id: Date.now(), name });
  document.getElementById('new-team-name').value = '';
  saveData(); updateAll();
  playSound('add'); showToast('✅ Đã tạo: ' + name);
}
function deleteTeam(id) {
  if (!confirm('Xóa tổ này? Tất cả học sinh trong tổ cũng bị xóa!')) return;
  teams = teams.filter(t => t.id !== id);
  students = students.filter(s => s.teamId !== id);
  saveData(); updateAll();
  playSound('sub'); showToast('🗑️ Đã xóa tổ');
}

// === HỌC SINH ===
function addStudent() {
  const name = document.getElementById('new-student-name').value.trim();
  const tid = parseInt(document.getElementById('new-student-team').value);
  if (!name) return showToast('Nhập tên học sinh!');
  if (!tid) return showToast('Chọn tổ!');
  students.push({ id: Date.now(), name, teamId: tid, score: 0 });
  document.getElementById('new-student-name').value = '';
  saveData(); updateAll();
  playSound('add'); showToast('✅ Đã thêm: ' + name);
}
function deleteStudent(id) {
  if (!confirm('Xóa học sinh này?')) return;
  students = students.filter(s => s.id !== id);
  saveData(); updateAll();
  playSound('sub'); showToast('🗑️ Đã xóa học sinh');
}

// === KIỂM TRA LÊN TOP 3 ===
function checkTopChange() {
  const top3Now = [...students].sort((a,b)=>b.score-a.score).slice(0,3).map(s=>s.id);
  const newOnes = top3Now.filter(id => !prevTopIds.includes(id));
  prevTopIds = top3Now;
  if (newOnes.length > 0) {
    setTimeout(() => {
      playSound('win');
      showStars(document.getElementById('top-students'), 10);
      showToast('🎉 Có người mới lên TOP 3!');
    }, 300);
  }
}

// === CỘNG/TRỪ ĐIỂM ===
function changeScore(isAdd) {
  const sid = parseInt(document.getElementById('sel-student').value);
  const val = parseInt(document.getElementById('score-val').value) || 1;
  const reason = document.getElementById('score-reason').value.trim() || 'Không ghi rõ';
  const s = students.find(x => x.id === sid);
  if (!s) return showToast('Chọn học sinh!');

  s.score += isAdd ? val : -val;
  if (s.score < 0) s.score = 0;

  history.unshift({
    time: new Date().toLocaleString('vi-VN'),
    type: 'student', target: s.name,
    change: isAdd ? val : -val, reason
  });

  document.getElementById('score-reason').value = '';
  saveData(); updateAll();
  playSound(isAdd ? 'add' : 'sub');
  if (isAdd) showStars(document.getElementById('sel-student'), 5);
  checkTopChange();
  showToast(`${isAdd?'✅ +':'❌ '}${val} điểm → ${s.name}`);
}

function changeTeamScore(isAdd) {
  const tid = parseInt(document.getElementById('sel-team').value);
  const val = parseInt(document.getElementById('team-score-val').value) || 5;
  const reason = document.getElementById('team-score-reason').value.trim() || 'Không ghi rõ';
  const t = teams.find(x => x.id === tid);
  if (!t) return showToast('Chọn tổ!');

  const members = students.filter(s => s.teamId === tid);
  const per = Math.ceil(val / members.length) || val;
  members.forEach(s => {
    s.score += isAdd ? per : -per;
    if (s.score < 0) s.score = 0;
  });

  history.unshift({
    time: new Date().toLocaleString('vi-VN'),
    type: 'team', target: t.name,
    change: isAdd ? val : -val, reason
  });

  document.getElementById('team-score-reason').value = '';
  saveData(); updateAll();
  playSound(isAdd ? 'add' : 'sub');
  checkTopChange();
  showToast(`${isAdd?'✅ +':'❌ '}${val} điểm → ${t.name}`);
}

function clearHistory() {
  if (!confirm('Xóa toàn bộ lịch sử?')) return;
  history = []; saveData(); updateAll();
  playSound('sub'); showToast('🗑️ Đã xóa lịch sử');
}

// === RENDER TOP 3 ===
function renderTop3(containerId, list, getName, getScore) {
  const c = document.getElementById(containerId);
  let html = '';
  for (let i=0; i<3; i++) {
    const x = list[i];
    if (x) {
      const cls = i===0 ? 'card-1' : i===1 ? 'card-2' : 'card-3';
      const medal = i===0 ? '🥇' : i===1 ? '🥈' : '🥉';
      html += `
        <div class="card ${cls}">
          <div class="card-rank">${medal}</div>
          <div class="card-name">${getName(x)}</div>
          <div class="card-score">${getScore(x)} điểm</div>
        </div>`;
    } else {
      html += `<div class="card card-empty">Chưa có</div>`;
    }
  }
  c.innerHTML = html;
}

// === GỌI NGẪU NHIÊN ===
let isRolling = false;
function updateRandomFilter() {
  const show = document.getElementById('random-filter').value === 'team';
  document.getElementById('random-team').style.display = show ? 'block' : 'none';
}
function getPool() {
  const filter = document.getElementById('random-filter').value;
  if (filter === 'team') {
    const tid = parseInt(document.getElementById('random-team').value);
    return students.filter(s => s.teamId === tid);
  }
  return students;
}
function pickRandom() {
  const pool = getPool();
  if (!pool.length) return showToast('Chưa có học sinh!');
  const res = document.getElementById('random-result');
  const btn = document.getElementById('random-btn');
  if (isRolling) return;
  isRolling = true;
  btn.textContent = 'Đang chọn...';
  res.classList.add('rolling');
  let c = 0, max = 20;
  const interval = setInterval(() => {
    res.textContent = pool[Math.floor(Math.random()*pool.length)].name;
    playSound('roll');
    if (++c >= max) {
      clearInterval(interval);
      const chosen = pool[Math.floor(Math.random()*pool.length)];
      const t = teams.find(x => x.id === chosen.teamId);
      res.innerHTML = `<strong style="font-size:32px;">${chosen.name}</strong><br><small style="color:#7B1FA2;">${t?.name||'Chưa có tổ'} · ${chosen.score} điểm</small>`;
      res.classList.remove('rolling');
      btn.textContent = '🎯 Bốc thăm lại!';
      isRolling = false;
      playSound('bell');
      showStars(res, 8);
    }
  }, 70);
}

// === ĐẾM NGƯỢC ===
let sec = 0, timer = null, running = false;
function setQuick(m) {
  document.getElementById('timer-min').value = m;
  document.getElementById('timer-sec').value = 0;
  updateTimerDisplay(m*60);
  playSound('click');
}
function updateTimerDisplay(s) {
  const m = Math.floor(s/60), ss = s%60;
  const d = document.getElementById('timer-display');
  d.textContent = `${String(m).padStart(2,'0')}:${String(ss).padStart(2,'0')}`;
  d.classList.remove('warning','danger');
  if (s <= 10 && s > 5) d.classList.add('warning');
  if (s <= 5 && s > 0) d.classList.add('danger');
}
function toggleTimer() {
  if (running) {
    clearInterval(timer); running = false;
    document.getElementById('timer-toggle').textContent = '▶️ Bắt đầu';
    document.getElementById('timer-toggle').className = 'timer-btn timer-start';
    return;
  }
  const m = parseInt(document.getElementById('timer-min').value)||0;
  const s = parseInt(document.getElementById('timer-sec').value)||0;
  sec = m*60 + s;
  if (sec <= 0) return showToast('Nhập thời gian!');
  running = true;
  document.getElementById('timer-toggle').textContent = '⏸️ Tạm dừng';
  document.getElementById('timer-toggle').className = 'timer-btn timer-pause';
  timer = setInterval(() => {
    if (--sec <= 0) {
      clearInterval(timer); running = false;
      document.getElementById('timer-display').textContent = 'HẾT GIỜI! ⏰';
      document.getElementById('timer-toggle').textContent = '▶️ Bắt đầu';
      document.getElementById('timer-toggle').className = 'timer-btn timer-start';
      playSound('bell'); playSound('bell');
      return;
    }
    if (sec <= 10) playSound('tick');
    updateTimerDisplay(sec);
  }, 1000);
}
function resetTimer() {
  clearInterval(timer); running = false;
  const m = parseInt(document.getElementById('timer-min').value)||0;
  const s = parseInt(document.getElementById('timer-sec').value)||0;
  sec = m*60 + s;
  updateTimerDisplay(sec);
  document.getElementById('timer-toggle').textContent = '▶️ Bắt đầu';
  document.getElementById('timer-toggle').className = 'timer-btn timer-start';
  playSound('click');
}

// === CẬP NHẬT TOÀN BỘ ===
function updateAll() {
  const teamOpts = () => `<option value="">-- Chọn --</option>` +
    teams.map(t => `<option value="${t.id}">${t.name}</option>`).join('');

  document.getElementById('new-student-team').innerHTML = teamOpts();
  document.getElementById('sel-team').innerHTML = teamOpts();
  document.getElementById('random-team').innerHTML = teamOpts();

  document.getElementById('sel-student').innerHTML =
    `<option value="">-- Chọn học sinh --</option>` +
    students.map(s => {
      const t = teams.find(x => x.id === s.teamId);
      return `<option value="${s.id}">${s.name} — ${t?.name||'Chưa có tổ'} (${s.score} điểm)</option>`;
    }).join('');

  // Top 3 Cá nhân
  const rankStu = [...students].sort((a,b)=>b.score-a.score);
  renderTop3('top-students', rankStu, s=>s.name, s=>s.score);

  // Top 3 Tổ
  const rankTeam = teams.map(t => ({
    ...t, total: students.filter(s=>s.teamId===t.id).reduce((sum,s)=>sum+s.score,0)
  })).sort((a,b)=>b.total-a.total);
  renderTop3('top-teams', rankTeam, t=>t.name, t=>t.total);

  // Danh sách học sinh
  document.getElementById('student-list').innerHTML = students.length ? students.map(s=>{
    const t = teams.find(x=>x.id===s.teamId);
    return `<div class="list-item">
      <div><strong>${s.name}</strong><br><small style="color:#90A4AE;">${t?.name||'Chưa có tổ'}</small></div>
      <div style="display:flex;align-items:center;">
        <span class="score-val">${s.score}</span>
        <button class="del-btn" onclick="deleteStudent(${s.id})">Xóa</button>
      </div>
    </div>`;
  }).join('') : '<p style="color:#90A4AE;text-align:center;padding:15px;">Chưa có học sinh</p>';

  // Danh sách Tổ
  document.getElementById('team-list').innerHTML = teams.length ? teams.map(t=>{
    const mem = students.filter(s=>s.teamId===t.id);
    const total = mem.reduce((sum,s)=>sum+s.score,0);
    return `<div class="list-item">
      <div><strong>${t.name}</strong><br><small style="color:#90A4AE;">${mem.length} thành viên</small></div>
      <div style="display:flex;align-items:center;">
        <span class="score-val">${total}</span>
        <button class="del-btn" onclick="deleteTeam(${t.id})">Xóa</button>
      </div>
    </div>`;
  }).join('') : '<p style="color:#90A4AE;text-align:center;padding:15px;">Chưa có Tổ</p>';

  // Lịch sử
  document.getElementById('history-list').innerHTML = history.length ? history.map(h=>`
    <div class="history-item ${h.change>0?'plus':'minus'}">
      <strong>${h.change>0?'+':''}${h.change} điểm</strong> — ${h.type==='student'?'👤':'👥'} ${h.target}
      <span class="history-time">${h.time} · ${h.reason}</span>
    </div>
  `).join('') : '<p style="color:#90A4AE;text-align:center;padding:15px;">Chưa có lịch sử</p>';
}

// === KHỞI TẠO ===
document.addEventListener('DOMContentLoaded', () => {
  showScreen('screen-home');
  updateAll();
  prevTopIds = [...students].sort((a,b)=>b.score-a.score).slice(0,3).map(s=>s.id);
  // chuẩn bị âm thanh khi người dùng chạm màn hình lần đầu
  document.addEventListener('touchstart', initAudio, { once: true });
  document.addEventListener('click', initAudio, { once: true });
});
</script>
</body>
</html>
