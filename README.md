<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>抽獎遊戲</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
        }
        h1 {
            color: #333;
        }
        .container {
            text-align: center;
        }
        .input-container {
            margin-bottom: 20px;
        }
        input[type="text"] {
            padding: 8px;
            font-size: 16px;
            width: 200px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            margin: 5px;
        }
        .result {
            margin-top: 20px;
            font-size: 18px;
            color: #333;
            opacity: 0;
            transition: opacity 0.5s ease-in;
        }
        .result.visible {
            opacity: 1;
        }
        .hidden {
            display: none;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>抽獎遊戲</h1>
        <div class="input-container">
            <input type="text" id="username" placeholder="請輸入您的名稱">
        </div>
        <button onclick="startDraw()">開始抽獎</button>
        <div id="resultsContainer"></div>
        <button class="hidden" id="tryAgainBtn" onclick="resetGame()">再來一次</button>
        <button class="hidden" id="backBtn" onclick="goToMainPage()">回到主頁</button>
    </div>

    <script>
        function getPrize() {
            const chance = Math.random() * 100;

            if (chance < 1) {
                const subChance = Math.random();
                if (subChance < 0.3) return "獎項1 - 立牌（長髮）";
                if (subChance < 0.6) return "獎項1 - 立牌（短髮）";
                if (subChance < 0.7) return "獎項1 - 飯友（長髮）";
                if (subChance < 0.8) return "獎項1 - 飯友（短髮）";
                return "獎項1 - 貼紙";
            } else if (chance < 92) {
                return "鳴謝惠顧";
            } else if (chance < 97) {
                return "再來一次";
            } else {
                return "BAN600";
            }
        }

        function startDraw() {
            const username = document.getElementById('username').value;
            if (!username) {
                alert("請先輸入您的名稱！");
                return;
            }

            // 清空結果區域
            const resultsContainer = document.getElementById('resultsContainer');
            resultsContainer.innerHTML = "";

            // 5秒延遲後開始顯示抽獎結果
            setTimeout(() => {
                let results = [];
                for (let i = 0; i < 10; i++) {
                    results.push(`第 ${i + 1} 次抽獎結果: ` + getPrize());
                }

                results.forEach((result, index) => {
                    // 創建結果的 <div> 元素
                    const resultDiv = document.createElement("div");
                    resultDiv.classList.add("result");
                    resultDiv.innerHTML = `<strong>${username} 的第 ${index + 1} 次抽獎結果：</strong> ${result}`;
                    
                    // 延遲 0.3 秒顯示每個結果
                    setTimeout(() => {
                        resultDiv.classList.add("visible");
                    }, index * 300);
                    
                    resultsContainer.appendChild(resultDiv);
                });

                // 顯示 "再來一次" 和 "回到主頁" 按鈕
                document.getElementById('tryAgainBtn').classList.remove('hidden');
                document.getElementById('backBtn').classList.remove('hidden');
            }, 5000);
        }

        function resetGame() {
            document.getElementById('resultsContainer').innerHTML = "";
            document.getElementById('tryAgainBtn').classList.add('hidden');
            document.getElementById('backBtn').classList.add('hidden');
            document.getElementById('username').value = "";
        }

        function goToMainPage() {
            alert("回到主頁");
            resetGame();
        }
    </script>

</body>
</html>
