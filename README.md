# report3
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>七美德量表（短版）- 中文测试</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
            background: #f0f2f5;
            color: #1a1a1a;
            line-height: 1.6;
            min-height: 100vh;
            padding: 20px 16px;
        }
        .container {
            max-width: 640px;
            margin: 0 auto;
        }
        .card {
            background: #fff;
            border-radius: 16px;
            box-shadow: 0 2px 12px rgba(0,0,0,0.08);
            padding: 32px 24px;
        }
        .btn {
            display: inline-block;
            padding: 12px 32px;
            border-radius: 10px;
            border: none;
            font-size: 15px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            text-align: center;
        }
        .btn-primary {
            background: #4a90d9;
            color: #fff;
        }
        .btn-primary:hover { background: #3a7bc8; }
        .btn-outline {
            background: #fff;
            color: #666;
            border: 1px solid #ddd;
        }
        .btn-outline:hover { background: #f5f5f5; }
        .option-btn {
            width: 100%;
            text-align: left;
            padding: 14px 18px;
            border-radius: 10px;
            border: 2px solid #e5e7eb;
            background: #fff;
            color: #333;
            cursor: pointer;
            font-size: 15px;
            font-weight: 500;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 10px;
        }
        .option-btn:hover { border-color: #b0c4de; background: #f8fafc; }
        .option-btn.selected {
            border-color: #4a90d9;
            background: #f0f7ff;
            color: #4a90d9;
        }
        .option-num {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            width: 28px;
            height: 28px;
            border-radius: 50%;
            border: 2px solid #ccc;
            background: #fff;
            color: #666;
            font-size: 13px;
            font-weight: 700;
            flex-shrink: 0;
        }
        .option-btn.selected .option-num {
            border-color: #4a90d9;
            background: #4a90d9;
            color: #fff;
        }
        .progress-bar {
            background: #e8f0fe;
            height: 6px;
            border-radius: 3px;
            overflow: hidden;
            margin-bottom: 28px;
        }
        .progress-fill {
            background: #4a90d9;
            height: 100%;
            border-radius: 3px;
            transition: width 0.3s ease;
        }
        .virtue-tag {
            display: inline-block;
            background: #f0f0f0;
            color: #888;
            font-size: 12px;
            padding: 4px 12px;
            border-radius: 20px;
            font-weight: 500;
            margin-bottom: 10px;
        }
        .score-row {
            background: #f8f9fa;
            border-radius: 12px;
            padding: 16px 20px;
            margin-bottom: 12px;
        }
        .score-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 8px;
        }
        .score-bar-bg {
            background: #e5e7eb;
            height: 8px;
            border-radius: 4px;
            overflow: hidden;
        }
        .score-bar-fill {
            height: 100%;
            border-radius: 4px;
            transition: width 0.8s ease;
        }
        .info-box {
            background: #fff8e1;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 24px;
            font-size: 14px;
            color: #555;
            line-height: 1.6;
        }
        .info-box strong { color: #333; }
        .warning-box {
            background: #ffebee;
            border-radius: 12px;
            padding: 16px 20px;
            margin-bottom: 20px;
            font-size: 14px;
            color: #c62828;
        }
        @media (max-width: 480px) {
            body { padding: 12px 10px; }
            .card { padding: 24px 16px; }
        }
    </style>
<base target="_blank">
</head>
<body>
    <div class="container" id="app"></div>

    <script>
        const questions = [
            { id: 1, virtue: "faith", text: "相信上帝使我的生命有意义。" },
            { id: 2, virtue: "hope", text: "我热切期待为我预备的美好事物。" },
            { id: 3, virtue: "love", text: "帮助和服务他人对我来说非常重要。" },
            { id: 4, virtue: "justice", text: "我认为自己是一个坚定不移地追求正义的人。" },
            { id: 5, virtue: "courage", text: "我不会因为害怕而阻止自己做正确的事。" },
            { id: 6, virtue: "temperance", text: "我认为自己是一个始终避免极端的人。" },
            { id: 7, virtue: "wisdom", text: "我在决定追求什么目标时，会思考什么是最重要的。" },
            { id: 8, virtue: "faith", text: "对上帝的信任是我生命中的力量源泉。" },
            { id: 9, virtue: "hope", text: "我对摆在我面前的未来保持希望。" },
            { id: 10, virtue: "love", text: "同理心常常激励我在他人挣扎时伸出援手。" },
            { id: 11, virtue: "justice", text: "我积极反对周围看到的不公正现象。" },
            { id: 12, virtue: "courage", text: "我勇敢地走出舒适区去做正确的事。" },
            { id: 13, virtue: "temperance", text: "我努力过有节制的生活，避免极端。" },
            { id: 14, virtue: "wisdom", text: "我寻找向他人学习和成长的机会。" },
            { id: 15, virtue: "faith", text: "我强烈相信上帝的良善。" },
            { id: 16, virtue: "hope", text: "我紧紧抓住事情最终会被纠正的期望。" },
            { id: 17, virtue: "love", text: "我对那些正在受苦的人怀有深切的同情。" },
            { id: 18, virtue: "justice", text: "我捍卫所有人群的权利和尊严。" },
            { id: 19, virtue: "courage", text: "我总是直面恐惧，而不是逃避它们。" },
            { id: 20, virtue: "temperance", text: "通过自律，我避免屈服于可能使我偏离长期计划的诱惑。" },
            { id: 21, virtue: "wisdom", text: "我经常反思如何最好地践行我的价值观。" },
            { id: 22, virtue: "faith", text: "信靠上帝给了我人生目标。" },
            { id: 23, virtue: "hope", text: "我能够在许多不同的环境中保持坚定的希望。" },
            { id: 24, virtue: "love", text: "我努力成为一个坚定不移地付出爱的人。" },
            { id: 25, virtue: "justice", text: "我经常为那些不被尊重的人发声。" },
            { id: 26, virtue: "courage", text: "即使需要冒险，我也会追求我的呼召。" },
            { id: 27, virtue: "temperance", text: "我谨慎行事，不在言语或行为上冲动。" },
            { id: 28, virtue: "wisdom", text: "我通常在接受一个观点之前会权衡多个角度。" },
            { id: 29, virtue: "faith", text: "我寻求深刻地认识上帝。" },
            { id: 30, virtue: "hope", text: "当事情艰难时，我能够找到超越自身的力量继续前行。" },
            { id: 31, virtue: "love", text: "即使与他人意见不合，我也会对他们友善。" },
            { id: 32, virtue: "justice", text: "我渴望看到人们从压迫的处境中得释放。" },
            { id: 33, virtue: "courage", text: "我愿意拥抱不适，以便在世界上行善。" },
            { id: 34, virtue: "temperance", text: "我在许多情况下（工作、人际关系、健康）都锻炼自我克制。" },
            { id: 35, virtue: "wisdom", text: "我欢迎关于我弱点的反馈。" }
        ];

        const options = [
            { value: 0, label: "完全不像我" },
            { value: 1, label: "有一点像我" },
            { value: 2, label: "有些像我" },
            { value: 3, label: "很像我" },
            { value: 4, label: "完全像我" }
        ];

        const virtueNames = {
            faith: "信德 (Faith)",
            hope: "望德 (Hope)",
            love: "爱德 (Love)",
            justice: "正义 (Justice)",
            courage: "勇气 (Courage)",
            temperance: "节制 (Temperance)",
            wisdom: "智慧 (Wisdom)"
        };

        const virtueItems = {
            faith: [1, 8, 15, 22, 29],
            hope: [2, 9, 16, 23, 30],
            love: [3, 10, 17, 24, 31],
            justice: [4, 11, 18, 25, 32],
            courage: [5, 12, 19, 26, 33],
            temperance: [6, 13, 20, 27, 34],
            wisdom: [7, 14, 21, 28, 35]
        };

        let currentPage = 0;
        const answers = {};

        function render() {
            const app = document.getElementById('app');
            if (currentPage === 0) {
                app.innerHTML = renderIntro();
            } else if (currentPage <= questions.length) {
                app.innerHTML = renderQuestion(currentPage - 1);
            } else {
                app.innerHTML = renderResults();
            }
        }

        function renderIntro() {
            return `
                <div class="card" style="text-align: center; padding: 48px 24px;">
                    <div style="font-size: 56px; margin-bottom: 16px;">✨</div>
                    <h1 style="font-size: 28px; font-weight: 700; color: #1a1a1a; margin-bottom: 12px;">七美德量表（短版）</h1>
                    <p style="font-size: 16px; color: #666; line-height: 1.6; margin-bottom: 32px;">
                        本测试包含 35 道题目，评估你在七个核心美德维度上的水平：<br>
                        <span style="color: #4a90d9; font-weight: 600;">信德、望德、爱德、正义、勇气、节制、智慧</span>
                    </p>
                    <div style="background: #f5f7fa; border-radius: 12px; padding: 20px; margin-bottom: 32px; text-align: left;">
                        <p style="font-size: 14px; color: #555; margin-bottom: 8px; font-weight: 600;">📋 说明：</p>
                        <p style="font-size: 14px; color: #666; line-height: 1.6;">
                            请根据你<span style="color: #d94a4a; font-weight: 600;">通常的状态</span>（而非你认为应该成为的样子）诚实作答。<br>
                            对于提到"上帝"的题目，你可以将其理解为符合你信仰或经验的高等力量。如果某条陈述与你的信仰或经验完全不符，请选择"完全不像我"。
                        </p>
                    </div>
                    <button onclick="startTest()" class="btn btn-primary" style="font-size: 16px; padding: 14px 48px;">开始测试</button>
                </div>
            `;
        }

        function renderQuestion(index) {
            const q = questions[index];
            const progress = ((index + 1) / questions.length * 100).toFixed(0);
            const hasAnswer = answers[q.id] !== undefined;
            return `
                <div class="card">
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 16px;">
                        <span style="font-size: 13px; color: #999; font-weight: 500;">第 ${index + 1} / ${questions.length} 题</span>
                        <span style="font-size: 13px; color: #4a90d9; font-weight: 600;">${progress}%</span>
                    </div>
                    <div class="progress-bar">
                        <div class="progress-fill" style="width: ${progress}%;"></div>
                    </div>
                    <div>
                        <span class="virtue-tag">${virtueNames[q.virtue]}</span>
                    </div>
                    <h2 style="font-size: 20px; font-weight: 600; color: #1a1a1a; margin-bottom: 28px; line-height: 1.5;">${q.text}</h2>
                    <div>
                        ${options.map(opt => `
                            <button onclick="selectAnswer(${q.id}, ${opt.value})" 
                                class="option-btn ${answers[q.id] === opt.value ? 'selected' : ''}">
                                <span class="option-num">${opt.value}</span>
                                ${opt.label}
                            </button>
                        `).join('')}
                    </div>
                    <div style="display: flex; justify-content: space-between; margin-top: 28px;">
                        <button onclick="prevQuestion()" class="btn btn-outline" style="font-size: 14px; ${index === 0 ? 'visibility: hidden;' : ''}">上一题</button>
                        <button onclick="nextQuestion()" class="btn btn-primary" style="font-size: 14px; background: ${hasAnswer ? '#4a90d9' : '#ccc'}; cursor: ${hasAnswer ? 'pointer' : 'not-allowed'};">
                            ${index === questions.length - 1 ? '查看结果' : '下一题'}
                        </button>
                    </div>
                </div>
            `;
        }

        function renderResults() {
            const scores = {};
            let answeredCount = 0;
            for (const [virtue, items] of Object.entries(virtueItems)) {
                let sum = 0;
                let count = 0;
                items.forEach(id => {
                    if (answers[id] !== undefined) {
                        sum += answers[id];
                        count++;
                    }
                });
                answeredCount = Math.max(answeredCount, count > 0 ? items.length : 0);
                scores[virtue] = count > 0 ? sum / count : 0;
            }

            const totalAnswered = Object.keys(answers).length;
            const allAnswered = totalAnswered === questions.length;

            const sorted = Object.entries(scores).sort((a, b) => b[1] - a[1]);
            const maxScore = 4;

            return `
                <div class="card">
                    <div style="text-align: center; margin-bottom: 32px;">
                        <div style="font-size: 48px; margin-bottom: 12px;">📊</div>
                        <h1 style="font-size: 24px; font-weight: 700; color: #1a1a1a; margin-bottom: 8px;">测试结果</h1>
                        <p style="font-size: 14px; color: #888;">七美德量表（短版）评分</p>
                        <p style="font-size: 13px; color: #999; margin-top: 6px;">已作答 ${totalAnswered} / ${questions.length} 题</p>
                    </div>

                    ${!allAnswered ? `
                        <div class="warning-box">
                            ⚠️ 你还有 ${questions.length - totalAnswered} 道题未作答，未作答的题目按 0 分计算。建议返回补答以获得更准确的结果。
                        </div>
                    ` : ''}

                    <div style="margin-bottom: 32px;">
                        ${sorted.map(([virtue, score]) => {
                            const pct = (score / maxScore * 100).toFixed(0);
                            const color = pct >= 75 ? '#4caf50' : pct >= 50 ? '#ff9800' : '#f44336';
                            return `
                                <div class="score-row">
                                    <div class="score-header">
                                        <span style="font-size: 15px; font-weight: 600; color: #333;">${virtueNames[virtue]}</span>
                                        <span style="font-size: 18px; font-weight: 700; color: ${color};">${score.toFixed(2)} <span style="font-size: 13px; color: #999;">/ 4.00</span></span>
                                    </div>
                                    <div class="score-bar-bg">
                                        <div class="score-bar-fill" style="background: ${color}; width: ${pct}%;"></div>
                                    </div>
                                </div>
                            `;
                        }).join('')}
                    </div>

                    <div class="info-box">
                        <strong>💡 解读：</strong><br>
                        每个维度的得分范围为 0–4 分。分数越高，表示你在该美德维度上的典型表现越强。<br><br>
                        你的最高维度是 <strong style="color: #4a90d9;">${virtueNames[sorted[0][0]]}</strong>（${sorted[0][1].toFixed(2)} 分），
                        最低维度是 <strong style="color: #d94a4a;">${virtueNames[sorted[6][0]]}</strong>（${sorted[6][1].toFixed(2)} 分）。
                    </div>

                    <div style="text-align: center;">
                        <button onclick="restartTest()" class="btn btn-primary" style="padding: 12px 36px;">重新测试</button>
                    </div>
                </div>
            `;
        }

        function startTest() {
            currentPage = 1;
            render();
        }

        function selectAnswer(id, value) {
            answers[id] = value;
            render();
            setTimeout(() => {
                if (currentPage <= questions.length) {
                    currentPage++;
                    render();
                }
            }, 280);
        }

        function nextQuestion() {
            const q = questions[currentPage - 1];
            if (answers[q.id] !== undefined) {
                currentPage++;
                render();
            }
        }

        function prevQuestion() {
            if (currentPage > 1) {
                currentPage--;
                render();
            }
        }

        function restartTest() {
            currentPage = 0;
            for (let k in answers) delete answers[k];
            render();
        }

        render();
    </script>
</body>
</html>
