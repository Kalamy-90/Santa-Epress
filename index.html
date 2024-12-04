// Configuration du jeu
let game = {
    canvas: null,
    ctx: null,
    width: 800,
    height: 600,
    running: false,
    score: 0,
    timeLeft: 60,
    lastTime: 0,
    player: null,
    presents: [],
    chimneys: [],
    obstacles: [],
    stars: [],
    snowflakes: [],
    difficultySettings: {
        easy: { speed: 1, obstacleRate: 0.5, starRate: 0.8 },
        medium: { speed: 1.5, obstacleRate: 0.7, starRate: 0.6 },
        hard: { speed: 2, obstacleRate: 1, starRate: 0.4 }
    }
};

// Classe joueur (Père Noël)
class Player {
    constructor() {
        this.x = 100;
        this.y = game.height / 2;
        this.width = 80;
        this.height = 60;
        this.speed = 5;
        this.presentCooldown = 0;
    }

    update() {
        // Gestion des contrôles
        if (keys[config.controls.up]) this.y = Math.max(0, this.y - this.speed);
        if (keys[config.controls.down]) this.y = Math.min(game.height - this.height, this.y + this.speed);
        if (keys[config.controls.left]) this.x = Math.max(0, this.x - this.speed);
        if (keys[config.controls.right]) this.x = Math.min(game.width - this.width, this.x + this.speed);
        
        if (this.presentCooldown > 0) this.presentCooldown--;
    }

    draw() {
        game.ctx.drawImage(images.santa, this.x, this.y, this.width, this.height);
    }

    dropPresent() {
        if (this.presentCooldown === 0) {
            game.presents.push(new Present(this.x, this.y + this.height / 2));
            playSound('drop');
            this.presentCooldown = 20;
        }
    }
}

// Classe cadeau
class Present {
    constructor(x, y) {
        this.x = x;
        this.y = y;
        this.width = 30;
        this.height = 30;
        this.speed = 3;
        this.falling = true;
    }

    update() {
        if (this.falling) {
            this.y += this.speed;
            if (this.y > game.height) {
                return false;
            }
            
            // Vérification collision avec cheminées
            for (let chimney of game.chimneys) {
                if (this.checkCollision(chimney)) {
                    game.score += 100;
                    playSound('success');
                    return false;
                }
            }
        }
        return true;
    }

    draw() {
        game.ctx.drawImage(images.present, this.x, this.y, this.width, this.height);
    }

    checkCollision(obj) {
        return this.x < obj.x + obj.width &&
               this.x + this.width > obj.x &&
               this.y < obj.y + obj.height &&
               this.y + this.height > obj.y;
    }
}

// Classe cheminée
class Chimney {
    constructor() {
        this.width = 60;
        this.height = 80;
        this.x = game.width;
        this.y = game.height - this.height;
    }

    update() {
        this.x -= 2;
        return this.x + this.width > 0;
    }

    draw() {
        game.ctx.drawImage(images.chimney, this.x, this.y, this.width, this.height);
    }
}

// Classe obstacle (oiseaux et drones)
class Obstacle {
    constructor() {
        this.width = 40;
        this.height = 40;
        this.x = game.width;
        this.y = Math.random() * (game.height - this.height);
        this.type = Math.random() < 0.5 ? 'bird' : 'drone';
        this.speed = this.type === 'bird' ? 3 : 4;
    }

    update() {
        this.x -= this.speed;
        
        if (this.type === 'bird') {
            this.y += Math.sin(this.x / 30) * 2;
        }
        
        // Collision avec le joueur
        if (game.player.checkCollision(this)) {
            game.score = Math.max(0, game.score - 50);
            playSound('crash');
            return false;
        }
        
        return this.x + this.width > 0;
    }

    draw() {
        const image = this.type === 'bird' ? images.bird : images.drone;
        game.ctx.drawImage(image, this.x, this.y, this.width, this.height);
    }
}

// Classe étoile (bonus)
class Star {
    constructor() {
        this.width = 30;
        this.height = 30;
        this.x = game.width;
        this.y = Math.random() * (game.height - this.height);
        this.speed = 2;
    }

    update() {
        this.x -= this.speed;
        
        if (game.player.checkCollision(this)) {
            game.score += 50;
            playSound('collect');
            return false;
        }
        
        return this.x + this.width > 0;
    }

    draw() {
        game.ctx.drawImage(images.star, this.x, this.y, this.width, this.height);
    }
}

// Classe flocon de neige
class Snowflake {
    constructor() {
        this.x = Math.random() * game.width;
        this.y = -10;
        this.size = Math.random() * 3 + 2;
        this.speed = Math.random() * 2 + 1;
        this.wind = Math.random() * 2 - 1;
    }

    update() {
        this.y += this.speed;
        this.x += this.wind;
        return this.y < game.height;
    }

    draw() {
        game.ctx.beginPath();
        game.ctx.fillStyle = 'white';
        game.ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
        game.ctx.fill();
    }
}

// Gestionnaire de touches
const keys = {};
document.addEventListener('keydown', (e) => {
    keys[e.key] = true;
    if (e.key === config.controls.drop) {
        game.player.dropPresent();
    }
});
document.addEventListener('keyup', (e) => keys[e.key] = false);

// Fonctions de jeu principales
function startGame() {
    loadSounds();
    updateVolumes();
    
    game.canvas = document.getElementById('gameCanvas');
    game.ctx = game.canvas.getContext('2d');
    
    document.getElementById('mainMenu').style.display = 'none';
    game.canvas.style.display = 'block';
    document.getElementById('hud').style.display = 'block';
    
    game.running = true;
    game.score = 0;
    game.timeLeft = 60;
    game.player = new Player();
    game.presents = [];
    game.chimneys = [];
    game.obstacles = [];
    game.stars = [];
    game.snowflakes = [];
    
    config.audio.music.play();
    
    requestAnimationFrame(gameLoop);
}

function gameLoop(timestamp) {
    if (!game.lastTime) game.lastTime = timestamp;
    const deltaTime = (timestamp - game.lastTime) / 1000;
    game.lastTime = timestamp;
    
    if (!game.running) return;
    
    update(deltaTime);
    draw();
    
    if (game.timeLeft > 0) {
        requestAnimationFrame(gameLoop);
    } else {
        endGame();
    }
}

function update(deltaTime) {
    // Mise à jour du temps
    game.timeLeft = Math.max(0, game.timeLeft - deltaTime);
    
    // Mise à jour des entités
    game.player.update();
    
    // Génération aléatoire d'entités
    if (Math.random() < 0.02) game.chimneys.push(new Chimney());
    if (Math.random() < 0.01) game.obstacles.push(new Obstacle());
    if (Math.random() < 0.008) game.stars.push(new Star());
    if (Math.random() < 0.1) game.snowflakes.push(new Snowflake());
    
    // Mise à jour des tableaux d'entités
    game.presents = game.presents.filter(p => p.update());
    game.chimneys = game.chimneys.filter(c => c.update());
    game.obstacles = game.obstacles.filter(o => o.update());
    game.stars = game.stars.filter(s => s.update());
    game.snowflakes = game.snowflakes.filter(s => s.update());
    
    // Mise à jour HUD
    document.getElementById('score').textContent = `🎁 Score: ${game.score}`;
    document.getElementById('timer').textContent = `⏰ Temps: ${Math.ceil(game.timeLeft)}s`;
}

function draw() {
    game.ctx.clearRect(0, 0, game.width, game.height);
    
    // Dessin du fond
    game.ctx.drawImage(images.background, 0, 0, game.width, game.height);
    
    // Dessin des entités
    game.snowflakes.forEach(s => s.draw());
    game.stars.forEach(s => s.draw());
    game.chimneys.forEach(c => c.draw());
    game.presents.forEach(p => p.draw());
    game.obstacles.forEach(o => o.draw());
    game.player.draw();
}

function endGame() {
    game.running = false;
    config.audio.music.pause();
    config.audio.music.currentTime = 0;
    
    const menu = document.createElement('div');
    menu.className = 'menu';
    menu.innerHTML = `
        <h2>Game Over!</h2>
        <p>Score final: ${game.score}</p>
        <button class="btn" onclick="location.reload()">Rejouer</button>
    `;
    
    document.getElementById('gameContainer').appendChild(menu);
}

function playSound(type) {
    const sound = config.audio.effects[type];
    sound.currentTime = 0;
    sound.play();
}

function showSettings() {
    document.getElementById('mainMenu').style.display = 'none';
    document.getElementById('settings').style.display = 'block';
}

function showControls() {
    document.getElementById('mainMenu').style.display = 'none';
    document.getElementById('controls').style.display = 'block';
}

function backToMain() {
    document.querySelectorAll('.menu-content').forEach(el => el.style.display = 'none');
    document.getElementById('mainMenu').style.display = 'block';
}
