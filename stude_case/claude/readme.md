https://claude.ai/public/artifacts/43d9a85c-af53-47cf-92af-ea2f26f14324

estourou prompt ao tentar um unico compoente

<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>✈️ Sky Runner - Jogo de Aviação</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(135deg, #0c0c0c 0%, #1a1a2e 50%, #16213e 100%);
            font-family: 'Orbitron', monospace;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            color: white;
            overflow: hidden;
        }

        .game-container {
            position: relative;
            border: 3px solid #00ff88;
            border-radius: 15px;
            box-shadow: 0 0 30px rgba(0, 255, 136, 0.3);
            background: rgba(0, 0, 0, 0.8);
        }

        canvas {
            display: block;
            border-radius: 12px;
            background: linear-gradient(to bottom, 
                #87CEEB 0%, 
                #98D8E8 30%, 
                #B8E6B8 70%, 
                #228B22 70%, 
                #1F5F1F 100%);
        }

        .hud {
            position: absolute;
            top: 10px;
            left: 10px;
            right: 10px;
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            pointer-events: none;
            z-index: 10;
        }

        .hud-left, .hud-right {
            background: rgba(0, 0, 0, 0.7);
            padding: 8px 12px;
            border-radius: 8px;
            border: 1px solid #00ff88;
            font-size: 12px;
            font-weight: 700;
        }

        .score {
            color: #00ff88;
            font-size: 16px;
            text-shadow: 0 0 10px #00ff88;
        }

        .health-bar {
            width: 100px;
            height: 8px;
            background: #333;
            border-radius: 4px;
            overflow: hidden;
            margin-top: 5px;
        }

        .health-fill {
            height: 100%;
            background: linear-gradient(90deg, #ff0000, #ffff00, #00ff00);
            transition: width 0.3s ease;
        }

        .game-over, .start-screen {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.9);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            border-radius: 12px;
        }

        .game-over h1, .start-screen h1 {
            font-size: 2.5rem;
            color: #ff4757;
            text-shadow: 0 0 20px #ff4757;
            margin-bottom: 20px;
            animation: pulse 2s infinite;
        }

        .start-screen h1 {
            color: #00ff88;
            text-shadow: 0 0 20px #00ff88;
        }

        .final-score {
            font-size: 1.5rem;
            color: #00ff88;
            margin-bottom: 20px;
        }

        .restart-btn, .start-btn {
            padding: 12px 24px;
            font-size: 1.2rem;
            font-family: 'Orbitron', monospace;
            font-weight: 700;
            background: linear-gradient(45deg, #00ff88, #00cc6a);
            color: #000;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
        }

        .restart-btn:hover, .start-btn:hover {
            transform: scale(1.1);
            box-shadow: 0 0 20px rgba(0, 255, 136, 0.5);
        }

        .controls {
            position: absolute;
            bottom: 10px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(0, 0, 0, 0.7);
            padding: 8px 16px;
            border-radius: 8px;
            font-size: 11px;
            border: 1px solid #555;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }

        .shake {
            animation: shake 0.5s ease-in-out;
        }

        .powerup-indicator {
            position: absolute;
            top: 60px;
            left: 10px;
            background: rgba(255, 215, 0, 0.8);
            color: #000;
            padding: 5px 10px;
            border-radius: 15px;
            font-size: 11px;
            font-weight: 700;
            display: none;
        }
    </style>
</head>
<body>
    <div class="game-container">
        <canvas id="gameCanvas" width="1000" height="600"></canvas>
        
        <!-- HUD -->
        <div class="hud">
            <div class="hud-left">
                <div class="score">PONTOS: <span id="score">0</span></div>
                <div>NÍVEL: <span id="level">1</span></div>
                <div>VIDA:</div>
                <div class="health-bar">
                    <div class="health-fill" id="healthFill"></div>
                </div>
            </div>
            <div class="hud-right">
                <div>VELOCIDADE: <span id="speed">100</span> km/h</div>
                <div>COMBUSTÍVEL: <span id="fuel">100</span>%</div>
                <div>RECORDE: <span id="highScore">0</span></div>
            </div>
        </div>

        <!-- Power-up Indicator -->
        <div class="powerup-indicator" id="powerupIndicator">
            ESCUDO ATIVO! 🛡️
        </div>

        <!-- Controles -->
        <div class="controls">
            🎮 ↑↓ Altitude | ESPAÇO Turbo | R Reiniciar
        </div>

        <!-- Tela Inicial -->
        <div class="start-screen" id="startScreen">
            <h1>✈️ SKY RUNNER</h1>
            <div style="text-align: center; margin-bottom: 30px; color: #ccc;">
                <p>Voe pelo céu perigoso!</p>
                <p>Desvie de obstáculos, colete power-ups e sobreviva!</p>
            </div>
            <button class="start-btn" onclick="startGame()">INICIAR JOGO</button>
        </div>

        <!-- Game Over -->
        <div class="game-over" id="gameOver" style="display: none;">
            <h1>💥 GAME OVER</h1>
            <div class="final-score">Pontuação Final: <span id="finalScore">0</span></div>
            <div style="color: #ccc; margin-bottom: 20px;">
                <span id="gameOverReason">Você colidiu!</span>
            </div>
            <button class="restart-btn" onclick="restartGame()">JOGAR NOVAMENTE</button>
        </div>
    </div>

    <script>
        // Canvas e contexto
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        
        // Elementos da interface
        const elements = {
            score: document.getElementById('score'),
            level: document.getElementById('level'),
            speed: document.getElementById('speed'),
            fuel: document.getElementById('fuel'),
            highScore: document.getElementById('highScore'),
            healthFill: document.getElementById('healthFill'),
            startScreen: document.getElementById('startScreen'),
            gameOver: document.getElementById('gameOver'),
            finalScore: document.getElementById('finalScore'),
            gameOverReason: document.getElementById('gameOverReason'),
            powerupIndicator: document.getElementById('powerupIndicator')
        };

        // Estado do jogo
        let gameState = 'start'; // 'start', 'playing', 'gameOver'
        let gameSpeed = 3;
        let score = 0;
        let level = 1;
        let health = 100;
        let fuel = 100;
        let highScore = parseInt(localStorage.getItem('skyRunnerHighScore') || '0');
        
        // Configurações do jogo
        const GAME_WIDTH = canvas.width;
        const GAME_HEIGHT = canvas.height;
        const GROUND_HEIGHT = 120;

        // Jogador (avião)
        const player = {
            x: 100,
            y: GAME_HEIGHT / 2,
            width: 40,
            height: 20,
            speed: 5,
            turboSpeed: 8,
            isTurbo: false,
            shield: false,
            shieldTime: 0
        };

        // Arrays de objetos do jogo
        let obstacles = [];
        let powerups = [];
        let particles = [];
        let clouds = [];

        // Controles
        const keys = {
            up: false,
            down: false,
            space: false
        };

        // Inicializar nuvens
        function initClouds() {
            clouds = [];
            for (let i = 0; i < 8; i++) {
                clouds.push({
                    x: Math.random() * GAME_WIDTH * 2,
                    y: 50 + Math.random() * 200,
                    size: 15 + Math.random() * 25,
                    speed: 0.5 + Math.random() * 1.5,
                    opacity: 0.3 + Math.random() * 0.4
                });
            }
        }

        // Classe para obstáculos
        class Obstacle {
            constructor(x, y, width, height, type = 'mountain') {
                this.x = x;
                this.y = y;
                this.width = width;
                this.height = height;
                this.type = type;
                this.passed = false;
            }

            update() {
                this.x -= gameSpeed;
            }

            draw() {
                if (this.type === 'mountain') {
                    // Montanha/Rocha
                    ctx.fillStyle = '#654321';
                    ctx.fillRect(this.x, this.y, this.width, this.height);
                    ctx.fillStyle = '#8B4513';
                    ctx.fillRect(this.x, this.y, this.width, 10);
                } else if (this.type === 'bird') {
                    // Pássaro hostil
                    ctx.fillStyle = '#8B0000';
                    ctx.beginPath();
                    ctx.ellipse(this.x + this.width/2, this.y + this.height/2, 
                               this.width/2, this.height/2, 0, 0, Math.PI * 2);
                    ctx.fill();
                    // Asas
                    ctx.fillStyle = '#A0522D';
                    ctx.fillRect(this.x - 5, this.y + 5, 15, 3);
                    ctx.fillRect(this.x + this.width - 10, this.y + 5, 15, 3);
                } else if (this.type === 'missile') {
                    // Míssil
                    ctx.fillStyle = '#FF4500';
                    ctx.fillRect(this.x, this.y, this.width, this.height);
                    ctx.fillStyle = '#FF0000';
                    ctx.fillRect(this.x, this.y + 2, this.width - 5, this.height - 4);
                    // Rastro de fogo
                    for (let i = 0; i < 5; i++) {
                        ctx.fillStyle = `rgba(255, ${100 + i * 30}, 0, ${0.8 - i * 0.15})`;
                        ctx.fillRect(this.x - i * 8, this.y + 3, 8, this.height - 6);
                    }
                }
            }

            isOffScreen() {
                return this.x + this.width < 0;
            }

            checkCollision(rect) {
                return this.x < rect.x + rect.width &&
                       this.x + this.width > rect.x &&
                       this.y < rect.y + rect.height &&
                       this.y + this.height > rect.y;
            }
        }

        // Classe para power-ups
        class PowerUp {
            constructor(x, y, type) {
                this.x = x;
                this.y = y;
                this.width = 25;
                this.height = 25;
                this.type = type;
                this.collected = false;
                this.bobOffset = Math.random() * Math.PI * 2;
            }

            update() {
                this.x -= gameSpeed;
                this.bobOffset += 0.1;
            }

            draw() {
                const bobY = this.y + Math.sin(this.bobOffset) * 3;
                
                if (this.type === 'health') {
                    // Kit médico
                    ctx.fillStyle = '#FF0000';
                    ctx.fillRect(this.x, bobY, this.width, this.height);
                    ctx.fillStyle = '#FFFFFF';
                    ctx.fillRect(this.x + 8, bobY + 5, this.width - 16, 15);
                    ctx.fillRect(this.x + 5, bobY + 8, this.width - 10, 9);
                } else if (this.type === 'fuel') {
                    // Combustível
                    ctx.fillStyle = '#32CD32';
                    ctx.fillRect(this.x, bobY, this.width, this.height);
                    ctx.fillStyle = '#00FF00';
                    ctx.fillRect(this.x + 2, bobY + 2, this.width - 4, this.height - 4);
                } else if (this.type === 'shield') {
                    // Escudo
                    ctx.fillStyle = '#4169E1';
                    ctx.beginPath();
                    ctx.arc(this.x + this.width/2, bobY + this.height/2, this.width/2, 0, Math.PI * 2);
                    ctx.fill();
                    ctx.strokeStyle = '#00BFFF';
                    ctx.lineWidth = 3;
                    ctx.stroke();
                } else if (this.type === 'points') {
                    // Pontos extras
                    ctx.fillStyle = '#FFD700';
                    ctx.beginPath();
                    // Estrela
                    const centerX = this.x + this.width/2;
                    const centerY = bobY + this.height/2;
                    const spikes = 5;
                    const outerRadius = this.width/2;
                    const innerRadius = outerRadius * 0.5;
                    
                    ctx.moveTo(centerX, centerY - outerRadius);
                    for (let i = 0; i < spikes * 2; i++) {
                        const radius = i % 2 === 0 ? outerRadius : innerRadius;
                        const angle = (i * Math.PI) / spikes - Math.PI/2;
                        ctx.lineTo(centerX + Math.cos(angle) * radius, 
                                  centerY + Math.sin(angle) * radius);
                    }
                    ctx.closePath();
                    ctx.fill();
                }
            }

            isOffScreen() {
                return this.x + this.width < 0;
            }

            checkCollision(rect) {
                return this.x < rect.x + rect.width &&
                       this.x + this.width > rect.x &&
                       this.y < rect.y + rect.height &&
                       this.y + this.height > rect.y;
            }
        }

        // Classe para partículas de efeito
        class Particle {
            constructor(x, y, color, size, speedX, speedY, life) {
                this.x = x;
                this.y = y;
                this.color = color;
                this.size = size;
                this.speedX = speedX;
                this.speedY = speedY;
                this.life = life;
                this.maxLife = life;
            }

            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                this.life--;
                this.size *= 0.98;
            }

            draw() {
                const alpha = this.life / this.maxLife;
                ctx.save();
                ctx.globalAlpha = alpha;
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
                ctx.restore();
            }

            isDead() {
                return this.life <= 0 || this.size < 0.5;
            }
        }

        // Criar explosão de partículas
        function createExplosion(x, y, color, count = 10) {
            for (let i = 0; i < count; i++) {
                const angle = (Math.PI * 2 * i) / count;
                const speed = 2 + Math.random() * 4;
                particles.push(new Particle(
                    x, y, color,
                    3 + Math.random() * 5,
                    Math.cos(angle) * speed,
                    Math.sin(angle) * speed,
                    30 + Math.random() * 20
                ));
            }
        }

        // Gerar obstáculos
        function spawnObstacle() {
            const types = ['mountain', 'bird', 'missile'];
            const type = types[Math.floor(Math.random() * types.length)];
            
            let width, height, y;
            
            if (type === 'mountain') {
                width = 40 + Math.random() * 60;
                height = 80 + Math.random() * 120;
                y = GAME_HEIGHT - GROUND_HEIGHT - height;
            } else if (type === 'bird') {
                width = 25;
                height = 15;
                y = 100 + Math.random() * 300;
            } else if (type === 'missile') {
                width = 30;
                height = 10;
                y = 50 + Math.random() * 400;
            }
            
            obstacles.push(new Obstacle(GAME_WIDTH, y, width, height, type));
        }

        // Gerar power-ups
        function spawnPowerUp() {
            const types = ['health', 'fuel', 'shield', 'points'];
            const type = types[Math.floor(Math.random() * types.length)];
            const y = 100 + Math.random() * 350;
            
            powerups.push(new PowerUp(GAME_WIDTH, y, type));
        }

        // Desenhar nuvens
        function drawClouds() {
            clouds.forEach(cloud => {
                ctx.save();
                ctx.globalAlpha = cloud.opacity;
                ctx.fillStyle = '#FFFFFF';
                
                ctx.beginPath();
                ctx.arc(cloud.x, cloud.y, cloud.size, 0, Math.PI * 2);
                ctx.arc(cloud.x + cloud.size * 0.8, cloud.y, cloud.size * 0.8, 0, Math.PI * 2);
                ctx.arc(cloud.x + cloud.size * 1.6, cloud.y, cloud.size, 0, Math.PI * 2);
                ctx.fill();
                
                cloud.x -= cloud.speed;
                if (cloud.x < -cloud.size * 2) {
                    cloud.x = GAME_WIDTH + cloud.size;
                }
                
                ctx.restore();
            });
        }

        // Desenhar jogador
        function drawPlayer() {
            const x = player.x;
            const y = player.y;
            
            // Escudo
            if (player.shield) {
                ctx.strokeStyle = '#00BFFF';
                ctx.lineWidth = 3;
                ctx.beginPath();
                ctx.arc(x + player.width/2, y + player.height/2, 35, 0, Math.PI * 2);
                ctx.stroke();
                
                ctx.strokeStyle = '#4169E1';
                ctx.lineWidth = 1;
                ctx.beginPath();
                ctx.arc(x + player.width/2, y + player.height/2, 32, 0, Math.PI * 2);
                ctx.stroke();
            }
            
            // Corpo do avião
            ctx.fillStyle = player.isTurbo ? '#FF6B6B' : '#FF4757';
            ctx.beginPath();
            ctx.moveTo(x + player.width, y + player.height/2);
            ctx.lineTo(x, y);
            ctx.lineTo(x, y + player.height);
            ctx.closePath();
            ctx.fill();
            
            // Asas
            ctx.fillStyle = '#E17055';
            ctx.fillRect(x + 5, y - 8, 25, 6);
            ctx.fillRect(x + 5, y + player.height + 2, 25, 6);
            
            // Cauda
            ctx.fillStyle = '#FF6B6B';
            ctx.fillRect(x - 8, y + 5, 12, 10);
            
            // Turbo effect
            if (player.isTurbo) {
                for (let i = 0; i < 8; i++) {
                    particles.push(new Particle(
                        x - 10 - Math.random() * 20,
                        y + player.height/2 + (Math.random() - 0.5) * 15,
                        `hsl(${20 + Math.random() * 40}, 100%, 60%)`,
                        2 + Math.random() * 3,
                        -3 - Math.random() * 2,
                        (Math.random() - 0.5) * 4,
                        15 + Math.random() * 10
                    ));
                }
            }
        }

        // Event listeners
        document.addEventListener('keydown', (e) => {
            switch(e.key) {
                case 'ArrowUp':
                    keys.up = true;
                    e.preventDefault();
                    break;
                case 'ArrowDown':
                    keys.down = true;
                    e.preventDefault();
                    break;
                case ' ':
                    keys.space = true;
                    e.preventDefault();
                    break;
                case 'r':
                case 'R':
                    if (gameState === 'gameOver') restartGame();
                    break;
            }
        });

        document.addEventListener('keyup', (e) => {
            switch(e.key) {
                case 'ArrowUp':
                    keys.up = false;
                    break;
                case 'ArrowDown':
                    keys.down = false;
                    break;
                case ' ':
                    keys.space = false;
                    player.isTurbo = false;
                    break;
            }
        });

        // Atualizar jogador
        function updatePlayer() {
            const speed = keys.space && fuel > 0 ? player.turboSpeed : player.speed;
            
            if (keys.up && player.y > 0) {
                player.y -= speed;
            }
            if (keys.down && player.y < GAME_HEIGHT - GROUND_HEIGHT - player.height) {
                player.y += speed;
            }
            
            // Turbo
            if (keys.space && fuel > 0) {
                player.isTurbo = true;
                fuel -= 0.5;
                if (fuel < 0) fuel = 0;
            } else {
                player.isTurbo = false;
                if (fuel < 100) fuel += 0.1;
            }
            
            // Escudo
            if (player.shield) {
                player.shieldTime--;
                if (player.shieldTime <= 0) {
                    player.shield = false;
                    elements.powerupIndicator.style.display = 'none';
                }
            }
            
            // Consumo de combustível natural
            fuel -= 0.02;
            if (fuel <= 0) {
                fuel = 0;
                takeDamage(1, 'Combustível esgotado!');
            }
        }

        // Sistema de dano
        function takeDamage(amount, reason) {
            if (player.shield) return;
            
            health -= amount;
            canvas.parentElement.classList.add('shake');
            setTimeout(() => canvas.parentElement.classList.remove('shake'), 500);
            
            createExplosion(player.x + player.width/2, player.y + player.height/2, '#FF0000', 15);
            
            if (health <= 0) {
                gameOver(reason);
            }
        }

        // Coletar power-up
        function collectPowerUp(powerup) {
            createExplosion(powerup.x + powerup.width/2, powerup.y + powerup.height/2, '#FFD700', 8);
            
            switch(powerup.type) {
                case 'health':
                    health = Math.min(100, health + 25);
                    break;
                case 'fuel':
                    fuel = Math.min(100, fuel + 30);
                    break;
                case 'shield':
                    player.shield = true;
                    player.shieldTime = 300; // 5 segundos
                    elements.powerupIndicator.style.display = 'block';
                    break;
                case 'points':
                    score += 100;
                    break;
            }
        }

        // Atualizar jogo
        function updateGame() {
            if (gameState !== 'playing') return;
            
            updatePlayer();
            
            // Atualizar obstáculos
            obstacles.forEach((obstacle, index) => {
                obstacle.update();
                
                if (obstacle.checkCollision(player)) {
                    takeDamage(20, 'Colidiu com obstáculo!');
                    obstacles.splice(index, 1);
                } else if (!obstacle.passed && obstacle.x + obstacle.width < player.x) {
                    obstacle.passed = true;
                    score += 10;
                }
                
                if (obstacle.isOffScreen()) {
                    obstacles.splice(index, 1);
                }
            });
            
            // Atualizar power-ups
            powerups.forEach((powerup, index) => {
                powerup.update();
                
                if (powerup.checkCollision(player)) {
                    collectPowerUp(powerup);
                    powerups.splice(index, 1);
                }
                
                if (powerup.isOffScreen()) {
                    powerups.splice(index, 1);
                }
            });
            
            // Atualizar partículas
            particles.forEach((particle, index) => {
                particle.update();
                if (particle.isDead()) {
                    particles.splice(index, 1);
                }
            });
            
            // Spawn de obstáculos e power-ups
            if (Math.random() < 0.02 + level * 0.005) {
                spawnObstacle();
            }
            
            if (Math.random() < 0.008) {
                spawnPowerUp();
            }
            
            // Aumentar dificuldade
            if (score > level * 500) {
                level++;
                gameSpeed += 0.5;
            }
            
            // Regeneração lenta de vida
            if (health < 100 && Math.random() < 0.005) {
                health += 1;
            }
            
            // Atualizar interface
            updateHUD();
        }

        // Atualizar HUD
        function updateHUD() {
            elements.score.textContent = score;
            elements.level.textContent = level;
            elements.speed.textContent = Math.round(gameSpeed * 33.33);
            elements.fuel.textContent = Math.round(fuel);
            elements.healthFill.style.width = health + '%';
            elements.highScore.textContent = highScore;
        }

        // Renderizar jogo
        function renderGame() {
            // Limpar canvas
            ctx.clearRect(0, 0, GAME_WIDTH, GAME_HEIGHT);
            
            // Desenhar nuvens
            drawClouds();
            
            // Desenhar linha do horizonte
            ctx.strokeStyle = '#2D5016';
            ctx.lineWidth = 3;
            ctx.beginPath();
            ctx.moveTo(0, GAME_HEIGHT - GROUND_HEIGHT);
            ctx.lineTo(GAME_WIDTH, GAME_HEIGHT - GROUND_HEIGHT);
            ctx.stroke();
            
            // Desenhar obstáculos
            obstacles.forEach(obstacle => obstacle.draw());
            
            // Desenhar power-ups
            powerups.forEach(powerup => powerup.draw());
            
            // Desenhar partículas
            particles.forEach(particle => particle.draw());
            
            // Desenhar jogador
            if (gameState === 'playing') {
                drawPlayer();
            }
        }

        // Game Over
        function gameOver(reason) {
            gameState = 'gameOver';
            
            if (score > highScore) {
                highScore = score;
                localStorage.setItem('skyRunnerHighScore', highScore.toString());
            }
            
            elements.finalScore.textContent = score;
            elements.gameOverReason.textContent = reason;
            elements.gameOver.style.display = 'flex';
        }

        //
