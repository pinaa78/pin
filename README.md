<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Benar atau Salah: Mitos vs Fakta</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #74b9ff, #0984e3);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
        }
        .game-container {
            background: white;
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
            width: 350px;
            text-align: center;
            position: relative;
        }
        .stats {
            display: flex;
            justify-content: space-between;
            font-weight: bold;
            margin-bottom: 20px;
            color: #2d3436;
        }
        .card {
            background: #dfe6e9;
            padding: 30px 20px;
            border-radius: 15px;
            min-height: 120px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            color: #2d3436;
            margin-bottom: 25px;
            box-shadow: inset 0 2px 5px rgba(0,0,0,0.05);
            transition: all 0.3s ease;
        }
        .btn-container {
            display: flex;
            gap: 15px;
        }
        button {
            flex: 1;
            padding: 12px;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: transform 0.1s, background 0.2s;
        }
        button:active {
            transform: scale(0.95);
        }
        .btn-salah {
            background-color: #ff7675;
            color: white;
        }
        .btn-salah:hover { background-color: #d63031; }
        .btn-benar {
            background-color: #55efc4;
            color: #2d3436;
        }
        .btn-benar:hover { background-color: #00b894; }
        #explanation {
            margin-top: 15px;
            font-size: 14px;
            color: #636e72;
            min-height: 40px;
        }
    </style>
</head>
<body>

    <div class="game-container">
        <h2>Mitos vs Fakta</h2>
        <div class="stats">
            <span id="score">Skor: 0</span>
            <span id="lives">Nyawa: ❤️❤️❤️</span>
        </div>
        
        <div class="card" id="question-card">
            Memuat pertanyaan...
        </div>

        <div class="btn-container">
            <button class="btn-salah" onclick="checkAnswer(false)">SALAH ❌</button>
            <button class="btn-benar" onclick="checkAnswer(true)">BENAR ✔️</button>
        </div>

        <div id="explanation"></div>
    </div>

    <script>
        // Daftar Pertanyaan (Bank Soal)
        const questions = [
            {
                text: "Pisang adalah buah yang tumbuh di pohon besar berbatang kayu.",
                answer: false,
                explanation: "Salah! Pisang sebenarnya adalah tanaman terna raksasa/herba, batangnya bukan kayu sejati."
            },
            {
                text: "Gurun terluas di dunia adalah Benua Antartika.",
                answer: true,
                explanation: "Benar! Antartika dikategorikan sebagai gurun kutub karena curah hujannya yang sangat rendah."
            },
            {
                text: "Manusia membagikan sekitar 50% DNA yang sama dengan pisang.",
                answer: true,
                explanation: "Benar! Banyak gen dasar untuk fungsi seluler yang mirip di antara makhluk hidup."
            },
            {
                text: "Piramida Giza di Mesir dibangun oleh para budak yang disiksa.",
                answer: false,
                explanation: "Salah! Bukti arkeologis menunjukkan mereka adalah pekerja bayaran/tukang batu profesional yang dihormati."
            }
        ];

        let currentIndex = 0;
        let score = 0;
        let lives = 3;
        let isAnswered = false;

        const cardElement = document.getElementById("question-card");
        const scoreElement = document.getElementById("score");
        const livesElement = document.getElementById("lives");
        const explanationElement = document.getElementById("explanation");

        function loadQuestion() {
            if (lives <= 0) {
                cardElement.innerHTML = "Game Over! 🎮<br>Skor Akhir Anda: " + score;
                document.querySelector(".btn-container").style.display = "none";
                explanationElement.innerHTML = "";
                return;
            }

            if (currentIndex >= questions.length) {
                cardElement.innerHTML = "Selamat! Anda menyelesaikan semua soal! 🎉<br>Skor: " + score;
                document.querySelector(".btn-container").style.display = "none";
                explanationElement.innerHTML = "";
                return;
            }

            isAnswered = false;
            cardElement.innerHTML = questions[currentIndex].text;
            explanationElement.innerHTML = "";
        }

        function checkAnswer(playerChoice) {
            if (isAnswered) return;
            isAnswered = true;

            const currentQ = questions[currentIndex];
            
            if (playerChoice === currentQ.answer) {
                score += 10;
                explanationElement.innerHTML = "✅ **Benar!** " + currentQ.explanation;
                explanationElement.style.color = "#00b894";
            } else {
                lives -= 1;
                explanationElement.innerHTML = "❌ **Salah!** " + currentQ.explanation;
                explanationElement.style.color = "#d63031";
            }

            // Perbarui tampilan UI
            scoreElement.innerText = "Skor: " + score;
            livesElement.innerText = "Nyawa: " + "❤️".repeat(lives);
            currentIndex++;

            // Jeda 2,5 detik sebelum lanjut ke soal berikutnya
            setTimeout(loadQuestion, 2500);
        }

        // Jalankan game saat pertama kali dibuka
        loadQuestion();
    </script>

</body>
</html>
