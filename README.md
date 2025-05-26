<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Almanca - Türkçe Kelime Testi</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet" />
<style>
  /* ===== Temel Stil ve Font ===== */
  body {
    font-family: 'Inter', sans-serif;
    background-color: #f5f7fa;
    color: #333;
    margin: 0;
    display: flex;
    height: 100vh;
    transition: background-color 0.3s ease, color 0.3s ease;
  }
  body.dark-mode {
    background-color: #121212;
    color: #ddd;
  }

  /* ===== Sidebar ===== */
  #sidebar {
    width: 240px;
    background: #34495e;
    color: #ecf0f1;
    padding: 20px;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    gap: 12px;
    transition: width 0.3s ease;
    box-shadow: 2px 0 8px rgba(0,0,0,0.15);
    border-top-right-radius: 10px;
    border-bottom-right-radius: 10px;
  }
  #sidebar.collapsed {
    width: 60px;
  }
  #sidebar button, #sidebar label {
    background: #3d566e;
    border: none;
    padding: 12px 16px;
    border-radius: 8px;
    font-weight: 600;
    color: #ecf0f1;
    cursor: pointer;
    transition: background-color 0.2s ease;
    text-align: left;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    user-select: none;
  }
  #sidebar button:hover, #sidebar label:hover {
    background: #5a7ab8;
    color: white;
  }
  #sidebar.collapsed button, #sidebar.collapsed label {
    text-indent: -9999px;
    padding: 12px 0;
  }
  #toggleSidebarBtn {
    background: #27ae60;
    font-size: 22px;
    padding: 12px;
    border-radius: 8px;
    margin-bottom: 20px;
    transition: background-color 0.3s ease;
  }
  #toggleSidebarBtn:hover {
    background: #2ecc71;
  }

  /* ===== Content ===== */
  #content {
    flex-grow: 1;
    padding: 40px 50px;
    overflow-y: auto;
  }

  /* ===== Bölümler ===== */
  section {
    max-width: 700px;
    margin: 0 auto;
    background: white;
    border-radius: 16px;
    padding: 30px 40px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.1);
    transition: background-color 0.3s ease, box-shadow 0.3s ease;
  }
  body.dark-mode section {
    background: #1f2937;
    box-shadow: 0 10px 30px rgba(0,0,0,0.5);
  }
  section h2 {
    font-weight: 700;
    margin-bottom: 24px;
    color: #2c3e50;
  }
  body.dark-mode section h2 {
    color: #f5f5f5;
  }

  /* ===== Form Elemanları ===== */
  input[type="text"], input[type="number"], input[type="file"], textarea {
    width: 100%;
    padding: 14px 18px;
    margin: 10px 0 24px;
    border-radius: 12px;
    border: 1px solid #ccc;
    font-size: 18px;
    transition: border-color 0.3s ease;
    box-sizing: border-box;
    resize: vertical;
  }
  input[type="text"]:focus,
  input[type="number"]:focus,
  input[type="file"]:focus,
  textarea:focus {
    outline: none;
    border-color: #5a7ab8;
    box-shadow: 0 0 8px rgba(90,122,184,0.4);
  }
  body.dark-mode input[type="text"],
  body.dark-mode input[type="number"],
  body.dark-mode input[type="file"],
  body.dark-mode textarea {
    background-color: #2d3748;
    color: #eee;
    border-color: #555;
  }

  /* ===== Buton ===== */
  button.submitBtn {
    background-color: #5a7ab8;
    color: white;
    border: none;
    padding: 16px 28px;
    font-size: 18px;
    border-radius: 12px;
    cursor: pointer;
    font-weight: 600;
    box-shadow: 0 6px 15px rgba(90,122,184,0.4);
    transition: background-color 0.3s ease, box-shadow 0.3s ease;
  }
  button.submitBtn:hover {
    background-color: #4169e1;
    box-shadow: 0 8px 20px rgba(65,105,225,0.6);
  }

  /* ===== Yazı ve Durum ===== */
  #wordDisplay {
    font-size: 30px;
    font-weight: 700;
    margin-bottom: 20px;
    text-align: center;
    color: #34495e;
  }
  body.dark-mode #wordDisplay {
    color: #a0aec0;
  }
  #status {
    font-size: 20px;
    min-height: 30px;
    margin-bottom: 20px;
    text-align: center;
    font-weight: 600;
  }
  #timer {
    font-weight: 700;
    font-size: 22px;
    margin-bottom: 30px;
    text-align: center;
    color: #2c3e50;
  }
  body.dark-mode #timer {
    color: #a0aec0;
  }

  /* ===== Tab Menü Butonları ===== */
  .tab-buttons {
    display: flex;
    gap: 15px;
    margin-bottom: 20px;
    flex-wrap: wrap;
  }
  .tab-buttons button {
    flex-grow: 1;
    background: #3d566e;
    border: none;
    padding: 12px 16px;
    border-radius: 8px;
    color: #ecf0f1;
    font-weight: 600;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  .tab-buttons button.active,
  .tab-buttons button:hover {
    background: #5a7ab8;
  }

  /* ===== Responsive ===== */
  @media (max-width: 768px) {
    #sidebar {
      position: fixed;
      height: 100%;
      z-index: 999;
      bottom: 0;
      top: 0;
      left: 0;
      border-radius: 0;
    }
    #content {
      padding: 20px;
      margin-left: 60px;
    }
    #sidebar.collapsed {
      width: 60px;
    }
  }

  /* ===== Kapanma animasyonu ve görünürlük ===== */
  .hidden {
    display: none !important;
  }
</style>
</head>
<body>
  <div id="sidebar">
    <button id="toggleSidebarBtn" title="Sidebar Kapat/Aç">☰</button>
    <button class="sidebar-tab-btn active" data-tab="test">Test</button>
    <button class="sidebar-tab-btn" data-tab="addWords">Kelime Ekle</button>
    <button class="sidebar-tab-btn" data-tab="editTime">Süre Düzenle</button>
    <button id="toggleDarkModeBtn" title="Karanlık Mod Aç/Kapat">🌓 Karanlık Mod</button>
  </div>

  <div id="content">
    <!-- Test Bölümü -->
    <section id="testSection">
      <h2>Kelime Testi</h2>
      <div id="timer">Süre: 60</div>
      <div id="wordDisplay">Başlamak için "Başlat" butonuna basın</div>
      <input type="text" id="answerInput" placeholder="Türkçe karşılığı yazın" autocomplete="off" disabled />
      <div id="status"></div>
      <button id="startTestBtn" class="submitBtn">Başlat</button>
    </section>

    <!-- Kelime Ekleme Bölümü -->
    <section id="addWordsSection" class="hidden">
      <h2>Kelime Ekle</h2>
      <label for="newWordDe">Almanca Kelime:</label>
      <input type="text" id="newWordDe" placeholder="Örn: Apfel" autocomplete="off" />
      <label for="newWordTr">Türkçe Karşılık:</label>
      <input type="text" id="newWordTr" placeholder="Örn: Elma" autocomplete="off" />
      <button id="addWordBtn" class="submitBtn">Ekle</button>
      <hr />
      <h3>Toplu CSV Dosyası Yükle (Almanca;Türkçe)</h3>
      <input type="file" id="csvFileInput" accept=".csv,text/csv" />
      <button id="loadCsvBtn" class="submitBtn" style="margin-top: 10px;">Yükle</button>
      <div id="csvLoadStatus"></div>
    </section>

    <!-- Süre Düzenleme Bölümü -->
    <section id="editTimeSection" class="hidden">
      <h2>Süre Düzenle</h2>
      <label for="testDurationInput">Test Süresi (saniye):</label>
      <input type="number" id="testDurationInput" min="10" max="600" value="60" />
      <button id="saveDurationBtn" class="submitBtn">Kaydet</button>
      <div id="durationStatus" style="margin-top: 10px; font-weight: 600;"></div>
    </section>

    <!-- Sonuç Ekranı -->
    <section id="resultSection" class="hidden">
      <h2>Test Sonucu</h2>
      <p>Doğru Sayısı: <span id="correctCountResult"></span></p>
      <p>Yanlış Sayısı: <span id="incorrectCountResult"></span></p>
      <button id="restartTestBtn" class="submitBtn">Yeni Test Başlat</button>
    </section>
  </div>

  <script>
    (() => {
      // DOM Elements
      const sidebar = document.getElementById('sidebar');
      const toggleSidebarBtn = document.getElementById('toggleSidebarBtn');
      const toggleDarkModeBtn = document.getElementById('toggleDarkModeBtn');

      const testSection = document.getElementById('testSection');
      const addWordsSection = document.getElementById('addWordsSection');
      const editTimeSection = document.getElementById('editTimeSection');
      const resultSection = document.getElementById('resultSection');

      const tabButtons = document.querySelectorAll('.sidebar-tab-btn');

      const timerDisplay = document.getElementById('timer');
      const wordDisplay = document.getElementById('wordDisplay');
      const answerInput = document.getElementById('answerInput');
      const statusDisplay = document.getElementById('status');
      const startTestBtn = document.getElementById('startTestBtn');
      const restartTestBtn = document.getElementById('restartTestBtn');

      // Kelime ekleme alanları
      const newWordDeInput = document.getElementById('newWordDe');
      const newWordTrInput = document.getElementById('newWordTr');
      const addWordBtn = document.getElementById('addWordBtn');
      const csvFileInput = document.getElementById('csvFileInput');
      const loadCsvBtn = document.getElementById('loadCsvBtn');
      const csvLoadStatus = document.getElementById('csvLoadStatus');

      // Süre düzenleme alanları
      const testDurationInput = document.getElementById('testDurationInput');
      const saveDurationBtn = document.getElementById('saveDurationBtn');
      const durationStatus = document.getElementById('durationStatus');

      // Veri
      let words = [
        { de: 'Apfel', tr: 'Elma' },
        { de: 'Haus', tr: 'Ev' },
        { de: 'Buch', tr: 'Kitap' },
        { de: 'Stuhl', tr: 'Sandalye' },
        { de: 'Tisch', tr: 'Masa' }
      ];

      let testDuration = 60; // saniye
      let timer = null;
      let timeLeft = testDuration;
      let currentWordIndex = 0;
      let correctCount = 0;
      let incorrectCount = 0;
      let testActive = false;

      // Sidebar toggle
      toggleSidebarBtn.addEventListener('click', () => {
        sidebar.classList.toggle('collapsed');
      });

      // Dark mode toggle
      toggleDarkModeBtn.addEventListener('click', () => {
        document.body.classList.toggle('dark-mode');
      });

      // Tab switch
      tabButtons.forEach(btn => {
        btn.addEventListener('click', () => {
          tabButtons.forEach(b => b.classList.remove('active'));
          btn.classList.add('active');
          showSection(btn.dataset.tab);
        });
      });

      function showSection(tab) {
        testSection.classList.add('hidden');
        addWordsSection.classList.add('hidden');
        editTimeSection.classList.add('hidden');
        resultSection.classList.add('hidden');

        if (tab === 'test') testSection.classList.remove('hidden');
        else if (tab === 'addWords') addWordsSection.classList.remove('hidden');
        else if (tab === 'editTime') editTimeSection.classList.remove('hidden');
      }

      // Test fonksiyonları
      function startTest() {
        if (words.length === 0) {
          alert('Lütfen önce kelime ekleyin.');
          return;
        }
        testDuration = parseInt(testDurationInput.value) || 60;
        timeLeft = testDuration;
        currentWordIndex = 0;
        correctCount = 0;
        incorrectCount = 0;
        testActive = true;

        updateTimerDisplay();
        startTestBtn.disabled = true;
        answerInput.disabled = false;
        answerInput.value = '';
        answerInput.focus();
        statusDisplay.textContent = '';
        wordDisplay.textContent = words[currentWordIndex].de;

        timer = setInterval(() => {
          timeLeft--;
          updateTimerDisplay();

          if (timeLeft <= 0) {
            finishTest();
          }
        }, 1000);
      }

      function updateTimerDisplay() {
        timerDisplay.textContent = `Süre: ${timeLeft}`;
      }

      function finishTest() {
        clearInterval(timer);
        testActive = false;
        startTestBtn.disabled = false;
        answerInput.disabled = true;
        statusDisplay.textContent = '';
        wordDisplay.textContent = '';

        // Sonuç ekranına geç
        document.querySelector('.sidebar-tab-btn.active').classList.remove('active');
        tabButtons.forEach(b => b.classList.remove('active'));
        resultSection.classList.remove('hidden');

        document.getElementById('correctCountResult').textContent = correctCount;
        document.getElementById('incorrectCountResult').textContent = incorrectCount;
      }

      // Cevap kontrolü
      answerInput.addEventListener('keydown', (e) => {
        if (!testActive) return;
        if (e.key === 'Enter') {
          checkAnswer();
        }
      });

      function checkAnswer() {
        let userAnswer = answerInput.value.trim().toLowerCase();
        let correctAnswer = words[currentWordIndex].tr.toLowerCase();

        if (userAnswer === '') return;

        if (userAnswer === correctAnswer) {
          correctCount++;
          statusDisplay.textContent = '✔ Doğru!';
          statusDisplay.style.color = 'green';
        } else {
          incorrectCount++;
          statusDisplay.textContent = `✘ Yanlış! Doğru cevap: ${words[currentWordIndex].tr}`;
          statusDisplay.style.color = 'red';
        }

        answerInput.value = '';
        currentWordIndex++;
        if (currentWordIndex >= words.length) {
          finishTest();
        } else {
          wordDisplay.textContent = words[currentWordIndex].de;
          answerInput.focus();
        }
      }

      startTestBtn.addEventListener('click', startTest);

      restartTestBtn.addEventListener('click', () => {
        resultSection.classList.add('hidden');
        showSection('test');
        startTestBtn.disabled = false;
        wordDisplay.textContent = 'Başlamak için "Başlat" butonuna basın';
      });

      // Kelime ekleme
      addWordBtn.addEventListener('click', () => {
        const de = newWordDeInput.value.trim();
        const tr = newWordTrInput.value.trim();
        if (!de || !tr) {
          alert('Lütfen her iki alanı da doldurun.');
          return;
        }
        words.push({ de, tr });
        newWordDeInput.value = '';
        newWordTrInput.value = '';
        alert(`"${de}" - "${tr}" kelimesi eklendi.`);
      });

      // CSV Yükleme
      loadCsvBtn.addEventListener('click', () => {
        const file = csvFileInput.files[0];
        if (!file) {
          alert('Lütfen bir CSV dosyası seçin.');
          return;
        }

        const reader = new FileReader();
        reader.onload = function(e) {
          const text = e.target.result;
          const lines = text.split(/\r?\n/);
          let addedCount = 0;
          lines.forEach(line => {
            if (!line.trim()) return;
            const parts = line.split(';');
            if (parts.length === 2) {
              const de = parts[0].trim();
              const tr = parts[1].trim();
              if (de && tr) {
                words.push({ de, tr });
                addedCount++;
              }
            }
          });
          csvLoadStatus.textContent = `${addedCount} kelime yüklendi.`;
          csvLoadStatus.style.color = 'green';
          csvFileInput.value = '';
        };
        reader.readAsText(file);
      });

      // Süre kaydetme
      saveDurationBtn.addEventListener('click', () => {
        let val = parseInt(testDurationInput.value);
        if (isNaN(val) || val < 10 || val > 600) {
          durationStatus.textContent = 'Süre 10 ile 600 saniye arasında olmalı.';
          durationStatus.style.color = 'red';
          return;
        }
        testDuration = val;
        durationStatus.textContent = `Test süresi ${val} saniye olarak ayarlandı.`;
        durationStatus.style.color = 'green';
      });

      // Sayfa yüklendiğinde default sekme
      showSection('test');
    })();
  </script>
</body>
</html>
