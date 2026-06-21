<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ArcadeZone - Unlimited Games</title>
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
        }
        header {
            background: #1a153a;
            padding: 20px;
            text-align: center;
            border-bottom: 3px solid #6c5ce7;
        }
        header h1 {
            color: #6c5ce7;
            font-size: 2.5rem;
            text-transform: uppercase;
            letter-spacing: 2px;
        }
        /* Category Navigation */
        .categories {
            display: flex;
            justify-content: center;
            gap: 15px;
            padding: 20px;
            background: #130f26;
        }
        .cat-btn {
            padding: 10px 20px;
            background: #251b4e;
            border: 2px solid #6c5ce7;
            color: #fff;
            border-radius: 25px;
            cursor: pointer;
            font-weight: bold;
            transition: 0.3s;
        }
        .cat-btn.active, .cat-btn:hover {
            background: #6c5ce7;
            box-shadow: 0 0 10px #6c5ce7;
        }
        /* Main Grid Area */
        .main-container {
            max-width: 1200px;
            margin: 30px auto;
            padding: 0 20px;
        }
        .games-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
            gap: 25px;
        }
        .game-card {
            background: #1a153a;
            border-radius: 12px;
            overflow: hidden;
            border: 1px solid #2d2460;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
        }
        .game-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 10px 20px rgba(108, 92, 231, 0.3);
            border-color: #6c5ce7;
        }
        .game-thumb {
            width: 100%;
            height: 150px;
            background-size: cover;
            background-position: center;
        }
        .game-info {
            padding: 15px;
        }
        .game-title {
            font-size: 1.1rem;
            font-weight: bold;
            margin-bottom: 5px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        .game-tag {
            display: inline-block;
            font-size: 0.75rem;
            background: #6c5ce7;
            padding: 3px 8px;
            border-radius: 4px;
        }
        /* Game Modal / Player View */
        .game-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(10, 7, 20, 0.95);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }
        .modal-content {
            position: relative;
            width: 80%;
            max-width: 900px;
            height: 70vh;
            background: #000;
            border: 3px solid #6c5ce7;
            border-radius: 8px;
            overflow: hidden;
        }
        iframe {
            width: 100%;
            height: 100%;
            border: none;
        }
        .close-btn {
            margin-top: 20px;
            padding: 12px 30px;
            background: #ff7675;
            color: #fff;
            border: none;
            border-radius: 5px;
            font-size: 1rem;
            cursor: pointer;
            font-weight: bold;
        }
    </style>
</head>
<body>

<header>
    <h1>🕹️ ArcadeZone</h1>
    <p>Explore Unlimited HTML5 Games</p>
</header>

<div class="categories">
    <button class="cat-btn active" onclick="filterCategory('All')">All Games</button>
    <button class="cat-btn" onclick="filterCategory('Action')">Action</button>
    <button class="cat-btn" onclick="filterCategory('Racing')">Racing</button>
    <button class="cat-btn" onclick="filterCategory('Puzzle')">Puzzle</button>
</div>

<div class="main-container">
    <div class="games-grid" id="gamesGrid">
        </div>
</div>

<div class="game-modal" id="gameModal">
    <div class="modal-content">
        <iframe id="gameFrame" src=""></iframe>
    </div>
    <button class="close-btn" onclick="closeGame()">Close Game</button>
</div>

<script>
// Mock Database Array (Yahan aap real APIs ya database connect karenge)
// Note: iFrames ke liye main ne open-source free distribution urls use kiye hain
const gamesData = [
    {
        id: 1,
        title: "Space Adventure",
        category: "Action",
        thumb: "https://images.unsplash.com/photo-1614728894747-a83421e2b9c9?w=400",
        embedUrl: "https://html5.gamedistribution.com/embed/f09804c8f3cf42b79a0b1df3395b00ee/"
    },
    {
        id: 2,
        title: "Cyber Racer x",
        category: "Racing",
        thumb: "https://images.unsplash.com/photo-1511512578047-dfb367046420?w=400",
        embedUrl: "https://html5.gamedistribution.com/embed/5bc5f19067b848eb8b51296068307db3/"
    },
    {
        id: 3,
        title: "Classic Block Puzzle",
        category: "Puzzle",
        thumb: "https://images.unsplash.com/photo-1606167668584-78701c57f13d?w=400",
        embedUrl: "https://html5.gamedistribution.com/embed/815777a83ee14ef19cb9f8ff3e86c05a/"
    },
    {
        id: 4,
        title: "Archery King",
        category: "Action",
        thumb: "https://images.unsplash.com/photo-1511193311914-0346f16efe90?w=400",
        embedUrl: "https://html5.gamedistribution.com/embed/69a30b4ec2b8426ca2da4ffc18685e82/"
    }
];

const grid = document.getElementById('gamesGrid');
const modal = document.getElementById('gameModal');
const frame = document.getElementById('gameFrame');

// Function to render games into grid
function renderGames(games) {
    grid.innerHTML = "";
    games.forEach(game => {
        const card = document.createElement('div');
        card.className = 'game-card';
        card.onclick = () => playGame(game.embedUrl);
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

// Filter Logic
function filterCategory(category) {
    // Update active class on buttons
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

// Play Game Frame Loader
function playGame(url) {
    frame.src = url;
    modal.style.display = 'flex';
}

// Close Game Logic
function closeGame() {
    frame.src = ""; // Clear memory/iframe
    modal.style.display = 'none';
}

// Initial Load
renderGames(gamesData);
</script>

</body>
</html>
