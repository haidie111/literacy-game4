[二年级下生字学习助手.html](https://github.com/user-attachments/files/23447518/default.html)
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>二年级下学期识字游戏</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "微软雅黑", "楷体", sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        
        .container {
            width: 100%;
            max-width: 800px;
            background-color: white;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(to right, #4facfe, #00f2fe);
            color: white;
            padding: 20px;
            text-align: center;
            position: relative;
        }
        
        .header h1 {
            font-size: 28px;
            margin-bottom: 10px;
        }
        
        .header p {
            font-size: 16px;
            opacity: 0.9;
        }
        
        .header::after {
            content: "";
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 5px;
            background: linear-gradient(to right, #43e97b, #38f9d7);
        }
        
        .content {
            padding: 30px;
        }
        
        .mode-selection {
            display: flex;
            justify-content: space-around;
            margin-bottom: 30px;
        }
        
        .mode-btn {
            padding: 15px 25px;
            border: none;
            border-radius: 50px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .mode-btn.pinyin {
            background: linear-gradient(to right, #ff6b6b, #ff8e8e);
            color: white;
        }
        
        .mode-btn.hanzi {
            background: linear-gradient(to right, #43e97b, #38f9d7);
            color: white;
        }
        
        .mode-btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
        }
        
        .mode-btn.active {
            transform: scale(1.05);
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.2);
        }
        
        .game-area {
            background-color: #f8f9fa;
            border-radius: 15px;
            padding: 30px;
            text-align: center;
            margin-bottom: 20px;
            min-height: 300px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            position: relative;
        }
        
        .question {
            font-size: 48px;
            margin-bottom: 30px;
            color: #333;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }
        
        .pinyin-question {
            font-size: 42px;
            color: #ff6b6b;
        }
        
        .hanzi-question {
            font-size: 60px;
            color: #4facfe;
        }
        
        .options {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            width: 100%;
            max-width: 500px;
        }
        
        .option {
            padding: 15px;
            background-color: white;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 24px;
            cursor: pointer;
            transition: all 0.2s;
        }
        
        .option:hover {
            background-color: #f0f0f0;
            transform: translateY(-3px);
        }
        
        .option.correct {
            background-color: #a8e6cf;
            border-color: #56c596;
            animation: pulse 0.5s;
        }
        
        .option.wrong {
            background-color: #ffaaa5;
            border-color: #ff8b94;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        .controls {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 20px;
        }
        
        .level-info {
            font-size: 18px;
            font-weight: bold;
            color: #4facfe;
        }
        
        .next-btn {
            padding: 10px 25px;
            background: linear-gradient(to right, #4facfe, #00f2fe);
            border: none;
            border-radius: 50px;
            color: white;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .next-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
        }
        
        .next-btn:disabled {
            background: #cccccc;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        
        .score {
            font-size: 18px;
            font-weight: bold;
            color: #ff6b6b;
            margin-top: 20px;
        }
        
        .progress-bar {
            height: 10px;
            background-color: #e0e0e0;
            border-radius: 5px;
            margin-top: 20px;
            overflow: hidden;
        }
        
        .progress {
            height: 100%;
            background: linear-gradient(to right, #4facfe, #00f2fe);
            width: 0%;
            transition: width 0.5s;
        }
        
        .feedback {
            margin-top: 15px;
            font-size: 18px;
            font-weight: bold;
            min-height: 27px;
        }
        
        .correct-feedback {
            color: #4CAF50;
        }
        
        .wrong-feedback {
            color: #F44336;
        }
        
        /* 模态框样式 */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 100;
            justify-content: center;
            align-items: center;
        }
        
        .modal-content {
            background-color: white;
            padding: 30px;
            border-radius: 20px;
            text-align: center;
            max-width: 500px;
            width: 90%;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            animation: popIn 0.5s;
        }
        
        @keyframes popIn {
            0% { transform: scale(0.5); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }
        
        .modal h2 {
            font-size: 32px;
            margin-bottom: 20px;
            color: #4facfe;
        }
        
        .modal p {
            font-size: 20px;
            margin-bottom: 20px;
            line-height: 1.5;
        }
        
        .modal-btn {
            padding: 12px 30px;
            background: linear-gradient(to right, #4facfe, #00f2fe);
            border: none;
            border-radius: 50px;
            color: white;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .modal-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
        }
        
        .success-modal {
            background: linear-gradient(135deg, #a8e6cf, #dcedc1);
        }
        
        .encourage-modal {
            background: linear-gradient(135deg, #ffd3b6, #ffaaa5);
        }
        
        .modal-icon {
            font-size: 60px;
            margin-bottom: 20px;
        }
        
        @media (max-width: 600px) {
            .options {
                grid-template-columns: 1fr;
            }
            
            .question {
                font-size: 36px;
            }
            
            .pinyin-question {
                font-size: 32px;
            }
            
            .hanzi-question {
                font-size: 48px;
            }
            
            .mode-selection {
                flex-direction: column;
                gap: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>二年级下学期识字游戏</h1>
            <p>根据拼音识字 · 根据汉字认识拼音</p>
        </div>
        
        <div class="content">
            <div class="mode-selection">
                <button class="mode-btn pinyin active">拼音识字</button>
                <button class="mode-btn hanzi">汉字识拼音</button>
            </div>
            
            <div class="game-area">
                <div class="question" id="question">?</div>
                <div class="options" id="options">
                    <!-- 选项将通过JavaScript动态生成 -->
                </div>
                <div class="feedback" id="feedback"></div>
            </div>
            
            <div class="progress-bar">
                <div class="progress" id="progress"></div>
            </div>
            
            <div class="controls">
                <div class="level-info" id="level-info">第1关</div>
                <button class="next-btn" id="next-btn" disabled>下一题</button>
                <div class="score" id="score">得分: 0</div>
            </div>
        </div>
    </div>

    <!-- 成功模态框 -->
    <div class="modal" id="success-modal">
        <div class="modal-content success-modal">
            <div class="modal-icon">🎉</div>
            <h2>太棒了！</h2>
            <p>恭喜你成功完成第<span id="success-level">5</span>关！全部答对，真是太厉害了！</p>
            <button class="modal-btn" id="success-continue-btn">继续挑战</button>
        </div>
    </div>

    <!-- 鼓励模态框 -->
    <div class="modal" id="encourage-modal">
        <div class="modal-content encourage-modal">
            <div class="modal-icon">🌟</div>
            <h2>完成第<span id="encourage-level">1</span>关！</h2>
            <p id="encourage-text">你真棒！继续加油，下一关会更精彩！</p>
            <button class="modal-btn" id="encourage-continue-btn">继续挑战</button>
        </div>
    </div>

    <!-- 继续加油模态框 -->
    <div class="modal" id="try-harder-modal">
        <div class="modal-content">
            <div class="modal-icon">💪</div>
            <h2>继续加油！</h2>
            <p>第<span id="try-harder-level">5</span>关没有全部答对，再接再厉，相信你下次一定能成功！</p>
            <button class="modal-btn" id="try-harder-continue-btn">继续挑战</button>
        </div>
    </div>

    <script>
        // 部编版二年级下学期语文教材生字表（完整版）
        const wordDatabase = [
            // 第一单元
            { hanzi: "诗", pinyin: "shī" },
            { hanzi: "村", pinyin: "cūn" },
            { hanzi: "童", pinyin: "tóng" },
            { hanzi: "碧", pinyin: "bì" },
            { hanzi: "妆", pinyin: "zhuāng" },
            { hanzi: "绿", pinyin: "lǜ" },
            { hanzi: "丝", pinyin: "sī" },
            { hanzi: "剪", pinyin: "jiǎn" },
            { hanzi: "冲", pinyin: "chōng" },
            { hanzi: "寻", pinyin: "xún" },
            { hanzi: "姑", pinyin: "gū" },
            { hanzi: "娘", pinyin: "niáng" },
            { hanzi: "吐", pinyin: "tǔ" },
            { hanzi: "柳", pinyin: "liǔ" },
            { hanzi: "荡", pinyin: "dàng" },
            { hanzi: "桃", pinyin: "táo" },
            { hanzi: "杏", pinyin: "xìng" },
            { hanzi: "鲜", pinyin: "xiān" },
            { hanzi: "邮", pinyin: "yóu" },
            { hanzi: "递", pinyin: "dì" },
            
            // 第二单元
            { hanzi: "邓", pinyin: "dèng" },
            { hanzi: "植", pinyin: "zhí" },
            { hanzi: "格", pinyin: "gé" },
            { hanzi: "引", pinyin: "yǐn" },
            { hanzi: "注", pinyin: "zhù" },
            { hanzi: "满", pinyin: "mǎn" },
            { hanzi: "休", pinyin: "xiū" },
            { hanzi: "息", pinyin: "xī" },
            { hanzi: "锋", pinyin: "fēng" },
            { hanzi: "昨", pinyin: "zuó" },
            { hanzi: "冒", pinyin: "mào" },
            { hanzi: "留", pinyin: "liú" },
            { hanzi: "弯", pinyin: "wān" },
            { hanzi: "背", pinyin: "bēi" },
            { hanzi: "洒", pinyin: "sǎ" },
            { hanzi: "温", pinyin: "wēn" },
            { hanzi: "暖", pinyin: "nuǎn" },
            { hanzi: "能", pinyin: "néng" },
            { hanzi: "桌", pinyin: "zhuō" },
            { hanzi: "味", pinyin: "wèi" },
            
            // 第三单元
            { hanzi: "州", pinyin: "zhōu" },
            { hanzi: "湾", pinyin: "wān" },
            { hanzi: "岛", pinyin: "dǎo" },
            { hanzi: "峡", pinyin: "xiá" },
            { hanzi: "民", pinyin: "mín" },
            { hanzi: "族", pinyin: "zú" },
            { hanzi: "谊", pinyin: "yì" },
            { hanzi: "齐", pinyin: "qí" },
            { hanzi: "奋", pinyin: "fèn" },
            { hanzi: "贴", pinyin: "tiē" },
            { hanzi: "街", pinyin: "jiē" },
            { hanzi: "舟", pinyin: "zhōu" },
            { hanzi: "艾", pinyin: "ài" },
            { hanzi: "敬", pinyin: "jìng" },
            { hanzi: "转", pinyin: "zhuǎn" },
            { hanzi: "团", pinyin: "tuán" },
            { hanzi: "热", pinyin: "rè" },
            { hanzi: "闹", pinyin: "nào" },
            { hanzi: "贝", pinyin: "bèi" },
            { hanzi: "壳", pinyin: "ké" },
            
            // 第四单元
            { hanzi: "彩", pinyin: "cǎi" },
            { hanzi: "梦", pinyin: "mèng" },
            { hanzi: "森", pinyin: "sēn" },
            { hanzi: "拉", pinyin: "lā" },
            { hanzi: "结", pinyin: "jié" },
            { hanzi: "苹", pinyin: "píng" },
            { hanzi: "般", pinyin: "bān" },
            { hanzi: "精", pinyin: "jīng" },
            { hanzi: "灵", pinyin: "líng" },
            { hanzi: "伞", pinyin: "sǎn" },
            { hanzi: "姨", pinyin: "yí" },
            { hanzi: "弟", pinyin: "dì" },
            { hanzi: "便", pinyin: "biàn" },
            { hanzi: "教", pinyin: "jiāo" },
            { hanzi: "游", pinyin: "yóu" },
            { hanzi: "戏", pinyin: "xì" },
            { hanzi: "母", pinyin: "mǔ" },
            { hanzi: "周", pinyin: "zhōu" },
            { hanzi: "围", pinyin: "wéi" },
            { hanzi: "句", pinyin: "jù" },
            
            // 第五单元
            { hanzi: "亡", pinyin: "wáng" },
            { hanzi: "牢", pinyin: "láo" },
            { hanzi: "钻", pinyin: "zuān" },
            { hanzi: "劝", pinyin: "quàn" },
            { hanzi: "丢", pinyin: "diū" },
            { hanzi: "告", pinyin: "gào" },
            { hanzi: "筋", pinyin: "jīn" },
            { hanzi: "疲", pinyin: "pí" },
            { hanzi: "图", pinyin: "tú" },
            { hanzi: "课", pinyin: "kè" },
            { hanzi: "摆", pinyin: "bǎi" },
            { hanzi: "座", pinyin: "zuò" },
            { hanzi: "交", pinyin: "jiāo" },
            { hanzi: "哈", pinyin: "hā" },
            { hanzi: "页", pinyin: "yè" },
            { hanzi: "抢", pinyin: "qiǎng" },
            { hanzi: "嘻", pinyin: "xī" },
            { hanzi: "愿", pinyin: "yuàn" },
            { hanzi: "意", pinyin: "yì" },
            { hanzi: "麦", pinyin: "mài" },
            
            // 第六单元
            { hanzi: "湖", pinyin: "hú" },
            { hanzi: "莲", pinyin: "lián" },
            { hanzi: "穷", pinyin: "qióng" },
            { hanzi: "荷", pinyin: "hé" },
            { hanzi: "绝", pinyin: "jué" },
            { hanzi: "含", pinyin: "hán" },
            { hanzi: "岭", pinyin: "lǐng" },
            { hanzi: "吴", pinyin: "wú" },
            { hanzi: "雷", pinyin: "léi" },
            { hanzi: "乌", pinyin: "wū" },
            { hanzi: "黑", pinyin: "hēi" },
            { hanzi: "压", pinyin: "yā" },
            { hanzi: "垂", pinyin: "chuí" },
            { hanzi: "户", pinyin: "hù" },
            { hanzi: "迎", pinyin: "yíng" },
            { hanzi: "扑", pinyin: "pū" },
            { hanzi: "指", pinyin: "zhǐ" },
            { hanzi: "针", pinyin: "zhēn" },
            { hanzi: "帮", pinyin: "bāng" },
            { hanzi: "助", pinyin: "zhù" },
            
            // 第七单元
            { hanzi: "扇", pinyin: "shàn" },
            { hanzi: "慢", pinyin: "màn" },
            { hanzi: "遇", pinyin: "yù" },
            { hanzi: "兔", pinyin: "tù" },
            { hanzi: "安", pinyin: "ān" },
            { hanzi: "根", pinyin: "gēn" },
            { hanzi: "痛", pinyin: "tòng" },
            { hanzi: "最", pinyin: "zuì" },
            { hanzi: "店", pinyin: "diàn" },
            { hanzi: "决", pinyin: "jué" },
            { hanzi: "定", pinyin: "dìng" },
            { hanzi: "商", pinyin: "shāng" },
            { hanzi: "夫", pinyin: "fū" },
            { hanzi: "终", pinyin: "zhōng" },
            { hanzi: "完", pinyin: "wán" },
            { hanzi: "换", pinyin: "huàn" },
            { hanzi: "期", pinyin: "qī" },
            { hanzi: "蛙", pinyin: "wā" },
            { hanzi: "卖", pinyin: "mài" },
            { hanzi: "搬", pinyin: "bān" },
            
            // 第八单元
            { hanzi: "祖", pinyin: "zǔ" },
            { hanzi: "啊", pinyin: "a" },
            { hanzi: "浓", pinyin: "nóng" },
            { hanzi: "望", pinyin: "wàng" },
            { hanzi: "蓝", pinyin: "lán" },
            { hanzi: "摘", pinyin: "zhāi" },
            { hanzi: "掏", pinyin: "tāo" },
            { hanzi: "赛", pinyin: "sài" },
            { hanzi: "忆", pinyin: "yì" },
            { hanzi: "乎", pinyin: "hū" },
            { hanzi: "农", pinyin: "nóng" },
            { hanzi: "糙", pinyin: "cāo" },
            { hanzi: "敏", pinyin: "mǐn" },
            { hanzi: "遮", pinyin: "zhē" },
            { hanzi: "胆", pinyin: "dǎn" },
            { hanzi: "量", pinyin: "liàng" },
            { hanzi: "具", pinyin: "jù" },
            { hanzi: "组", pinyin: "zǔ" },
            { hanzi: "育", pinyin: "yù" },
            { hanzi: "类", pinyin: "lèi" }
        ];

        // 鼓励话语库
        const encouragementMessages = [
            "你真棒！继续加油，下一关会更精彩！",
            "太厉害了！你的识字能力真强！",
            "做得好！继续保持这个状态！",
            "真聪明！你已经掌握了很多汉字！",
            "太出色了！你是个识字小能手！",
            "真了不起！你的进步很明显！",
            "太棒了！你的努力得到了回报！",
            "真厉害！继续挑战更高难度吧！",
            "做得好！你的语文水平越来越高了！",
            "太优秀了！你真是个学习小天才！"
        ];

        // 游戏状态
        let gameState = {
            mode: 'pinyin', // 默认模式：拼音识字
            currentLevel: 1,
            currentQuestion: 0,
            totalQuestions: 10,
            score: 0,
            currentWord: null,
            options: [],
            answered: false,
            levelScore: 0 // 当前关卡得分
        };

        // DOM元素
        const modeButtons = document.querySelectorAll('.mode-btn');
        const questionElement = document.getElementById('question');
        const optionsElement = document.getElementById('options');
        const nextButton = document.getElementById('next-btn');
        const levelInfoElement = document.getElementById('level-info');
        const scoreElement = document.getElementById('score');
        const progressElement = document.getElementById('progress');
        const feedbackElement = document.getElementById('feedback');
        
        // 模态框元素
        const successModal = document.getElementById('success-modal');
        const encourageModal = document.getElementById('encourage-modal');
        const tryHarderModal = document.getElementById('try-harder-modal');
        const successLevelElement = document.getElementById('success-level');
        const encourageLevelElement = document.getElementById('encourage-level');
        const encourageTextElement = document.getElementById('encourage-text');
        const tryHarderLevelElement = document.getElementById('try-harder-level');
        const successContinueBtn = document.getElementById('success-continue-btn');
        const encourageContinueBtn = document.getElementById('encourage-continue-btn');
        const tryHarderContinueBtn = document.getElementById('try-harder-continue-btn');

        // 初始化游戏
        function initGame() {
            updateLevelInfo();
            generateQuestion();
            updateScore();
            updateProgress();
            
            // 添加模式切换事件
            modeButtons.forEach(button => {
                button.addEventListener('click', function() {
                    modeButtons.forEach(btn => btn.classList.remove('active'));
                    this.classList.add('active');
                    gameState.mode = this.classList.contains('pinyin') ? 'pinyin' : 'hanzi';
                    resetGame();
                });
            });
            
            // 添加下一题按钮事件
            nextButton.addEventListener('click', function() {
                if (gameState.currentQuestion < gameState.totalQuestions) {
                    gameState.currentQuestion++;
                    generateQuestion();
                    updateProgress();
                    nextButton.disabled = true;
                    feedbackElement.textContent = '';
                    feedbackElement.className = 'feedback';
                } else {
                    // 完成当前关卡
                    checkLevelCompletion();
                }
            });
            
            // 添加模态框继续按钮事件
            successContinueBtn.addEventListener('click', function() {
                successModal.style.display = 'none';
                continueToNextLevel();
            });
            
            encourageContinueBtn.addEventListener('click', function() {
                encourageModal.style.display = 'none';
                continueToNextLevel();
            });
            
            tryHarderContinueBtn.addEventListener('click', function() {
                tryHarderModal.style.display = 'none';
                continueToNextLevel();
            });
        }

        // 检查关卡完成情况
        function checkLevelCompletion() {
            // 计算当前关卡得分百分比
            const levelPercentage = (gameState.levelScore / gameState.totalQuestions) * 100;
            
            // 如果是第5关并且全部答对
            if (gameState.currentLevel === 5 && levelPercentage === 100) {
                showSuccessModal();
                playSuccessSound();
            } 
            // 如果是第5关但没有全部答对
            else if (gameState.currentLevel === 5 && levelPercentage < 100) {
                showTryHarderModal();
                playTryHarderSound();
            }
            // 其他关卡
            else {
                showEncourageModal();
                playEncourageSound();
            }
        }

        // 显示成功模态框
        function showSuccessModal() {
            successLevelElement.textContent = gameState.currentLevel;
            successModal.style.display = 'flex';
        }

        // 显示鼓励模态框
        function showEncourageModal() {
            encourageLevelElement.textContent = gameState.currentLevel;
            // 随机选择一条鼓励话语
            const randomIndex = Math.floor(Math.random() * encouragementMessages.length);
            encourageTextElement.textContent = encouragementMessages[randomIndex];
            encourageModal.style.display = 'flex';
        }

        // 显示继续加油模态框
        function showTryHarderModal() {
            tryHarderLevelElement.textContent = gameState.currentLevel;
            tryHarderModal.style.display = 'flex';
        }

        // 继续到下一关
        function continueToNextLevel() {
            if (gameState.currentLevel < 10) {
                gameState.currentLevel++;
                gameState.currentQuestion = 0;
                gameState.levelScore = 0;
                gameState.totalQuestions = Math.min(10, gameState.currentLevel * 2);
                updateLevelInfo();
                generateQuestion();
                updateProgress();
            } else {
                // 游戏通关
                alert(`恭喜你！你已经完成了所有关卡！最终得分：${gameState.score}`);
                resetGame();
            }
        }

        // 播放成功音效
        function playSuccessSound() {
            // 创建成功音效
            const audioContext = new (window.AudioContext || window.webkitAudioContext)();
            const oscillator = audioContext.createOscillator();
            const gainNode = audioContext.createGain();
            
            oscillator.connect(gainNode);
            gainNode.connect(audioContext.destination);
            
            oscillator.type = 'sine';
            oscillator.frequency.setValueAtTime(523.25, audioContext.currentTime); // C5
            oscillator.frequency.setValueAtTime(659.25, audioContext.currentTime + 0.1); // E5
            oscillator.frequency.setValueAtTime(783.99, audioContext.currentTime + 0.2); // G5
            
            gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
            gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.5);
            
            oscillator.start(audioContext.currentTime);
            oscillator.stop(audioContext.currentTime + 0.5);
        }

        // 播放鼓励音效
        function playEncourageSound() {
            // 创建鼓励音效
            const audioContext = new (window.AudioContext || window.webkitAudioContext)();
            const oscillator = audioContext.createOscillator();
            const gainNode = audioContext.createGain();
            
            oscillator.connect(gainNode);
            gainNode.connect(audioContext.destination);
            
            oscillator.type = 'sine';
            oscillator.frequency.setValueAtTime(392.00, audioContext.currentTime); // G4
            oscillator.frequency.setValueAtTime(523.25, audioContext.currentTime + 0.2); // C5
            
            gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
            gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.4);
            
            oscillator.start(audioContext.currentTime);
            oscillator.stop(audioContext.currentTime + 0.4);
        }

        // 播放继续加油音效
        function playTryHarderSound() {
            // 创建继续加油音效
            const audioContext = new (window.AudioContext || window.webkitAudioContext)();
            const oscillator = audioContext.createOscillator();
            const gainNode = audioContext.createGain();
            
            oscillator.connect(gainNode);
            gainNode.connect(audioContext.destination);
            
            oscillator.type = 'sine';
            oscillator.frequency.setValueAtTime(261.63, audioContext.currentTime); // C4
            oscillator.frequency.setValueAtTime(220.00, audioContext.currentTime + 0.1); // A3
            oscillator.frequency.setValueAtTime(196.00, audioContext.currentTime + 0.2); // G3
            
            gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
            gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.3);
            
            oscillator.start(audioContext.currentTime);
            oscillator.stop(audioContext.currentTime + 0.3);
        }

        // 更新关卡信息
        function updateLevelInfo() {
            levelInfoElement.textContent = `第${gameState.currentLevel}关`;
        }

        // 更新分数
        function updateScore() {
            scoreElement.textContent = `得分: ${gameState.score}`;
        }

        // 更新进度条
        function updateProgress() {
            const progress = (gameState.currentQuestion / gameState.totalQuestions) * 100;
            progressElement.style.width = `${progress}%`;
        }

        // 生成问题
        function generateQuestion() {
            gameState.answered = false;
            
            // 随机选择一个字
            const randomIndex = Math.floor(Math.random() * wordDatabase.length);
            gameState.currentWord = wordDatabase[randomIndex];
            
            // 生成干扰选项
            gameState.options = generateOptions(gameState.currentWord, wordDatabase);
            
            // 显示问题
            if (gameState.mode === 'pinyin') {
                questionElement.textContent = gameState.currentWord.pinyin;
                questionElement.className = "question pinyin-question";
            } else {
                questionElement.textContent = gameState.currentWord.hanzi;
                questionElement.className = "question hanzi-question";
            }
            
            // 显示选项
            displayOptions();
        }

        // 生成选项
        function generateOptions(correctWord, wordPool) {
            const options = [correctWord];
            
            // 随机选择3个不同的干扰项
            while (options.length < 4) {
                const randomIndex = Math.floor(Math.random() * wordPool.length);
                const randomWord = wordPool[randomIndex];
                
                // 确保不重复
                if (!options.some(option => 
                    (gameState.mode === 'pinyin' && option.hanzi === randomWord.hanzi) ||
                    (gameState.mode === 'hanzi' && option.pinyin === randomWord.pinyin)
                )) {
                    options.push(randomWord);
                }
            }
            
            // 随机排序选项
            return shuffleArray(options);
        }

        // 打乱数组顺序
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // 显示选项
        function displayOptions() {
            optionsElement.innerHTML = '';
            
            gameState.options.forEach(option => {
                const optionElement = document.createElement('div');
                optionElement.className = 'option';
                
                if (gameState.mode === 'pinyin') {
                    optionElement.textContent = option.hanzi;
                } else {
                    optionElement.textContent = option.pinyin;
                }
                
                optionElement.addEventListener('click', function() {
                    if (!gameState.answered) {
                        checkAnswer(option);
                    }
                });
                
                optionsElement.appendChild(optionElement);
            });
        }

        // 检查答案
        function checkAnswer(selectedOption) {
            gameState.answered = true;
            
            const isCorrect = 
                (gameState.mode === 'pinyin' && selectedOption.hanzi === gameState.currentWord.hanzi) ||
                (gameState.mode === 'hanzi' && selectedOption.pinyin === gameState.currentWord.pinyin);
            
            // 更新选项样式
            const optionElements = document.querySelectorAll('.option');
            optionElements.forEach(element => {
                const elementValue = element.textContent;
                const isThisCorrect = 
                    (gameState.mode === 'pinyin' && elementValue === gameState.currentWord.hanzi) ||
                    (gameState.mode === 'hanzi' && elementValue === gameState.currentWord.pinyin);
                
                if (isThisCorrect) {
                    element.classList.add('correct');
                } else if (elementValue === selectedOption[gameState.mode === 'pinyin' ? 'hanzi' : 'pinyin']) {
                    element.classList.add('wrong');
                }
            });
            
            // 更新分数和反馈
            if (isCorrect) {
                gameState.score += 10;
                gameState.levelScore++;
                feedbackElement.textContent = '回答正确！';
                feedbackElement.className = 'feedback correct-feedback';
            } else {
                feedbackElement.textContent = `回答错误！正确答案是：${
                    gameState.mode === 'pinyin' ? gameState.currentWord.hanzi : gameState.currentWord.pinyin
                }`;
                feedbackElement.className = 'feedback wrong-feedback';
            }
            
            updateScore();
            nextButton.disabled = false;
        }

        // 重置游戏
        function resetGame() {
            gameState.currentLevel = 1;
            gameState.currentQuestion = 0;
            gameState.totalQuestions = 10;
            gameState.score = 0;
            gameState.levelScore = 0;
            updateLevelInfo();
            updateScore();
            generateQuestion();
            updateProgress();
            nextButton.disabled = true;
            feedbackElement.textContent = '';
            feedbackElement.className = 'feedback';
        }

        // 初始化游戏
        window.onload = initGame;
    </script>
</body>
</html>
