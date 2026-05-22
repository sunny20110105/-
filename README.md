<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>限界フリーターのもやし栽培 〜顔のある生活〜</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Kosugi+Maru&display=swap');

        body {
            font-family: 'Kosugi Maru', 'Helvetica Neue', Arial, sans-serif;
            background-color: #161616;
            color: #d1d5db;
            margin: 0;
            padding: 10px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            user-select: none;
        }
        .game-container {
            background-color: #222222;
            border-radius: 16px;
            padding: 20px;
            box-shadow: 0 12px 32px rgba(0,0,0,0.8);
            width: 100%;
            max-width: 480px;
            text-align: center;
            border: 1px solid #333333;
            position: relative;
        }
        .header-area {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
        }
        h1 {
            font-size: 1.25rem;
            margin: 0;
            color: #a7ff83;
            text-shadow: 0 0 8px rgba(167, 255, 131, 0.2);
            text-align: left;
        }
        .title-sub {
            font-size: 0.75rem;
            color: #777777;
            display: block;
            text-align: left;
            margin-top: 2px;
        }
        .sound-toggle {
            background: #333333;
            border: 1px solid #444;
            color: #888;
            padding: 6px 12px;
            font-size: 0.75rem;
            font-weight: bold;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.2s;
        }
        .sound-toggle.active {
            color: #ffd700;
            border-color: #ffd700;
            background-color: #2c2918;
        }
        
        /* イベントバナー表示 */
        .event-banner {
            background-color: #3b2a1a;
            border: 1px solid #d35400;
            color: #f39c12;
            padding: 10px;
            border-radius: 8px;
            margin-bottom: 12px;
            font-size: 0.8rem;
            font-weight: bold;
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            animation: pulse 1.5s infinite;
        }
        .event-banner-header {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            width: 100%;
        }
        .event-banner-desc {
            font-size: 0.7rem;
            margin-top: 4px;
            color: #ffd700;
            opacity: 0.95;
            font-weight: normal;
            line-height: 1.3;
        }
        @keyframes pulse {
            0% { opacity: 0.85; }
            50% { opacity: 1; }
            100% { opacity: 0.85; }
        }

        /* タブ切り替えボタン */
        .tabs {
            display: flex;
            gap: 8px;
            margin-bottom: 12px;
        }
        .tab-btn {
            flex: 1;
            background-color: #2a2a2a;
            border: 1px solid #444;
            color: #aaa;
            padding: 8px;
            font-size: 0.85rem;
            font-weight: bold;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s;
        }
        .tab-btn.active {
            background-color: #a7ff83;
            color: #121212;
            border-color: #a7ff83;
        }

        .status-panel {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            background-color: #181818;
            padding: 12px;
            border-radius: 10px;
            margin-bottom: 15px;
            border: 1px solid #282828;
        }
        .status-item {
            font-size: 0.75rem;
            color: #888888;
        }
        .status-value {
            font-size: 1.1rem;
            font-weight: bold;
            color: #ffd700;
            margin-top: 4px;
            display: block;
        }
        .status-value.water {
            color: #33b5e5;
        }
        .status-value.rank {
            color: #ff4444;
            font-size: 0.8rem;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        .canvas-container {
            position: relative;
            background-color: #0d0d0d;
            border-radius: 12px;
            overflow: hidden;
            border: 2px solid #3a3a3a;
        }
        #tray-canvas {
            display: block;
            cursor: pointer;
            touch-action: none;
            width: 100%;      
            height: auto;     
        }

        /* 独自の名前入力ダイアログポップアップ */
        .modal-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.8);
            border-radius: 16px;
            display: none;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 100;
        }
        .modal-content {
            background-color: #2a2a2a;
            border: 2px solid #444;
            border-radius: 12px;
            padding: 20px;
            width: 80%;
            max-width: 320px;
            text-align: center;
            box-shadow: 0 4px 20px rgba(0,0,0,0.5);
        }
        .modal-title {
            font-size: 0.9rem;
            color: #a7ff83;
            margin-bottom: 12px;
            font-weight: bold;
        }
        .modal-input {
            width: 100%;
            background-color: #111;
            border: 1px solid #666;
            color: #fff;
            border-radius: 6px;
            padding: 8px;
            font-size: 0.85rem;
            text-align: center;
            box-sizing: border-box;
            outline: none;
            font-family: inherit;
            margin-bottom: 15px;
        }
        .modal-input:focus {
            border-color: #a7ff83;
        }
        .modal-btns {
            display: flex;
            gap: 10px;
        }
        .modal-btn {
            flex: 1;
            padding: 8px;
            font-size: 0.8rem;
            font-weight: bold;
            border-radius: 6px;
            cursor: pointer;
            border: none;
            font-family: inherit;
        }
        .modal-btn-cancel {
            background-color: #444;
            color: #ddd;
        }
        .modal-btn-confirm {
            background-color: #a7ff83;
            color: #121212;
        }

        /* 図鑑エリア */
        .zukan-container {
            display: none;
            background-color: #181818;
            border-radius: 12px;
            border: 2px solid #3a3a3a;
            height: 300px;
            overflow-y: auto;
            padding: 10px;
            text-align: left;
        }
        .zukan-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 8px;
        }
        .zukan-item {
            background-color: #222;
            border: 1px solid #444;
            border-radius: 8px;
            padding: 10px;
            display: flex;
            align-items: center;
            gap: 12px;
            transition: all 0.2s;
        }
        .zukan-item.locked {
            opacity: 0.5;
            background-color: #151515;
            border: 1px dashed #333;
        }
        .zukan-icon-wrapper {
            width: 44px;
            height: 44px;
            border-radius: 50%;
            background-color: #0d0d0d;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 1px solid #333;
            flex-shrink: 0;
            position: relative;
            overflow: hidden;
        }
        .zukan-mame {
            width: 14px;
            height: 12px;
            border-radius: 50% 50% 40% 40%;
            position: absolute;
            top: 12px;
        }
        .zukan-stem {
            width: 4px;
            height: 20px;
            position: absolute;
            bottom: 6px;
            border-radius: 2px;
        }
        .zukan-info {
            flex-grow: 1;
        }
        .zukan-name {
            font-size: 0.85rem;
            font-weight: bold;
            color: #e0e0e0;
        }
        .zukan-item.locked .zukan-name {
            color: #555;
        }
        .zukan-desc {
            font-size: 0.7rem;
            color: #888;
            margin-top: 4px;
            line-height: 1.3;
        }
        .zukan-stats {
            font-size: 0.65rem;
            color: #999;
            margin-top: 4px;
            display: flex;
            gap: 10px;
        }
        .zukan-price {
            color: #ffd700;
        }

        .controls {
            margin-top: 15px;
            display: flex;
            gap: 10px;
            justify-content: center;
        }
        button.action-btn {
            background-color: #a7ff83;
            color: #121212;
            border: none;
            padding: 12px 18px;
            font-size: 0.9rem;
            font-weight: bold;
            font-family: 'Kosugi Maru', sans-serif;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.1s ease;
            flex: 1;
            box-shadow: 0 4px 0px #6eb850;
        }
        button.action-btn:hover {
            background-color: #baff9e;
        }
        button.action-btn:active {
            transform: translateY(3px);
            box-shadow: 0 1px 0px #6eb850;
        }
        button.action-btn:disabled {
            background-color: #444;
            color: #777;
            box-shadow: none;
            transform: none;
            cursor: not-allowed;
        }
        .log-box {
            margin-top: 12px;
            height: 40px;
            font-size: 0.75rem;
            color: #00ffcc;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: #0d0d0d;
            border-radius: 6px;
            padding: 0 10px;
            border: 1px solid #222222;
        }
        .shop-section {
            margin-top: 15px;
            text-align: left;
            background-color: #181818;
            padding: 12px;
            border-radius: 10px;
            border: 1px solid #282828;
        }
        .shop-title {
            font-size: 0.85rem;
            color: #a7ff83;
            font-weight: bold;
            margin-bottom: 8px;
            border-bottom: 1px solid #333;
            padding-bottom: 4px;
            display: flex;
            justify-content: space-between;
        }
        .shop-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 8px;
        }
        .shop-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 6px 10px;
            background: #202020;
            border-radius: 8px;
            border: 1px solid #2c2c2c;
        }
        .shop-item.locked {
            background: #151515;
            border: 1px dashed #222;
            opacity: 0.45;
        }
        .shop-info {
            flex-grow: 1;
            margin-right: 10px;
        }
        .shop-name {
            font-size: 0.8rem;
            font-weight: bold;
            color: #e0e0e0;
        }
        .shop-desc {
            font-size: 0.7rem;
            color: #888888;
        }
        button.buy-btn {
            background-color: #ffd700;
            color: #121212;
            border: none;
            padding: 8px 12px;
            font-size: 0.75rem;
            font-weight: bold;
            font-family: 'Kosugi Maru', sans-serif;
            border-radius: 6px;
            cursor: pointer;
            min-width: 80px;
            box-shadow: 0 3px 0px #bca100;
            transition: all 0.1s;
        }
        button.buy-btn:hover {
            background-color: #ffe240;
        }
        button.buy-btn:active {
            transform: translateY(2px);
            box-shadow: 0 1px 0px #bca100;
        }
        button.buy-btn:disabled {
            background-color: #333;
            color: #666;
            box-shadow: none;
            transform: none;
            cursor: not-allowed;
        }
        .instruction {
            font-size: 0.7rem;
            color: #666666;
            margin-top: 8px;
        }
    </style>
</head>
<body>

<div class="game-container">
    <div class="header-area">
        <div>
            <h1>🌱 限界フリーターのもやし栽培</h1>
            <span class="title-sub">〜豆腐パックに咲いた、妙に豊かなお顔たち〜</span>
        </div>
        <button id="btn-sound" class="sound-toggle active">🔊 音 ON</button>
    </div>

    <!-- 自作の名前変更ダイアログポップアップ -->
    <div id="rename-modal" class="modal-overlay">
        <div class="modal-content">
            <div class="modal-title">パックの名前を変更する</div>
            <input type="text" id="modal-name-input" class="modal-input" maxlength="12" placeholder="新しいパックの名前">
            <div class="modal-btns">
                <button id="modal-btn-cancel" class="modal-btn modal-btn-cancel">キャンセル</button>
                <button id="modal-btn-confirm" class="modal-btn modal-btn-confirm">変更する</button>
            </div>
        </div>
    </div>

    <!-- ランダムイベント警告エリア -->
    <div id="event-banner" class="event-banner">
        <div class="event-banner-header">
            <span id="event-icon">⚠</span>
            <span id="event-text">イベント発生中！</span>
            <span id="event-timer">(残り 0秒)</span>
        </div>
        <div id="event-desc" class="event-banner-desc">
            イベントの詳細効果がここに表示されます。
        </div>
    </div>

    <!-- 栽培／図鑑切り替えタブ -->
    <div class="tabs">
        <button id="tab-grow" class="tab-btn active">🧺 栽培（豆腐パック）</button>
        <button id="tab-zukan" class="tab-btn">📖 もやし図鑑</button>
    </div>
    
    <div class="status-panel">
        <div class="status-item">所持金<br><span id="money-display" class="status-value">0</span> 円</div>
        <div class="status-item">水分量<br><span id="water-display" class="status-value water">30</span> / 100</div>
        <div class="status-item">地位 (称号)<br><span id="rank-display" class="status-value rank">もやし初心者</span></div>
    </div>

    <!-- メイン：栽培コンテナ -->
    <div id="grow-view">
        <div class="canvas-container">
            <canvas id="tray-canvas" width="440" height="240"></canvas>
        </div>
    </div>

    <!-- サブ：図鑑コンテナ -->
    <div id="zukan-view" class="zukan-container">
        <div class="zukan-grid" id="zukan-grid-content">
            <!-- 動的に生成されます -->
        </div>
    </div>

    <div class="instruction" id="drag-guide">💡 パックの赤いラベルをタップ（クリック）すると名前を変更できます！</div>

    <div class="controls" id="grow-controls">
        <button id="btn-water" class="action-btn">💧 霧吹きを吹く</button>
        <button id="btn-harvest" class="action-btn" style="background-color: #ffd700; box-shadow: 0 4px 0px #bca100; color: #121212;">🧺 一括出荷</button>
    </div>

    <div class="log-box" id="log-message">
        暗い部屋の片隅、豆腐の空きパックでもやしを育て始めた。
    </div>

    <div class="shop-section" id="shop-area">
        <div class="shop-title">
            <span>💸 怪しい深夜の百急ネット（段階的解禁設備）</span>
            <span style="color: #ffd700;" id="total-harvested">累計出荷: 0本</span>
        </div>
        
        <div class="shop-grid">
            <div class="shop-item" id="item-box-spray">
                <div class="shop-info">
                    <div class="shop-name">ハイパー霧吹き (Lv <span id="lv-spray">1</span>)</div>
                    <div class="shop-desc">一度の水やり給水量 +<span id="val-spray">3</span></div>
                </div>
                <button id="buy-spray" class="buy-btn">15円</button>
            </div>

            <div class="shop-item" id="item-box-fluid">
                <div class="shop-info">
                    <div class="shop-name" id="name-fluid">怪しい夜間栽培ライト (Lv <span id="lv-fluid">0</span>)</div>
                    <div class="shop-desc" id="desc-fluid">自動水分補給 +<span id="val-fluid">0</span>/秒</div>
                </div>
                <button id="buy-fluid" class="buy-btn">50円</button>
            </div>

            <div class="shop-item" id="item-box-speed">
                <div class="shop-info">
                    <div class="shop-name" id="name-speed">怪しい活力液「のびーるX」 (Lv <span id="lv-speed">1</span>)</div>
                    <div class="shop-desc" id="desc-speed">もやしの成長速度が上昇 (x<span id="val-speed">1.0</span>)</div>
                </div>
                <button id="buy-speed" class="buy-btn">120円</button>
            </div>

            <div class="shop-item" id="item-box-pot">
                <div class="shop-info">
                    <div class="shop-name" id="name-pot">こだわり豆乳極厚パック (最大 <span id="val-max-pot">50</span>本)</div>
                    <div class="shop-desc" id="desc-pot">容器を拡張して同時栽培可能数をUP！</div>
                </div>
                <button id="buy-pot" class="buy-btn">300円</button>
            </div>

            <!-- 新規追加設備「招きもやしのお守り」 -->
            <div class="shop-item" id="item-box-luck">
                <div class="shop-info">
                    <div class="shop-name" id="name-luck">怪しいお守り「招きもやし」 (Lv <span id="lv-luck">0</span>)</div>
                    <div class="shop-desc" id="desc-luck">怪しい気運で、レアもやしの発生確率が少し上昇！</div>
                </div>
                <button id="buy-luck" class="buy-btn">600円</button>
            </div>
        </div>
    </div>
</div>

<script>
    // --- 音響システム (Web Audio API) ---
    const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    let isSoundOn = true;

    function playSound(type) {
        if (!isSoundOn) return;
        if (audioCtx.state === 'suspended') {
            audioCtx.resume();
        }

        const osc = audioCtx.createOscillator();
        const gainNode = audioCtx.createGain();
        osc.connect(gainNode);
        gainNode.connect(audioCtx.destination);

        const now = audioCtx.currentTime;

        if (type === 'water') {
            osc.type = 'triangle';
            osc.frequency.setValueAtTime(120, now);
            osc.frequency.exponentialRampToValueAtTime(1200, now + 0.15);
            gainNode.gain.setValueAtTime(0.15, now);
            gainNode.gain.linearRampToValueAtTime(0, now + 0.15);
            osc.start(now);
            osc.stop(now + 0.15);
        } else if (type === 'harvest') {
            osc.type = 'sine';
            osc.frequency.setValueAtTime(500, now);
            osc.frequency.setValueAtTime(800, now + 0.04);
            gainNode.gain.setValueAtTime(0.1, now);
            gainNode.gain.linearRampToValueAtTime(0, now + 0.07);
            osc.start(now);
            osc.stop(now + 0.07);
        } else if (type === 'buy') {
            osc.type = 'sine';
            osc.frequency.setValueAtTime(987.77, now);
            osc.frequency.setValueAtTime(1318.51, now + 0.08);
            gainNode.gain.setValueAtTime(0.1, now);
            gainNode.gain.exponentialRampToValueAtTime(0.01, now + 0.3);
            osc.start(now);
            osc.stop(now + 0.3);
        } else if (type === 'levelUp') {
            osc.type = 'square';
            osc.frequency.setValueAtTime(523.25, now);
            osc.frequency.setValueAtTime(659.25, now + 0.1);
            osc.frequency.setValueAtTime(783.99, now + 0.2);
            osc.frequency.setValueAtTime(1046.50, now + 0.3);
            gainNode.gain.setValueAtTime(0.05, now);
            gainNode.gain.linearRampToValueAtTime(0, now + 0.5);
            osc.start(now);
            osc.stop(now + 0.5);
        } else if (type === 'alert') {
            osc.type = 'sawtooth';
            osc.frequency.setValueAtTime(300, now);
            osc.frequency.linearRampToValueAtTime(600, now + 0.3);
            gainNode.gain.setValueAtTime(0.08, now);
            gainNode.gain.linearRampToValueAtTime(0, now + 0.3);
            osc.start(now);
            osc.stop(now + 0.3);
        }
    }

    // --- ゲームデータ ---
    const state = {
        money: 0,
        water: 30,
        maxWater: 100,
        totalHarvested: 0,
        moyashis: [],
        effects: [], 
        maxMoyashiCapacity: 50, 
        packName: "超・限界極みパック", // パックの初期名
        levels: {
            spray: 1, 
            fluid: 0, 
            speed: 1, 
            pot: 1,
            luck: 0   // 新：招きもやしのレベル
        },
        costs: {
            spray: 15,
            fluid: 50,
            speed: 120,
            pot: 300,
            luck: 600 // 新：招きもやしの初期コスト
        },
        // 図鑑アンロック管理 & 収穫数カウンター (15種類に大幅拡張！)
        zukan: {
            NORMAL: { discovered: true, count: 0 }, 
            THIN: { discovered: false, count: 0 },
            BLACK: { discovered: false, count: 0 },
            HEART: { discovered: false, count: 0 },
            MUSTACHE: { discovered: false, count: 0 },
            BABY: { discovered: false, count: 0 },
            CAT: { discovered: false, count: 0 },
            SAMURAI: { discovered: false, count: 0 },
            PUNK: { discovered: false, count: 0 },       // 新種1
            NINJA: { discovered: false, count: 0 },      // 新種2
            DISCO: { discovered: false, count: 0 },
            ALIEN: { discovered: false, count: 0 },      // 新種3
            ZOMBIE: { discovered: false, count: 0 },
            ANGEL: { discovered: false, count: 0 },
            GOLD: { discovered: false, count: 0 }
        },
        currentEvent: null, 
        eventTimeLeft: 0,   
        lastEventTime: 0,    
        rainDrops: []       
    };

    // フリーター称号 (10段階へ拡張！)
    const RANKS = [
        { minMoney: 0, title: "もやし初心者" },
        { minMoney: 100, title: "もやしが主食" },
        { minMoney: 500, title: "実家からの独立" },
        { minMoney: 2000, title: "もやしマスター" },
        { minMoney: 10000, title: "豆腐パックの一等星" },
        { minMoney: 30000, title: "もやしブローカー" },
        { minMoney: 100000, title: "もやし大富豪" },
        { minMoney: 300000, title: "豆腐パック支配者" },
        { minMoney: 1000000, title: "もやし財閥の総帥" },
        { minMoney: 5000000, title: "銀河もやし創世神" }
    ];

    // --- 各もやしの放置セリフ集 (15種類に超大幅ボリュームアップ！) ---
    const TALK_PATTERNS = {
        NORMAL: [
            "バイト代、いつだっけ…", "隣の部屋、また騒いでるな", "もやし炒め、飽きない？", 
            "外、雨降ってきたかな", "スマホの画面、バキバキだね", "布団干したいな…",
            "12円パスタこそ我が主食", "来世は松茸になりたい…", "水道代払ったっけ…",
            "この虚無感がたまらん", "バイト先バックレたいな", "あ、いま靴下に穴空いた"
        ],
        THIN: [
            "もう、限界っす…", "水分が足りない…気がする…", "細すぎて見えなくなっちゃう", 
            "エアコン、30度設定？", "風が吹いたら折れそう…", "栄養…分けてください…",
            "パックの底が冷たいです", "もやし溶けそう", "干からびる寸前です",
            "エアコンのフィルター、掃除しなよ", "僕たち、存在自体が奇跡", "明日こそ潤いを…"
        ],
        BLACK: [
            "黒豆だからって、調子乗ってないよ？", "たまには奮発してすき焼き食べなよ", "バイト先の店長、怖いね", 
            "少しだけ高級感、出てます？", "僕、煮物に合うんですよ", "ま、のんびり生きようや",
            "安いもやしと混ぜないでよね", "ワンランク上の黒豆パワー！", "家賃1000円上げていい？",
            "お味噌汁に入れると絶品だよ", "おしゃまな黒豆って呼ばれてます", "バイトお疲れ様、コーラ飲む？"
        ],
        HEART: [
            "ねぇ、こっち見て？", "愛してるよぉ！", "豆腐パックから愛を込めて♪", 
            "アホ毛じゃなくてハートだよ！", "君の隣に生えたいな", "ハッピーバレンタイン！",
            "この想い、一括出荷しないで！", "君にロックオン中♪", "僕が癒やしてあげるね",
            "胸のキュンキュンが止まらない！", "今日の夢に君が出てきたよ", "君と僕の共同生活だね"
        ],
        MUSTACHE: [
            "酸いも甘いも噛み分けた一本さ", "焦ってもしょうがない、どっしり構えな", "ダンディズムは豆腐パックにも宿る", 
            "ちょっとお茶でもせんかね", "仕事の悩みなら、いつでも聞くぞい", "人生、100年時代じゃな",
            "若者よ、霧吹きを恐れるな", "豆腐パックの裏にも歴史あり", "渋いダンディの香りじゃ",
            "ワシの若い頃は土で育ったものじゃ", "髭の手入れが忙しくてな", "たまには美味い酒が飲みてぇなぁ"
        ],
        BABY: [
            "ばぶー！", "だっこしてほしいのち", "おなかすいたバブ", 
            "よしよしして？", "バブみを感じてほしいち", "ねんねのじかん…",
            "まだ生まれたてバブ", "パックの中はあったかいち", "ちゅっちゅ…",
            "ミルクのお水くださいバブ", "ママー！お水ママ！", "ばぶばぶー！"
        ],
        CAT: [
            "お腹すいたにゃ", "ゴロゴロ…", "豆腐パックをツメでガリガリ", 
            "気まぐれに生えてみたにゃ", "なでなでしていいにゃよ", "また昼寝の時間にゃ",
            "にゃー（おみずの要求）", "ここの土、掘りやすいにゃ", "ふみふみ…",
            "フリーター、遊んでにゃ", "チュールはないにゃ？", "毛玉吐きそうにゃ"
        ],
        SAMURAI: [
            "この豆腐パック、拙者の戦場也", "水の一滴は血の一滴でござる", "安易に刈られると思うなよ！", 
            "武士は食わねど高楊枝…お腹減った…", "主君、霧吹きを頼み申す！", "正々堂々と勝負でござる！",
            "悪霊退散！カビなど恐れん！", "切腹の準備を…いや出荷か", "おのれ湿気め、成敗いたす！",
            "拙者のちょんまげは伊達ではない", "我が魂（マメ）、見事に咲かせよう", "主、本日も大儀であった"
        ],
        PUNK: [
            "うるせえ！もやしにルールなんかねえ！", "豆腐パックをぶち壊せ！", "俺のモヒカンに触るな！",
            "反逆のノイズを聴けえ！", "シャバい霧吹きはいらねえぜ！", "バイトなんか辞めちまえ！",
            "安売りのもやしで終わってたまるか！", "お行儀よく並んで生えろだと？クソ喰らえ！", "俺たちのパンクソウル！",
            "アナーキー・イン・ザ・パック！", "常識をブチ破るモヒカン！", "売値1円？冗談じゃねえ！"
        ],
        NINJA: [
            "忍びの里より参上…", "パックの隅に気配を消す…", "忍法・水分吸収の術！",
            "拙者の姿が見えるか？", "刈り取るのも一瞬の業也…", "天井のシミと同化するでござる",
            "背後を狙うカビの影を討つ…", "隠密行動こそ忍びの基本", "忍！今、主の手元をすり抜けた",
            "巻物を落としたでござる", "水蜘蛛の術…豆腐パックが揺れる", "しめやかに、発芽…"
        ],
        DISCO: [
            "フゥー！アゲてこーぜ！", "豆腐パックがダンスフロアだ！", "ミラーボールのように輝ぜ！", 
            "テンションMAXでいこう！", "イェーイ！もっと水くれー！", "踊り明かそうぜ、今夜！",
            "ワンルームディスコ、開幕！", "家賃滞納？踊ればチャラさ！", "ベースを響かせろ！",
            "光り輝くマイライフ！", "ステップが止まらないぜ！", "フィーバータイム突入！"
        ],
        ALIEN: [
            "ワレワレハ…モヤシダ…", "アパート上空にUFOを検出", "宇宙の深淵から電波を受信中",
            "地球の水分を調査する…", "ピピピ…バイトお疲れ様…", "パックをテラフォーミングする",
            "フォースを感じるポヨ", "ワタシ、オミズ、トモダチ", "母星の豆腐パックに帰りたい",
            "地球のフリーター、妙に親近感", "UFOから光線が…あ、栽培ライトか", "宇宙の真理はもやしにあり"
        ],
        ZOMBIE: [
            "湿気,最高…", "こっちにおいでよ…", "怨めしや〜", 
            "暗いアパートの隅、居心地いいな", "むしられても,また蘇る…", "うおお、水が染みる…",
            "カビの友達がたくさんいるよ", "バイオハザードパック！", "うう…肉（肥料）をくれ…",
            "一度死んでからが本番さ", "僕たちのゾンビパンチを受けろ", "世も末だね、ひっひっひ"
        ],
        ANGEL: [
            "あなたに神の恵みを", "家賃、払えるといいですね…", "迷えるフリーターを救いに来ました", 
            "豆腐パックに舞い降りし奇跡", "天界 of 霧吹き…", "心穏やかにお過ごしください",
            "あなたの心がきらきら光るのが見えます", "ガス代は天界が肩代わり…できませんでした", "聖水（霧吹き）を浴びましょう",
            "救済の時は近いです", "私の翼はもやしの葉っぱです", "愛と光を豆腐パックに"
        ],
        GOLD: [
            "今月の家賃、ワシに任せとけ", "金の力、見せてやるわい", "実質タダじゃな", 
            "金で買えないものはないのじゃ！", "まぶしすぎて目が潰れるぞい", "成金もやし、ここに極まれり！",
            "キャッシュでアパート丸ごと買ったろか", "金箔霧吹きに変えてくれんかね", "不労所得万歳！",
            "とりあえずタワマン買っといたぞい", "余った小銭で百急ネットを買収するか", "ワシを収穫すればバイト引退じゃ"
        ],
        WITHERED: [
            "もうへにゃへにゃだ…", "お,おみず…霧吹きを…", "し,しおれる……", 
            "限界を…超えた……", "視界が…まっ茶色に……",
            "誰か助けてえ…", "土に戻りそうです", "お肌がカサカサ…",
            "干からびて顔がシワシワに…", "エアコン消して…暑い…", "さようなら、豆腐パック…"
        ]
    };

    // --- もやしの種類データ ---
    const MOYASHI_TYPES = {
        NORMAL: { 
            name: 'ぷにぷにもやし', price: 1, color: '#fffff0', fillCapColor: '#ffe893', capColor: '#ffe893', weight: 35, capSize: 7, faceType: 'normal',
            description: 'スーパーで一袋19円で売られているフリーターの主食。どんな過酷な環境でもたくましく育つ、我々の精神的支柱。'
        },
        THIN: { 
            name: '限界極細もやし', price: 3, color: '#f5fcfd', fillCapColor: '#c2e0ff', capColor: '#c2e0ff', weight: 15, capSize: 5, faceType: 'thin',
            description: '日当たりと水分が足りない、まさに限界状態の我が部屋を体現した細さ。売ってもほぼ利益が出ないのが悲しい。'
        },
        BLACK: { 
            name: 'おしゃまな黒豆もやし', price: 10, color: '#fffff0', fillCapColor: '#4a3c31', capColor: '#4a3c31', weight: 11, capSize: 7.5, faceType: 'black',
            description: 'いつも買う安いものより、ワンランク上の黒豆もやし。バイト代が入った日だけ奮発して買う特別な存在。'
        },
        HEART: { 
            name: 'らぶらぶハートもやし', price: 50, color: '#fff0f5', fillCapColor: '#ff9ebb', capColor: '#ff9ebb', weight: 8, capSize: 8, isSpecial: 'heart', faceType: 'lovelove',
            description: 'アホ毛がラブリーなハート型のもやし。この暗い部屋で、一体誰に向かって愛をアピールしているのだろう。'
        },
        MUSTACHE: { 
            name: 'ダンディ髭おやじもやし', price: 120, color: '#fafae8', fillCapColor: '#bfb563', capColor: '#bfb563', weight: 7, capSize: 7, isSpecial: 'mustache', faceType: 'dandy',
            description: '見事な髭をたくわえた紳士。バイト先の厳しい店長に少し似ているが、こっちの方が圧倒的に優しく話を聞いてくれそう。'
        },
        BABY: { 
            name: 'べびぃバブもやし', price: 220, color: '#fffff0', fillCapColor: '#ffd3b6', capColor: '#ffd3b6', weight: 6, capSize: 6, isSpecial: 'baby', faceType: 'baby',
            description: '哺乳瓶のような芽をつけた赤ちゃんもやし。出荷するにはあまりに心が痛むが、背に腹は代えられない。許せ。'
        },
        CAT: { 
            name: 'にゃんこともやし', price: 350, color: '#fffff0', fillCapColor: '#fca5a5', capColor: '#fca5a5', weight: 5, capSize: 7.5, isSpecial: 'cat', faceType: 'cat',
            description: 'マメが猫耳型をした、きまぐれな新種もやし。豆腐パックをたまに引っ掻くが可愛いので許されている。'
        },
        SAMURAI: { 
            name: '武士もやし', price: 500, color: '#fffff0', fillCapColor: '#6b7280', capColor: '#6b7280', weight: 4, capSize: 8, isSpecial: 'samurai', faceType: 'samurai',
            description: 'ちょんまげを結い、忠義を誓うもやし。背筋がスッと伸びており、安易に刈り取られない武士のプライドを感じる。'
        },
        PUNK: { 
            name: '反逆のパンクもやし', price: 700, color: '#fff1f2', fillCapColor: '#fda4af', capColor: '#fda4af', weight: 3.5, capSize: 8, isSpecial: 'punk', faceType: 'punk',
            description: '頭部が尖ったモヒカン型の異端児もやし。豆腐パック内の不条理に抗うためロックンロールを奏でている。'
        },
        NINJA: { 
            name: '隠密忍者もやし', price: 900, color: '#f3f4f6', fillCapColor: '#374151', capColor: '#374151', weight: 3.0, capSize: 7.5, isSpecial: 'ninja', faceType: 'ninja',
            description: '頭に忍び頭巾を巻いたもやし。暗闇に溶け込み、時おり吹き出しすら消して完全に気配を絶つ。'
        },
        DISCO: { 
            name: 'パリピディスコもやし', price: 1200, color: '#f3e8ff', fillCapColor: '#c084fc', capColor: '#c084fc', weight: 2.5, capSize: 8.5, isSpecial: 'disco', faceType: 'disco',
            description: 'マメがミラーボールのように七色に変化するド派手なもやし。暗いフリーターの部屋をクラブのように彩ってくれる。'
        },
        ALIEN: { 
            name: '宇宙人タコもやし', price: 1800, color: '#ecfdf5', fillCapColor: '#34d399', capColor: '#34d399', weight: 2.0, capSize: 8, isSpecial: 'alien', faceType: 'alien',
            description: 'タコ型火星人の姿をした地球外生命体もやし。夜な夜な怪しい宇宙の周波数をフリーターの脳内に送り届けている。'
        },
        ZOMBIE: { 
            name: '闇堕ちおばけもやし', price: 2500, color: '#e8fdf0', fillCapColor: '#8a5cf5', capColor: '#8a5cf5', weight: 1.5, capSize: 7.5, isSpecial: 'ghost', faceType: 'zombie',
            description: '部屋のジメジメした湿気と負のオーラを限界まで吸い込み変異した。たまにこちらを怨めしそうに見つめてくる。'
        },
        ANGEL: { 
            name: '大天使みやびもやし', price: 5000, color: '#fffff9', fillCapColor: '#ffe359', capColor: '#ffe359', weight: 0.8, capSize: 8.5, isSpecial: 'angel', faceType: 'nerd',
            description: '頭上に神々しい輪っかを乗せた奇跡のもやし。このうらぶれたフリーターのアパートに、光と救済をもたらす天使。'
        },
        GOLD: { 
            name: '純金成金もやし', price: 10000, color: '#fffff0', fillCapColor: '#fbbf24', capColor: '#fbbf24', weight: 0.2, capSize: 9, isSpecial: 'gold', faceType: 'rich',
            description: '全身が純金でできている伝説の一本。これが一本出荷できるだけで、今月の家賃とガス代を無事に納めることができる。'
        }
    };

    // --- ランダムイベントの定義 ---
    const RANDOM_EVENTS = {
        RAIN: {
            id: 'RAIN',
            name: '限界アパートに激震！ゲリラ豪雨',
            icon: '🌧',
            desc: '雨漏りで水分が勝手に回復するが、溺れるな！ (自動水分補給+12/秒)',
            duration: 15,
            bgColor: 'rgba(33, 150, 243, 0.15)'
        },
        FESTIVAL: {
            id: 'FESTIVAL',
            name: '深夜のもやし祭り (深夜特売日)',
            icon: '🏮',
            desc: '深夜営業 of スーパーが奇跡 of 特売開始！出荷額が【2倍】になる！',
            duration: 18,
            bgColor: 'rgba(255, 215, 0, 0.15)'
        },
        MOLD: {
            id: 'MOLD',
            name: '梅雨 of 災厄！黒カビの襲来',
            icon: '🦠',
            desc: 'パック内が異常繁殖したカビに侵食！水分を吸われ、もやしが急乾燥！ (水分自動減少/もやし乾燥速度3倍、霧吹きを吹くとカビが少し消滅！)',
            duration: 15,
            bgColor: 'rgba(46, 204, 113, 0.18)'
        },
        GAS: {
            id: 'GAS',
            name: '怪しい活性化ガスの発生',
            icon: '💨',
            desc: 'アパートの隙間から怪しいガスが流入！もやしの成長速度が【3倍】に、しかし水分消費も【3倍】！',
            duration: 15,
            bgColor: 'rgba(155, 89, 182, 0.15)'
        },
        BONUS: {
            id: 'BONUS',
            name: '奇跡！バイト代の臨時収入',
            icon: '💰',
            desc: '日雇いバイトの未払金が振り込まれた！財布が一瞬潤う。',
            duration: 0, 
            bgColor: ''
        }
    };

    // 称号を取得する関数
    function getRank() {
        let currentRank = RANKS[0].title;
        for (let r of RANKS) {
            if (state.money >= r.minMoney) {
                currentRank = r.title;
            }
        }
        return currentRank;
    }

    // --- DOM要素の参照 ---
    const canvas = document.getElementById('tray-canvas');
    const ctx = canvas.getContext('2d');
    const moneyDisplay = document.getElementById('money-display');
    const waterDisplay = document.getElementById('water-display');
    const rankDisplay = document.getElementById('rank-display');
    const logMessage = document.getElementById('log-message');
    const totalHarvestedDisplay = document.getElementById('total-harvested');
    
    // イベントバナー用DOMの拡張
    const eventBanner = document.getElementById('event-banner');
    const eventIcon = document.getElementById('event-icon');
    const eventText = document.getElementById('event-text');
    const eventDesc = document.getElementById('event-desc');
    const eventTimerDisplay = document.getElementById('event-timer');
    
    // 独自の名前変更用ポップアップダイアログDOM
    const renameModal = document.getElementById('rename-modal');
    const modalNameInput = document.getElementById('modal-name-input');
    const modalBtnCancel = document.getElementById('modal-btn-cancel');
    const modalBtnConfirm = document.getElementById('modal-btn-confirm');
    
    const btnWater = document.getElementById('btn-water');
    const btnHarvest = document.getElementById('btn-harvest');
    const buySpray = document.getElementById('buy-spray');
    const buyFluid = document.getElementById('buy-fluid');
    const buySpeed = document.getElementById('buy-speed');
    const buyPot = document.getElementById('buy-pot');
    const buyLuck = document.getElementById('buy-luck'); 
    const btnSound = document.getElementById('btn-sound');
    
    const lvSpray = document.getElementById('lv-spray');
    const lvFluid = document.getElementById('lv-fluid');
    const lvSpeed = document.getElementById('lv-speed');
    const lvLuck = document.getElementById('lv-luck'); 
    const valSpray = document.getElementById('val-spray');
    const valFluid = document.getElementById('val-fluid');
    const valSpeed = document.getElementById('val-speed');
    const valMaxPot = document.getElementById('val-max-pot');

    // タブ切り替え用
    const tabGrow = document.getElementById('tab-grow');
    const tabZukan = document.getElementById('tab-zukan');
    const growView = document.getElementById('grow-view');
    const zukanView = document.getElementById('zukan-view');
    const dragGuide = document.getElementById('drag-guide');
    const growControls = document.getElementById('grow-controls');
    const shopArea = document.getElementById('shop-area');
    const zukanGridContent = document.getElementById('zukan-grid-content');

    let isDrawing = false;

    function setLog(msg) {
        logMessage.innerText = msg;
    }

    // --- UIとアンロックシステム状態の同期 ---
    function updateUI() {
        moneyDisplay.innerText = Math.floor(state.money);
        waterDisplay.innerText = Math.floor(state.water);
        rankDisplay.innerText = getRank();
        totalHarvestedDisplay.innerText = `累計出荷: ${state.totalHarvested}本`;

        // 1. ハイパー霧吹き (常にアンロック)
        lvSpray.innerText = state.levels.spray;
        valSpray.innerText = state.levels.spray * 3;
        buySpray.innerText = `${state.costs.spray}円`;
        buySpray.disabled = state.money < state.costs.spray;

        // 2. 夜間栽培ライト (霧吹きがLv2以上、つまり1度でも買ったらアンロック)
        const isFluidUnlocked = state.levels.spray >= 2;
        const itemBoxFluid = document.getElementById('item-box-fluid');
        const nameFluid = document.getElementById('name-fluid');
        const descFluid = document.getElementById('desc-fluid');

        if (isFluidUnlocked) {
            itemBoxFluid.classList.remove('locked');
            nameFluid.innerHTML = `怪しい夜間栽培ライト (Lv <span id="lv-fluid">${state.levels.fluid}</span>)`;
            descFluid.innerHTML = `自動水分補給 +<span id="val-fluid">${state.levels.fluid * 2}</span>/秒`;
            buyFluid.innerText = `${state.costs.fluid}円`;
            buyFluid.disabled = state.money < state.costs.fluid;
        } else {
            itemBoxFluid.classList.add('locked');
            nameFluid.innerHTML = `？？？ (ロック中)`;
            descFluid.innerHTML = `霧吹きをLv2以上にすると解禁`;
            buyFluid.innerText = `ロック中`;
            buyFluid.disabled = true;
        }

        // 3. のびーるX (夜間ライトがLv1以上、つまりライトを1回買ったらアンロック)
        const isSpeedUnlocked = state.levels.fluid >= 1;
        const itemBoxSpeed = document.getElementById('item-box-speed');
        const nameSpeed = document.getElementById('name-speed');
        const descSpeed = document.getElementById('desc-speed');

        if (isSpeedUnlocked) {
            itemBoxSpeed.classList.remove('locked');
            nameSpeed.innerHTML = `怪しい活力液「のびーるX」 (Lv <span id="lv-speed">${state.levels.speed}</span>)`;
            descSpeed.innerHTML = `もやしの成長速度が上昇 (x<span id="val-speed">${(1.0 + (state.levels.speed - 1) * 0.25).toFixed(2)}</span>)`;
            buySpeed.innerText = `${state.costs.speed}円`;
            buySpeed.disabled = state.money < state.costs.speed;
        } else {
            itemBoxSpeed.classList.add('locked');
            nameSpeed.innerHTML = `？？？ (ロック中)`;
            descSpeed.innerHTML = `夜間栽培ライトをLv1以上にすると解禁`;
            buySpeed.innerText = `ロック中`;
            buySpeed.disabled = true;
        }

        // 4. こだわり極厚パック (のびーるXがLv2以上、つまりのびーるXを1回買ったらアンロック)
        const isPotUnlocked = state.levels.speed >= 2;
        const itemBoxPot = document.getElementById('item-box-pot');
        const namePot = document.getElementById('name-pot');
        const descPot = document.getElementById('desc-pot');

        if (isPotUnlocked) {
            itemBoxPot.classList.remove('locked');
            namePot.innerHTML = `こだわり豆乳極厚パック (最大 <span id="val-max-pot">${state.maxMoyashiCapacity}</span>本)`;
            descPot.innerHTML = `容器を拡張して同時栽培可能数をUP！`;
            buyPot.disabled = state.money < state.costs.pot || state.maxMoyashiCapacity >= 100;
            if (state.maxMoyashiCapacity >= 100) {
                buyPot.innerText = "MAX";
            } else {
                buyPot.innerText = `${state.costs.pot}円`;
            }
        } else {
            itemBoxPot.classList.add('locked');
            namePot.innerHTML = `？？？ (ロック中)`;
            descPot.innerHTML = `のびーるXをLv2以上にすると解禁`;
            buyPot.innerText = `ロック中`;
            buyPot.disabled = true;
        }

        // 5. 新：招きもやしのお守り (こだわり極厚パックLv2以上(1度でも購入)で解禁)
        const isLuckUnlocked = state.levels.pot >= 2;
        const itemBoxLuck = document.getElementById('item-box-luck');
        const nameLuck = document.getElementById('name-luck');
        const descLuck = document.getElementById('desc-luck');

        if (isLuckUnlocked) {
            itemBoxLuck.classList.remove('locked');
            nameLuck.innerHTML = `怪しいお守り「招きもやし」 (Lv <span id="lv-luck">${state.levels.luck}</span>)`;
            descLuck.innerHTML = `運を引き寄せ、レアもやしの出現確率アップ！ (補正 +${state.levels.luck * 10}%)`;
            buyLuck.innerText = `${state.costs.luck}円`;
            buyLuck.disabled = state.money < state.costs.luck;
        } else {
            itemBoxLuck.classList.add('locked');
            nameLuck.innerHTML = `？？？ (ロック中)`;
            descLuck.innerHTML = `栽培パックを1回以上拡張すると解禁`;
            buyLuck.innerText = `ロック中`;
            buyLuck.disabled = true;
        }
    }

    function getRandomType() {
        const luckBonus = state.levels.luck * 0.15; 
        const rand = Math.random() * 100;
        let cumulative = 0;
        
        const adjustedWeights = {};
        let totalWeight = 0;
        
        Object.keys(MOYASHI_TYPES).forEach(key => {
            let w = MOYASHI_TYPES[key].weight;
            if (key === 'NORMAL' || key === 'THIN') {
                w = Math.max(5, w - luckBonus * 12);
            } else {
                w = w + luckBonus * (MOYASHI_TYPES[key].price > 1000 ? 0.3 : 1.2);
            }
            adjustedWeights[key] = w;
            totalWeight += w;
        });

        const scaledRand = (rand / 100) * totalWeight;

        const keys = Object.keys(adjustedWeights);
        for (let key of keys) {
            cumulative += adjustedWeights[key];
            if (scaledRand <= cumulative) {
                return key;
            }
        }
        return 'NORMAL';
    }

    function spawnMoyashi() {
        if (state.moyashis.length >= state.maxMoyashiCapacity) return; 
        
        const typeKey = getRandomType();
        const type = MOYASHI_TYPES[typeKey];
        const personalities = ['happy', 'sleepy', 'doya', 'surprised', 'drool', 'cry', 'punk', 'ninja', 'alien', 'nerd'];
        const personalFace = personalities[Math.floor(Math.random() * personalities.length)];

        state.moyashis.push({
            x: Math.random() * (canvas.width - 60) + 30,
            y: canvas.height - 35, 
            height: 0,
            maxHeight: Math.random() * 50 + 50,
            speed: (Math.random() * 0.4 + 0.3) * (1.0 + (state.levels.speed - 1) * 0.25),
            typeKey: typeKey, 
            type: type,
            wiggle: Math.random() * 100, 
            curve: (Math.random() - 0.5) * 14,
            witherRate: 0,
            blinkTimer: Math.random() * 100,
            personality: personalFace,
            msg: "",
            msgTimer: 0
        });
    }

    // パーティクルエフェクト
    function addEffect(x, y, type, color = '#fffff0') {
        const count = type === 'harvest' ? 8 : 4;
        for (let i = 0; i < count; i++) {
            state.effects.push({
                x: x,
                y: y,
                vx: (Math.random() - 0.5) * 4,
                vy: (Math.random() - 0.8) * 3 - 1,
                life: 1.0,
                decay: 0.04 + Math.random() * 0.02,
                size: Math.random() * 5 + 3,
                type: type, 
                color: color
            });
        }
    }

    // --- ランダムイベント発生装置 ---
    function triggerRandomEvent() {
        if (state.currentEvent) return;

        const keys = Object.keys(RANDOM_EVENTS);
        const randomKey = keys[Math.floor(Math.random() * keys.length)];
        const eventDef = RANDOM_EVENTS[randomKey];

        if (eventDef.id === 'BONUS') {
            const bonus = Math.floor(Math.random() * 201) + 100; 
            state.money += bonus;
            playSound('levelUp');
            setLog(`💰【臨時収入】日雇いバイト代が入った！財布に +${bonus} 円！`);
            updateUI();
            addEffect(canvas.width / 2, canvas.height - 100, 'star', '#ffd700');
        } else {
            state.currentEvent = eventDef;
            state.eventTimeLeft = eventDef.duration;
            playSound('alert');
            setLog(`${eventDef.icon}【イベント発生】${eventDef.name}！(${eventDef.desc})`);
            
            eventBanner.style.display = 'flex';
            eventIcon.innerText = eventDef.icon;
            eventText.innerText = eventDef.name;
            eventDesc.innerText = eventDef.desc; 
            eventTimerDisplay.innerText = `(残り ${state.eventTimeLeft}秒)`;

            if (eventDef.id === 'RAIN') {
                state.rainDrops = [];
                for(let i=0; i<30; i++) {
                    state.rainDrops.push({
                        x: Math.random() * canvas.width,
                        y: Math.random() * -canvas.height,
                        speed: Math.random() * 4 + 8,
                        len: Math.random() * 10 + 15
                    });
                }
            }
        }
    }

    // --- 図鑑データの生成・更新 ---
    function renderZukan() {
        zukanGridContent.innerHTML = '';
        Object.keys(MOYASHI_TYPES).forEach(key => {
            const data = MOYASHI_TYPES[key];
            const info = state.zukan[key];
            const itemDiv = document.createElement('div');
            itemDiv.className = `zukan-item ${info.discovered ? '' : 'locked'}`;

            if (info.discovered) {
                itemDiv.innerHTML = `
                    <div class="zukan-icon-wrapper">
                        <div class="zukan-stem" style="background-color: ${data.color};"></div>
                        <div class="zukan-mame" style="background-color: ${data.capColor};"></div>
                    </div>
                    <div class="zukan-info">
                        <div class="zukan-name">${data.name}</div>
                        <div class="zukan-desc">${data.description}</div>
                        <div class="zukan-stats">
                            <span>収穫数: ${info.count}本</span>
                            <span class="zukan-price">売値目安: 最大${data.price}円</span>
                        </div>
                    </div>
                `;
            } else {
                itemDiv.innerHTML = `
                    <div class="zukan-icon-wrapper">
                        <div style="font-size: 1.2rem; color: #444;">？</div>
                    </div>
                    <div class="zukan-info">
                        <div class="zukan-name">？？？？？？</div>
                        <div class="zukan-desc">未発見。豆腐パックで栽培して出荷すると情報が解禁される。</div>
                        <div class="zukan-stats">
                            <span>出現割合: ${data.weight}%</span>
                        </div>
                    </div>
                `;
            }
            zukanGridContent.appendChild(itemDiv);
        });
    }

    function unlockZukan(key) {
        if (!state.zukan[key].discovered) {
            state.zukan[key].discovered = true;
            return true; 
        }
        return false;
    }

    function drawSpeechBubble(text, x, y) {
        ctx.save();
        ctx.font = '9px sans-serif';
        const padding = 6;
        const textWidth = ctx.measureText(text).width;
        const bubbleW = textWidth + padding * 2;
        const bubbleH = 14 + padding;

        const bx = x - bubbleW / 2;
        const by = y - bubbleH - 8;

        ctx.shadowColor = 'rgba(0, 0, 0, 0.4)';
        ctx.shadowBlur = 4;

        ctx.fillStyle = 'rgba(255, 255, 255, 0.9)';
        ctx.beginPath();
        ctx.roundRect(bx, by, bubbleW, bubbleH, 4);
        ctx.fill();

        ctx.shadowBlur = 0; 

        ctx.beginPath();
        ctx.moveTo(x - 4, by + bubbleH);
        ctx.lineTo(x + 4, by + bubbleH);
        ctx.lineTo(x, by + bubbleH + 4);
        ctx.closePath();
        ctx.fill();

        ctx.fillStyle = '#111111';
        ctx.textAlign = 'center';
        ctx.fillText(text, x, by + 12);
        ctx.restore();
    }

    // --- 描画処理 ---
    function draw() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);

        ctx.fillStyle = '#1c1816';
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        
        ctx.strokeStyle = '#0f0c0b';
        ctx.lineWidth = 2;
        for(let i = 0; i < canvas.height; i += 60) {
            ctx.beginPath();
            ctx.moveTo(0, i);
            ctx.lineTo(canvas.width, i);
            ctx.stroke();
        }

        if (state.currentEvent && state.currentEvent.bgColor) {
            ctx.fillStyle = state.currentEvent.bgColor;
            ctx.fillRect(0, 0, canvas.width, canvas.height);
        }

        state.moyashis.forEach(m => {
            ctx.save();
            ctx.translate(m.x, m.y);

            const witherFactor = m.witherRate;
            
            ctx.beginPath();
            ctx.moveTo(0, 0);
            
            const segments = 6;
            const segHeight = m.height / segments;
            for(let i = 1; i <= segments; i++) {
                const currentY = -segHeight * i;
                const wiggleOffset = Math.sin(m.wiggle + i) * (m.height * 0.025);
                const witherOffset = witherFactor * (i / segments) * 16;
                const currentX = wiggleOffset + (m.curve * (i / segments)) + witherOffset;
                
                const finalY = (i === segments) ? currentY + (witherFactor * 6) : currentY;
                ctx.lineTo(currentX, finalY);
            }
            
            let stemColor = m.type.color;
            let fillCapColor = m.type.capColor;
            if (witherFactor > 0.1) {
                stemColor = '#7a756e';
                fillCapColor = '#4a3d35';
            }

            ctx.strokeStyle = stemColor;
            ctx.lineWidth = m.type === MOYASHI_TYPES.THIN ? 3 : 5; 
            ctx.lineCap = 'round';
            ctx.lineJoin = 'round';
            ctx.stroke();

            const topX = Math.sin(m.wiggle + segments) * (m.height * 0.025) + m.curve + (witherFactor * 16);
            const topY = -m.height + (witherFactor * 6);
            
            ctx.beginPath();
            ctx.ellipse(topX, topY, m.type.capSize, m.type.capSize * 0.85, 0, 0, Math.PI * 2);
            ctx.fillStyle = fillCapColor;
            if (m.type.isSpecial === 'disco' && witherFactor <= 0.1) {
                const hue = (Date.now() / 5 + m.x) % 360;
                ctx.fillStyle = `hsl(${hue}, 80%, 65%)`;
            }
            ctx.fill();

            const isGrown = m.height > 15;
            m.blinkTimer += 0.05;
            const isBlinking = Math.sin(m.blinkTimer) > 0.95; 

            if (isGrown) {
                ctx.save();
                ctx.translate(topX, topY);
                ctx.fillStyle = '#333333';
                ctx.strokeStyle = '#333333';
                ctx.lineWidth = 1.2;

                if (witherFactor > 0.2) {
                    ctx.beginPath();
                    ctx.moveTo(-3, -1); ctx.lineTo(-1, 1);
                    ctx.moveTo(-3, 1); ctx.lineTo(-1, -1);
                    ctx.moveTo(1, -1); ctx.lineTo(3, 1);
                    ctx.moveTo(1, 1); ctx.lineTo(3, -1);
                    ctx.stroke();
                    ctx.beginPath();
                    ctx.moveTo(-1, 3);
                    ctx.quadraticCurveTo(0, 1.5, 1, 3);
                    ctx.stroke();
                } else {
                    let face = m.personality;
                    if (m.type.faceType === 'dandy') face = 'dandy';
                    if (m.type.faceType === 'zombie') face = 'zombie';
                    if (m.type.faceType === 'baby') face = 'baby';
                    if (m.type.faceType === 'rich') face = 'rich'; 
                    if (m.type.faceType === 'samurai') face = 'samurai';
                    if (m.type.faceType === 'cat') face = 'cat';
                    if (m.type.faceType === 'disco') face = 'disco';
                    if (m.type.isSpecial === 'punk') face = 'punk';
                    if (m.type.isSpecial === 'ninja') face = 'ninja';
                    if (m.type.isSpecial === 'alien') face = 'alien';

                    if (face === 'happy') {
                        if (isBlinking) {
                            ctx.beginPath(); ctx.arc(-2, -1, 1.2, Math.PI, 0, false); ctx.stroke();
                            ctx.beginPath(); ctx.arc(2, -1, 1.2, Math.PI, 0, false); ctx.stroke();
                        } else {
                            ctx.beginPath(); ctx.arc(-2.2, -1, 1.2, 0, Math.PI * 2); ctx.arc(2.2, -1, 1.2, 0, Math.PI * 2); ctx.fill();
                        }
                        ctx.beginPath(); ctx.arc(0, 1.5, 1.5, 0, Math.PI, false); ctx.stroke(); 
                    } 
                    else if (face === 'sleepy') {
                        ctx.beginPath();
                        ctx.moveTo(-3, -1); ctx.lineTo(-1, -1);
                        ctx.moveTo(1, -1); ctx.lineTo(3, -1);
                        ctx.stroke();
                        ctx.beginPath(); ctx.arc(0, 2, 1, 0, Math.PI * 2); ctx.fill(); 
                    } 
                    else if (face === 'doya') {
                        ctx.beginPath();
                        ctx.moveTo(-3.5, -2.5); ctx.lineTo(-1.5, -1.5); 
                        ctx.moveTo(1.5, -1.5); ctx.lineTo(3.5, -2.5); 
                        ctx.stroke();
                        ctx.beginPath(); ctx.arc(-2, -0.5, 1.1, 0, Math.PI * 2); ctx.arc(2, -0.5, 1.1, 0, Math.PI * 2); ctx.fill();
                        ctx.beginPath(); ctx.moveTo(-2, 2.5); ctx.lineTo(2, 2); ctx.stroke(); 
                    } 
                    else if (face === 'surprised') {
                        ctx.beginPath(); ctx.arc(-2.2, -1, 1.2, 0, Math.PI * 2); ctx.arc(2.2, -1, 1.2, 0, Math.PI * 2); ctx.fill();
                        ctx.beginPath(); ctx.arc(0, 2, 2, 0, Math.PI * 2); ctx.stroke(); 
                    } 
                    else if (face === 'drool') {
                        ctx.beginPath(); ctx.arc(-2.2, -1, 1.2, 0, Math.PI * 2); ctx.arc(2.2, -1, 1.2, 0, Math.PI * 2); ctx.fill();
                        ctx.beginPath(); ctx.arc(0, 1.5, 1.5, 0, Math.PI * 2); ctx.fill(); 
                        ctx.fillStyle = 'rgba(133, 193, 233, 0.9)';
                        ctx.beginPath(); ctx.arc(1.5, 3.5, 1, 0, Math.PI * 2); ctx.fill();
                    }
                    else if (face === 'cry') {
                        ctx.beginPath();
                        ctx.moveTo(-3, -2); ctx.lineTo(-3, 1);
                        ctx.moveTo(3, -2); ctx.lineTo(3, 1);
                        ctx.moveTo(-1, 0); ctx.lineTo(1, 0);
                        ctx.stroke();
                        ctx.fillStyle = '#33b5e5';
                        ctx.beginPath();
                        ctx.arc(-3, 2.5, 1, 0, Math.PI * 2);
                        ctx.arc(3, 2.5, 1, 0, Math.PI * 2);
                        ctx.fill();
                    }
                    else if (face === 'dandy') {
                        ctx.beginPath(); ctx.arc(-2.5, -1, 1.2, 0, Math.PI * 2); ctx.arc(2.5, -1, 1.2, 0, Math.PI * 2); ctx.fill();
                        ctx.fillStyle = 'rgba(17, 17, 17, 1)';
                        ctx.beginPath();
                        ctx.ellipse(-1.5, 2, 2.2, 1, Math.PI / 6, 0, Math.PI * 2);
                        ctx.ellipse(1.5, 2, 2.2, 1, -Math.PI / 6, 0, Math.PI * 2);
                        ctx.fill();
                    }
                    else if (face === 'zombie') {
                        ctx.strokeStyle = '#555';
                        ctx.beginPath();
                        ctx.moveTo(-3, -2); ctx.lineTo(-1, 0); ctx.moveTo(-1, -2); ctx.lineTo(-3, 0); 
                        ctx.moveTo(1, -2); ctx.lineTo(3, 0); ctx.moveTo(3, -2); ctx.lineTo(1, 0);
                        ctx.stroke();
                        ctx.beginPath(); ctx.arc(0, 2.5, 2, Math.PI, 0, false); ctx.stroke(); 
                    }
                    else if (face === 'baby') {
                        ctx.beginPath(); ctx.arc(-2.2, -1, 1.5, 0, Math.PI * 2); ctx.arc(2.2, -1, 1.5, 0, Math.PI * 2); ctx.fill();
                        ctx.fillStyle = '#ffffff';
                        ctx.beginPath(); ctx.arc(-2.6, -1.4, 0.6, 0, Math.PI * 2); ctx.arc(1.8, -1.4, 0.6, 0, Math.PI * 2); ctx.fill(); 
                        ctx.fillStyle = '#333333';
                        ctx.beginPath(); ctx.arc(0, 1.5, 1, 0, Math.PI * 2); ctx.fill(); 
                    }
                    else if (face === 'samurai') {
                        ctx.beginPath();
                        ctx.moveTo(-3.5, -3); ctx.lineTo(-1, -1.5); 
                        ctx.moveTo(3.5, -3); ctx.lineTo(1, -1.5);
                        ctx.stroke();
                        ctx.beginPath(); ctx.arc(-2.2, -0.5, 1.2, 0, Math.PI * 2); ctx.arc(2.2, -0.5, 1.2, 0, Math.PI * 2); ctx.fill();
                        ctx.beginPath(); ctx.arc(0, 1.8, 1.2, 0, Math.PI, true); ctx.stroke(); 
                    }
                    else if (face === 'cat') {
                        ctx.beginPath();
                        ctx.moveTo(-3, -2); ctx.lineTo(-1, -1.5); ctx.lineTo(-3, -1);
                        ctx.moveTo(3, -2); ctx.lineTo(1, -1.5); ctx.lineTo(3, -1);
                        ctx.stroke();
                        ctx.beginPath();
                        ctx.arc(-1, 1.5, 1, 0, Math.PI, false);
                        ctx.arc(1, 1.5, 1, 0, Math.PI, false);
                        ctx.stroke();
                    }
                    else if (face === 'disco') {
                        ctx.fillStyle = '#000000';
                        ctx.beginPath();
                        ctx.roundRect(-4.5, -2.5, 4, 3, 1);
                        ctx.roundRect(0.5, -2.5, 4, 3, 1);
                        ctx.fill();
                        ctx.strokeStyle = '#000000';
                        ctx.beginPath();
                        ctx.moveTo(-1, -1.5); ctx.lineTo(1, -1.5);
                        ctx.stroke();
                        ctx.beginPath();
                        ctx.arc(0, 1.5, 1.5, 0, Math.PI, false);
                        ctx.stroke();
                    }
                    else if (face === 'rich') {
                        ctx.strokeStyle = '#e67e22';
                        ctx.font = 'bold 5px sans-serif';
                        ctx.fillText('¥', -5.2, 0.5);
                        ctx.fillText('¥', 1.2, 0.5);
                        ctx.beginPath(); ctx.arc(0, 2, 1.5, 0, Math.PI, false); ctx.stroke();
                    }
                    else if (face === 'punk') {
                        ctx.fillStyle = '#ff0055';
                        ctx.beginPath();
                        ctx.moveTo(-5, -3); ctx.lineTo(-2, -1); ctx.lineTo(-5, 1);
                        ctx.moveTo(5, -3); ctx.lineTo(2, -1); ctx.lineTo(5, 1);
                        ctx.fill();
                        ctx.fillStyle = '#000';
                        ctx.beginPath(); ctx.arc(-2.5, -1, 1.1, 0, Math.PI * 2); ctx.arc(2.5, -1, 1.1, 0, Math.PI * 2); ctx.fill();
                        ctx.strokeStyle = '#000';
                        ctx.beginPath(); ctx.moveTo(-2, 2.5); ctx.lineTo(2, 1.5); ctx.stroke();
                    }
                    else if (face === 'ninja') {
                        ctx.fillStyle = '#374151';
                        ctx.beginPath(); ctx.roundRect(-5.5, 0.5, 11, 5, 2); ctx.fill();
                        ctx.fillStyle = '#ffeb3b'; 
                        ctx.beginPath(); ctx.arc(-2.2, -1, 1.0, 0, Math.PI * 2); ctx.arc(2.2, -1, 1.0, 0, Math.PI * 2); ctx.fill();
                    }
                    else if (face === 'alien') {
                        ctx.fillStyle = '#000000';
                        ctx.beginPath();
                        ctx.ellipse(-2.5, -1, 1.8, 3, Math.PI/10, 0, Math.PI*2);
                        ctx.ellipse(2.5, -1, 1.8, 3, -Math.PI/10, 0, Math.PI*2);
                        ctx.fill();
                        ctx.beginPath(); ctx.arc(0, 2, 0.8, 0, Math.PI*2); ctx.fill();
                    }
                    else if (face === 'nerd') {
                        ctx.strokeStyle = '#000';
                        ctx.lineWidth = 1.5;
                        ctx.beginPath(); ctx.arc(-2.2, -1, 2.0, 0, Math.PI * 2); ctx.stroke();
                        ctx.beginPath(); ctx.arc(2.2, -1, 2.0, 0, Math.PI * 2); ctx.stroke();
                        ctx.beginPath(); ctx.moveTo(-0.2, -1); ctx.lineTo(0.2, -1); ctx.stroke();
                        ctx.lineWidth = 0.8;
                        ctx.beginPath(); ctx.arc(-2.2, -1, 1.0, 0, Math.PI * 2); ctx.stroke();
                        ctx.beginPath(); ctx.arc(2.2, -1, 1.0, 0, Math.PI * 2); ctx.stroke();
                        ctx.fillStyle = '#f87171';
                        ctx.beginPath(); ctx.ellipse(0, 2.2, 2, 1, 0, 0, Math.PI*2); ctx.fill();
                    }

                    if (face !== 'ninja') {
                        ctx.fillStyle = 'rgba(255, 182, 193, 0.7)';
                        ctx.beginPath();
                        ctx.arc(-4, 1.2, 1.5, 0, Math.PI * 2);
                        ctx.arc(4, 1.2, 1.5, 0, Math.PI * 2);
                        ctx.fill();
                    }
                }
                ctx.restore();
            }

            if (m.type.isSpecial === 'heart') {
                ctx.save();
                ctx.translate(topX, topY - m.type.capSize);
                ctx.strokeStyle = '#ff9ebb';
                ctx.lineWidth = 1.5;
                ctx.beginPath();
                ctx.moveTo(0, 0);
                ctx.quadraticCurveTo(-3, -4, -1, -6);
                ctx.quadraticCurveTo(0, -4, 0, -2);
                ctx.quadraticCurveTo(0, -4, 1, -6);
                ctx.quadraticCurveTo(3, -4, 0, 0);
                ctx.stroke();
                ctx.restore();
            } else if (m.type.isSpecial === 'angel') {
                ctx.save();
                ctx.translate(topX, topY - m.type.capSize - 4);
                ctx.strokeStyle = '#ffe893';
                ctx.lineWidth = 1.5;
                ctx.beginPath();
                ctx.ellipse(0, 0, 6, 1.8, 0, 0, Math.PI * 2);
                ctx.stroke();
                ctx.restore();
            } else if (m.type.isSpecial === 'baby') {
                ctx.save();
                ctx.translate(topX, topY - m.type.capSize - 3);
                ctx.fillStyle = '#ffffff';
                ctx.fillRect(-1.5, -4, 3, 4);
                ctx.fillStyle = '#ffb3b3';
                ctx.fillRect(-1, -6, 2, 2);
                ctx.restore();
            } else if (m.type.isSpecial === 'cat') {
                ctx.save();
                ctx.translate(topX, topY);
                ctx.fillStyle = m.type.capColor;
                ctx.beginPath();
                ctx.moveTo(-m.type.capSize + 1, -2);
                ctx.lineTo(-m.type.capSize - 1, -7);
                ctx.lineTo(-2, -m.type.capSize + 2);
                ctx.fill();
                ctx.beginPath();
                ctx.moveTo(m.type.capSize - 1, -2);
                ctx.lineTo(m.type.capSize + 1, -7);
                ctx.lineTo(2, -m.type.capSize + 2);
                ctx.fill();
                ctx.restore();
            } else if (m.type.isSpecial === 'samurai') {
                ctx.save();
                ctx.translate(topX, topY - m.type.capSize + 1);
                ctx.fillStyle = '#111111';
                ctx.beginPath();
                ctx.ellipse(0, -2, 2.5, 4, Math.PI / 4, 0, Math.PI * 2);
                ctx.fill();
                ctx.restore();
            } else if (m.type.isSpecial === 'punk') {
                ctx.save();
                ctx.translate(topX, topY - m.type.capSize);
                ctx.fillStyle = '#ff0055'; 
                ctx.beginPath();
                ctx.moveTo(-2, 1);
                ctx.lineTo(-1, -8);
                ctx.lineTo(1, -8);
                ctx.lineTo(2, 1);
                ctx.fill();
                ctx.beginPath();
                ctx.moveTo(-4, -1); ctx.lineTo(-1, -5); ctx.lineTo(0, -1); ctx.lineTo(2, -5); ctx.lineTo(4, -1);
                ctx.fill();
                ctx.restore();
            } else if (m.type.isSpecial === 'ninja') {
                ctx.save();
                ctx.translate(topX - 4, topY);
                ctx.fillStyle = '#1f2937';
                ctx.beginPath();
                ctx.ellipse(0, 0, 1.5, 4, Math.PI/6, 0, Math.PI*2);
                ctx.fill();
                ctx.restore();
            } else if (m.type.isSpecial === 'alien') {
                ctx.save();
                ctx.translate(topX, topY - m.type.capSize);
                ctx.strokeStyle = m.type.capColor;
                ctx.lineWidth = 1.2;
                ctx.beginPath();
                ctx.moveTo(-2, 0); ctx.quadraticCurveTo(-4, -4, -3, -7);
                ctx.moveTo(2, 0); ctx.quadraticCurveTo(4, -4, 3, -7);
                ctx.stroke();
                ctx.fillStyle = '#10b981';
                ctx.beginPath();
                ctx.arc(-3, -7, 1.5, 0, Math.PI*2);
                ctx.arc(3, -7, 1.5, 0, Math.PI*2);
                ctx.fill();
                ctx.restore();
            } else if (m.type.isSpecial === 'gold') {
                ctx.fillStyle = '#ffd700';
                ctx.beginPath();
                const p = Math.sin(Date.now() / 80) * 2;
                ctx.arc(topX - 8, topY - 6, 1 + p * 0.1, 0, Math.PI * 2);
                ctx.arc(topX + 8, topY + 4, 1.5 + p * 0.1, 0, Math.PI * 2);
                ctx.fill();
            }

            ctx.restore();

            if (m.msg && m.msgTimer > 0) {
                drawSpeechBubble(m.msg, m.x + topX, m.y + topY);
            }
        });

        const potY = canvas.height - 35;
        
        ctx.fillStyle = '#3a3028'; 
        ctx.beginPath();
        ctx.roundRect(15, potY, canvas.width - 30, 15, 4);
        ctx.fill();

        ctx.fillStyle = 'rgba(220, 240, 255, 0.2)'; 
        ctx.beginPath();
        ctx.moveTo(10, potY - 15); 
        ctx.lineTo(25, canvas.height - 12); 
        ctx.lineTo(canvas.width - 25, canvas.height - 12); 
        ctx.lineTo(canvas.width - 10, potY - 15); 
        ctx.lineTo(canvas.width - 15, potY - 15);
        ctx.lineTo(canvas.width - 28, canvas.height - 15);
        ctx.lineTo(28, canvas.height - 15);
        ctx.lineTo(15, potY - 15);
        ctx.closePath();
        ctx.fill();

        ctx.strokeStyle = 'rgba(255, 255, 255, 0.4)';
        ctx.lineWidth = 1;
        ctx.strokeRect(10, canvas.height - 12, canvas.width - 20, 1.5);

        // ラベル（赤い文字のエリア）の背景
        ctx.fillStyle = 'rgba(255, 255, 255, 0.85)';
        ctx.fillRect(canvas.width / 2 - 60, canvas.height - 25, 120, 13);
        
        ctx.strokeStyle = '#dd2222';
        ctx.lineWidth = 1;
        ctx.strokeRect(canvas.width / 2 - 60, canvas.height - 25, 120, 13);

        ctx.fillStyle = '#dd2222';
        ctx.font = 'bold 8px sans-serif';
        ctx.textAlign = 'center';
        ctx.fillText(state.packName, canvas.width / 2, canvas.height - 15);

        if (state.currentEvent && state.currentEvent.id === 'RAIN') {
            ctx.strokeStyle = 'rgba(174, 214, 241, 0.4)';
            ctx.lineWidth = 1;
            state.rainDrops.forEach(drop => {
                ctx.beginPath();
                ctx.moveTo(drop.x, drop.y);
                ctx.lineTo(drop.x + 1.5, drop.y + drop.len);
                ctx.stroke();

                drop.y += drop.speed;
                drop.x += 0.5;

                if (drop.y > canvas.height) {
                    drop.y = Math.random() * -40;
                    drop.x = Math.random() * canvas.width;
                }
            });
        }

        if (state.currentEvent && state.currentEvent.id === 'MOLD') {
            ctx.fillStyle = 'rgba(39, 174, 96, 0.15)';
            ctx.beginPath();
            ctx.ellipse(30, canvas.height - 40, 40, 15, 0, 0, Math.PI*2);
            ctx.ellipse(canvas.width - 30, canvas.height - 40, 40, 15, 0, 0, Math.PI*2);
            ctx.ellipse(canvas.width/2, canvas.height - 35, 80, 20, 0, 0, Math.PI*2);
            ctx.fill();

            ctx.fillStyle = 'rgba(46, 204, 113, 0.3)';
            for(let i=0; i<8; i++) {
                const px = Math.sin(Date.now()/500 + i) * 60 + (canvas.width / 8 * i) + 20;
                const py = Math.cos(Date.now()/300 + i) * 10 + canvas.height - 60;
                ctx.beginPath();
                ctx.arc(px, py, 2.5, 0, Math.PI*2);
                ctx.fill();
            }
        }

        state.effects.forEach((eff, index) => {
            eff.x += eff.vx;
            eff.y += eff.vy;
            eff.life -= eff.decay;
            if (eff.life <= 0) {
                state.effects.splice(index, 1);
                return;
            }

            ctx.save();
            ctx.globalAlpha = eff.life;
            ctx.fillStyle = eff.color;

            if (eff.type === 'star') {
                ctx.beginPath();
                for (let i = 0; i < 5; i++) {
                    ctx.lineTo(Math.cos((18 + i * 72) * Math.PI / 180) * eff.size + eff.x,
                               Math.sin((18 + i * 72) * Math.PI / 180) * eff.size + eff.y);
                    ctx.lineTo(Math.cos((54 + i * 72) * Math.PI / 180) * (eff.size/2) + eff.x,
                               Math.sin((54 + i * 72) * Math.PI / 180) * (eff.size/2) + eff.y);
                }
                ctx.closePath();
                ctx.fill();
            } else {
                ctx.beginPath();
                ctx.arc(eff.x, eff.y, eff.size * 0.5, 0, Math.PI * 2);
                ctx.fill();
            }
            ctx.restore();
        });

        // 水分ゲージ
        ctx.fillStyle = 'rgba(33, 150, 243, 0.25)';
        ctx.fillRect(0, 0, canvas.width * (state.water / state.maxWater), 6);
        ctx.fillStyle = '#2196f3';
        ctx.fillRect(canvas.width * (state.water / state.maxWater) - 2, 0, 2, 6);
    }

    // --- メインループ ---
    function gameLoop() {
        let speedMultiplier = 1.0;
        let waterDrainMultiplier = 1.0;

        if (state.currentEvent) {
            if (state.currentEvent.id === 'GAS') {
                speedMultiplier = 3.0;        
                waterDrainMultiplier = 3.0;   
            } else if (state.currentEvent.id === 'MOLD') {
                waterDrainMultiplier = 3.0;   
            }
        }

        state.moyashis.forEach(m => {
            if (state.water > 0) {
                if (m.height < m.maxHeight) {
                    m.height += m.speed * speedMultiplier;
                    state.water -= 0.005 * waterDrainMultiplier; 
                    if (state.water < 0) state.water = 0;
                }
                m.witherRate = Math.max(0, m.witherRate - 0.05);
            } else {
                const witherSpeed = (state.currentEvent && state.currentEvent.id === 'MOLD') ? 0.024 : 0.008;
                m.witherRate = Math.min(1, m.witherRate + witherSpeed); 
            }
            m.wiggle += 0.035;

            if (m.msgTimer > 0) {
                m.msgTimer--;
                if (m.msgTimer === 0) {
                    m.msg = "";
                }
            }
        });

        if (state.water > 15 && Math.random() < 0.02) {
            spawnMoyashi();
        }

        if (state.moyashis.length > 0 && Math.random() < 0.006) {
            const candidates = state.moyashis.filter(m => m.height > 20 && m.msgTimer === 0);
            if (candidates.length > 0) {
                const target = candidates[Math.floor(Math.random() * candidates.length)];
                let wordPool = [];

                if (target.witherRate > 0.3) {
                    wordPool = TALK_PATTERNS.WITHERED;
                } else {
                    wordPool = TALK_PATTERNS[target.typeKey] || TALK_PATTERNS.NORMAL;
                }

                target.msg = wordPool[Math.floor(Math.random() * wordPool.length)];
                if (target.typeKey === 'NINJA' && Math.random() < 0.5) {
                    target.msg = "";
                } else {
                    target.msgTimer = 180; 
                }
            }
        }

        if (state.currentEvent && state.currentEvent.id === 'RAIN') {
            state.water = Math.min(state.maxWater, state.water + 0.2); 
        }

        draw();
        updateUI();
        requestAnimationFrame(gameLoop);
    }

    // --- 1秒周期のシステムタイマー ---
    setInterval(() => {
        if (state.levels.fluid > 0) {
            let autoWater = state.levels.fluid * 2;
            if (state.currentEvent && state.currentEvent.id === 'MOLD') {
                autoWater = Math.max(0, autoWater - 3); 
            }
            state.water = Math.min(state.maxWater, state.water + autoWater);
            if (Math.random() < 0.4 && autoWater > 0) {
                addEffect(Math.random() * (canvas.width - 60) + 30, canvas.height - 35, 'droplet', '#33b5e5');
            }
        }

        if (state.currentEvent && state.currentEvent.id === 'MOLD') {
            state.water = Math.max(0, state.water - 4); 
        }

        if (state.currentEvent) {
            state.eventTimeLeft--;
            eventTimerDisplay.innerText = `(残り ${state.eventTimeLeft}秒)`;

            if (state.eventTimeLeft <= 0) {
                setLog("📢【イベント終了】「" + state.currentEvent.name + "」が終了しました。");
                state.currentEvent = null;
                eventBanner.style.display = 'none';
            }
        }

        if (!state.currentEvent) {
            if (Math.random() < 0.04) {
                triggerRandomEvent();
            }
        }
    }, 1000);

    // --- ダイアログポップアップの開閉制御 ---
    function openRenameModal() {
        modalNameInput.value = state.packName;
        renameModal.style.display = 'flex';
        setTimeout(() => modalNameInput.focus(), 100);
    }

    function closeRenameModal() {
        renameModal.style.display = 'none';
    }

    modalBtnCancel.addEventListener('click', closeRenameModal);

    modalBtnConfirm.addEventListener('click', () => {
        const newName = modalNameInput.value.trim();
        if (newName) {
            state.packName = newName;
            setLog(`📝 パックの名前を「${newName}」に書き換えました。`);
            playSound('buy');
        }
        closeRenameModal();
    });

    modalNameInput.addEventListener('keydown', (e) => {
        if (e.key === 'Enter') {
            modalBtnConfirm.click();
        } else if (e.key === 'Escape') {
            closeRenameModal();
        }
    });

    // --- タブ切り替え制御 ---
    tabGrow.addEventListener('click', () => {
        tabGrow.className = "tab-btn active";
        tabZukan.className = "tab-btn";
        growView.style.display = "block";
        zukanView.style.display = "none";
        dragGuide.style.display = "block";
        growControls.style.display = "flex";
        shopArea.style.display = "block";
    });

    tabZukan.addEventListener('click', () => {
        tabGrow.className = "tab-btn";
        tabZukan.className = "tab-btn active";
        growView.style.display = "none";
        zukanView.style.display = "block";
        dragGuide.style.display = "none";
        growControls.style.display = "none";
        shopArea.style.display = "none";
        renderZukan(); 
    });

    // --- インタラクション ---

    // 💧 霧吹き
    btnWater.addEventListener('click', () => {
        const addedWater = state.levels.spray * 3;
        state.water = Math.min(state.maxWater, state.water + addedWater);
        playSound('water');
        addEffect(canvas.width / 2, 50, 'droplet', '#33b5e5');

        if (state.currentEvent && state.currentEvent.id === 'MOLD') {
            addEffect(canvas.width/2, canvas.height - 40, 'droplet', '#2ecc71');
            state.water = Math.min(state.maxWater, state.water + 2); 
            setLog(`💧 カビを水で洗い流している！乾燥耐性が少し戻った。`);
        }

        if (Math.random() < 0.25) {
            spawnMoyashi();
        }
        if (!state.currentEvent || state.currentEvent.id !== 'MOLD') {
            setLog(`霧吹きをシュッシュッ！水分が ${addedWater} 回復した。`);
        }
    });

    // 🧺 一括出荷
    btnHarvest.addEventListener('click', () => {
        harvestAll();
    });

    function harvestAll() {
        if (state.moyashis.length === 0) {
            setLog("出荷できるもやしがありません…豆腐パックがガランとしています。");
            return;
        }

        let totalEarnings = 0;
        let harvestedCount = state.moyashis.length;
        let specialFound = "";
        let newDiscoveredCount = 0;

        let priceMultiplier = 1.0;
        if (state.currentEvent && state.currentEvent.id === 'FESTIVAL') {
            priceMultiplier = 2.0; 
        }

        state.moyashis.forEach(m => {
            const witherPenalty = 1 - (m.witherRate * 0.85); 
            const growthFactor = Math.max(0.1, m.height / m.maxHeight);
            const earnings = m.type.price * growthFactor * witherPenalty * priceMultiplier;
            
            totalEarnings += earnings;
            if (m.type.isSpecial) {
                specialFound = m.type.name;
            }

            const isNew = unlockZukan(m.typeKey);
            if (isNew) newDiscoveredCount++;
            state.zukan[m.typeKey].count += 1;

            addEffect(m.x, m.y - m.height, 'star', '#ffdf85');
        });

        state.money += totalEarnings;
        state.totalHarvested += harvestedCount;
        state.moyashis = []; 

        playSound('levelUp');

        let logStr = `一括出荷！${harvestedCount} 本を引っこ抜いて ${Math.floor(totalEarnings)} 円を稼いだ。`;
        if (state.currentEvent && state.currentEvent.id === 'FESTIVAL') {
            logStr += " 🏮【祭り効果】深夜の特売で出荷額がすべて2倍になった！";
        }
        if (newDiscoveredCount > 0) {
            logStr += ` 📖 新種を ${newDiscoveredCount} 種発見！図鑑を確認してみよう。`;
        } else if (specialFound && (!state.currentEvent || state.currentEvent.id !== 'FESTIVAL')) {
            logStr += ` 【変異種】「${specialFound}」が混じっていた。`;
        }
        setLog(logStr);
        updateUI();
    }

    // --- ドラッグなぞり収穫 & ラベルクリック判定 ---
    function checkHarvestOrLabelClick(clientX, clientY, isFirstClick) {
        const rect = canvas.getBoundingClientRect();
        const x = clientX - rect.left;
        const y = clientY - rect.top;

        // Canvasの解像度スケールを実画面座標に補正
        const scaleX = canvas.width / rect.width;
        const scaleY = canvas.height / rect.height;
        const targetX = x * scaleX;
        const targetY = y * scaleY;

        // 1. ラベル（赤い文字のエリア）のクリック判定（最初のクリック時のみ作動）
        if (isFirstClick) {
            const labelLeft = canvas.width / 2 - 60;
            const labelRight = canvas.width / 2 + 60;
            const labelTop = canvas.height - 25;
            const labelBottom = canvas.height - 12;

            if (targetX >= labelLeft && targetX <= labelRight && targetY >= labelTop && targetY <= labelBottom) {
                openRenameModal();
                return; 
            }
        }

        // 2. 通常のもやし収穫のドラッグ・タップ判定
        for (let i = state.moyashis.length - 1; i >= 0; i--) {
            const m = state.moyashis[i];
            const topY = m.y - m.height;
            
            const distToStem = Math.abs(m.x - targetX);
            const isYInRange = (targetY >= topY - 15 && targetY <= m.y);

            if (distToStem < 18 && isYInRange) {
                let priceMultiplier = 1.0;
                if (state.currentEvent && state.currentEvent.id === 'FESTIVAL') {
                    priceMultiplier = 2.0;
                }

                const witherPenalty = 1 - (m.witherRate * 0.85);
                const growthFactor = Math.max(0.1, m.height / m.maxHeight);
                const earnings = Math.floor(m.type.price * growthFactor * witherPenalty * priceMultiplier);
                
                state.money += earnings;
                state.totalHarvested += 1;
                
                const isNew = unlockZukan(m.typeKey);
                state.zukan[m.typeKey].count += 1;

                addEffect(m.x, topY, 'star', m.type.capColor);

                let logStr = `「${m.type.name}」を収穫！ ( +${earnings}円 )`;
                if (state.currentEvent && state.currentEvent.id === 'FESTIVAL') {
                    logStr += " 🏮祭り2倍！";
                }
                if (isNew) {
                    logStr += ` 📖 新種登録！`;
                }
                setLog(logStr);
                playSound('harvest');
                
                state.moyashis.splice(i, 1);
                updateUI();
                break;
            }
        }
    }

    // マウスドラッグ
    canvas.addEventListener('mousedown', (e) => {
        isDrawing = true;
        checkHarvestOrLabelClick(e.clientX, e.clientY, true); 
    });
    canvas.addEventListener('mousemove', (e) => {
        if (!isDrawing) return;
        checkHarvestOrLabelClick(e.clientX, e.clientY, false);
    });
    window.addEventListener('mouseup', () => {
        isDrawing = false;
    });

    // スマホスワイプ
    canvas.addEventListener('touchstart', (e) => {
        isDrawing = true;
        const touch = e.touches[0];
        checkHarvestOrLabelClick(touch.clientX, touch.clientY, true);
    });
    canvas.addEventListener('touchmove', (e) => {
        if (!isDrawing) return;
        const touch = e.touches[0];
        checkHarvestOrLabelClick(touch.clientX, touch.clientY, false);
    });
    window.addEventListener('touchend', () => {
        isDrawing = false;
    });

    // --- 百急ネットストア ---

    // 1. 霧吹き
    buySpray.addEventListener('click', () => {
        if (state.money >= state.costs.spray) {
            state.money -= state.costs.spray;
            state.levels.spray += 1;
            state.costs.spray = Math.floor(state.costs.spray * 1.6);
            playSound('buy');
            addEffect(canvas.width / 2, canvas.height - 80, 'star', '#a7ff83');
            setLog("ハイパー霧吹きを購入！一度にたくさん給水できるようになった。");
            updateUI();
        }
    });

    // 2. 栽培ライト (霧吹きLv2以上でアンロック)
    buyFluid.addEventListener('click', () => {
        if (state.levels.spray >= 2 && state.money >= state.costs.fluid) {
            state.money -= state.costs.fluid;
            state.levels.fluid += 1;
            state.costs.fluid = Math.floor(state.costs.fluid * 1.8);
            playSound('buy');
            addEffect(canvas.width / 2, canvas.height - 80, 'star', '#33b5e5');
            setLog("栽培ライトを購入！自動で水分が満ちるようになった。");
            updateUI();
        }
    });

    // 3. 活力液のびーるX (栽培ライトLv1以上でアンロック)
    buySpeed.addEventListener('click', () => {
        if (state.levels.fluid >= 1 && state.money >= state.costs.speed) {
            state.money -= state.costs.speed;
            state.levels.speed += 1;
            state.costs.speed = Math.floor(state.costs.speed * 2.0);
            playSound('buy');
            addEffect(canvas.width / 2, canvas.height - 80, 'star', '#ffd700');
            state.moyashis.forEach(m => {
                m.speed *= 1.25;
            });
            setLog("活力液「のびーるX」を注入！もやしたちが成長するスピードが上がった。");
            updateUI();
        }
    });

    // 4. 極厚パック拡張 (のびーるXLv2以上でアンロック)
    buyPot.addEventListener('click', () => {
        if (state.levels.speed >= 2 && state.money >= state.costs.pot && state.maxMoyashiCapacity < 100) {
            state.money -= state.costs.pot;
            state.maxMoyashiCapacity = Math.min(100, state.maxMoyashiCapacity + 25);
            state.costs.pot = Math.floor(state.costs.pot * 2.5);
            state.levels.pot += 1; 
            playSound('buy');
            addEffect(canvas.width / 2, canvas.height - 80, 'star', '#e0e0e0');
            
            state.packName = "こだわり豆乳パック";
            
            setLog(`容器を「こだわり豆乳パック」へ改良！同時栽培上限が ${state.maxMoyashiCapacity} 本にアップ！`);
            updateUI();
        }
    });

    // 5. 新：招きもやしのお守り (こだわり極厚パックLv2以上(1度でも購入)で解禁)
    buyLuck.addEventListener('click', () => {
        if (state.levels.pot >= 2 && state.money >= state.costs.luck) {
            state.money -= state.costs.luck;
            state.levels.luck += 1;
            state.costs.luck = Math.floor(state.costs.luck * 2.2);
            playSound('buy');
            addEffect(canvas.width / 2, canvas.height - 80, 'star', '#ffe893');
            setLog("怪しいお守り「招きもやし」を購入！豆腐パックに奇妙な開運のオーラが漂い、レアなもやしが発生しやすくなった！");
            updateUI();
        }
    });

    // 音の切替
    btnSound.addEventListener('click', () => {
        isSoundOn = !isSoundOn;
        if (isSoundOn) {
            btnSound.innerText = "🔊 音 ON";
            btnSound.classList.add('active');
            playSound('buy');
        } else {
            btnSound.innerText = "🔇 音 OFF";
            btnSound.classList.remove('active');
        }
    });

    // 初期もやし
    for(let i=0; i<3; i++) {
        spawnMoyashi();
        state.moyashis[i].height = Math.random() * 30 + 15;
    }

    // 最初の状態を初期化
    updateUI();
    gameLoop();
</script>

</body>
</html>
