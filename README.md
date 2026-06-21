<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ArcadeZone - Unlimited Games Hub</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body {
            background: #0f0c1b;
            color: #fff;
            overflow-x: hidden;
        }
        header {
            background: #1a153a;
            padding: 25px;
            text-align: center;
            border-bottom: 3px solid #6c5ce7;
        }
        header h1 {
            color: #6c5ce7;
            font-size: 2.5rem;
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 5px;
        }
        header p {
            color: #a29bfe;
            font-size: 1rem;
        }
        /* Category Navigation Bar */
        .categories {
            display: flex;
            justify-content: center;
            gap: 15px;
            padding: 20px;
            background: #130f26;
            flex-wrap: wrap;
        }
        .cat-btn {
            padding: 10px 25px;
            background: #251b4e;
            border: 2px solid #6c5ce7;
            color: #fff;
            border-radius: 25px;
            cursor: pointer;
            font-weight: bold;
            font-size: 0.9rem;
            transition: all 0.3s ease;
        }
        .cat-btn.active, .cat-btn:hover {
            background: #6c5ce7;
            box-shadow: 0 0 15px #6c5ce7;
            transform: scale(1.05);
        }
        /* Main Games Grid Area */
        .main-container {
            max-width: 1200px;
            margin: 40px auto;
            padding: 0 20px;
        }
        .games-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 30px;
        }
        .game-card {
            background: #1a153a;
            border-radius: 15px;
            overflow: hidden;
            border: 1px solid #2d2460;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }
        .game-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(108, 92, 231, 0.4);
            border-color: #6c5ce7;
        }
        .game-thumb {
            width: 100%;
            height: 160px;
            background-size: cover;
            background-position: center;
            background-color: #251b4e;
            position: relative;
        }
        .game-info {
            padding: 20px;
        }
        .game-title {
            font-size: 1.2rem;
            font-weight: bold;
            margin-bottom: 8px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            color: #fff;
        }
        .game-tag {
            display: inline-block;
            font-size: 0.8rem;
            background: #6c5ce7;
            padding: 4px 10px;
            border-radius: 20px;
            font-weight: 500;
        }
        /* Fullscreen Game Modal Layer */
        .game-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(7, 5, 15, 0.98);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }
        .modal-header {
            width: 85%;
            max-width: 950px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
        .modal-title {
            font-size: 1.5rem;
            font-weight: bold;
            color: #6c5ce7;
        }
        .close-btn {
            padding: 10px 25px;
            background: #ff7675;
            color: #fff;
            border: none;
            border-radius: 5px;
            font-size: 1rem;
            cursor: pointer;
            font-weight: bold;
            transition: background 0.2s;
        }
        .close-btn:hover {
            background: #ee5253;
        }
        .modal-content {
            width: 85%;
            max-width: 950px;
            height: 75vh;
            background: #000;
            border: 3px solid #6c5ce7;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 0 30px rgba(108, 92, 231, 0.5);
        }
        iframe {
            width: 100%;
            height: 100%;
            border: none;
        }
    </style>
</head>
<body>

<header>
    <h1>🕹️ ArcadeZone</h1>
    <p>Unlimited Open-Source Web Games Portal</p>
</header>

<div class="categories" id="categoryTabs">
    <button class="cat-btn active" onclick="filterCategory('All', event)">All Games</button>
    <button class="cat-btn" onclick="filterCategory('Racing', event)">Racing</button>
    <button class="cat-btn" onclick="filterCategory('Puzzle', event)">Puzzle</button>
</div>

<div class="main-container">
    <div class="games-grid" id="gamesGrid">
        </div>
</div>

<div class="game-modal" id="gameModal">
    <div class="modal-header">
        <div class="modal-title" id="currentGameTitle">Game Loading...</div>
        <button class="close-btn" onclick="closeGame()">× Close Game</button>
    </div>
    <div class="modal-content">
        <iframe id="gameFrame" src="" allowfullscreen></iframe>
    </div>
</div>

<script>
// Validated Iframe Friendly Target Source Array
const gamesData = [
    {
        id: 1,
        title: "HexGL (3D Racing Game)",
        category: "Racing",
        thumb: "https://images.unsplash.com/photo-1511512578047-dfb367046420?w=400",
        embedUrl: "https://hexgl.bkcore.com/play/"
    },
    {
        id: 2,
        title: "2048 Puzzle Grid",
        category: "Puzzle",
        thumb: "https://images.unsplash.com/photo-1606167668584-78701c57f13d?w=400",
        embedUrl: "https://gabrielecirulli.github.io/2048/"
    },
    {
        id: 3,
        title: "Hextris Speed Match",
        category: "Puzzle",
        thumb: "https://images.unsplash.com/photo-1511193311914-0346f16efe90?w=400",
        embedUrl: "https://hextris.io/"
    }
];

const grid = document.getElementById('gamesGrid');
const modal = document.getElementById('gameModal');
const frame = document.getElementById('gameFrame');
const modalTitle = document.getElementById('currentGameTitle');

// Core Render Component
function renderGames(list) {
    grid.innerHTML = "";
    if(list.length === 0) {
        grid.innerHTML = `<p style="grid-column: 1/-1; text-align:center; color:#aaa;">No games found in this category.</p>`;
        return;
    }
    list.forEach(game => {
        const card = document.createElement('div');
        card.className = 'game-card';
        card.onclick = () => playGame(game.title, game.embedUrl);
        card.innerHTML = `
            <div class="game-thumb" style="background-image: url('${game.thumb}')"></div>
            <div class="game-info">
                <div class="game-title">${game.title}</div>
                <span class="game-tag">${game.category}</span>
            </div>
        `;
        grid.appendChild(card);
    });
}

// Category Array Filter Handler
function filterCategory(category, event) {
    const buttons = document.querySelectorAll('.cat-btn');
    buttons.forEach(btn => btn.classList.remove('active'));
    event.target.classList.add('active');

    if(category === 'All') {
        renderGames(gamesData);
    } else {
        const filtered = gamesData.filter(g => g.category === category);
        renderGames(filtered);
    }
}

// Execution Loop Trigger for Frame
function playGame(title, url) {
    modalTitle.innerText = "Playing: " + title;
    frame.src = url;
    modal.style.display = 'flex';
}

// Memory Cleanup Logic
function closeGame() {
    frame.src = ""; 
    modal.style.display = 'none';
}

// App Initialization
renderGames(gamesData);
</script>

</body>
</html>
