<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pixel Brawlers - Impact Edition</title>
    <style>
        * { box-sizing: border-box; }
        body, html {
            margin: 0; padding: 0; width: 100%; height: 100%;
            background: #050508; color: #fff;
            font-family: 'Courier New', Courier, monospace;
            overflow: hidden; user-select: none;
        }
        #game-container { position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; image-rendering: pixelated; }
        canvas { display: block; width: 100%; height: 100%; }
        .overlay { position: absolute; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.95); display: flex; flex-direction: column; justify-content: center; align-items: center; z-index: 10; }
        .hidden { display: none !important; }
        
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 10px; margin-top: 20px; width: 95%; max-width: 1200px; max-height: 70vh; overflow-y: auto; padding: 15px; border: 1px solid #333; background: #111; }
        .card { background: #1a1a1a; padding: 12px; border: 2px solid #444; cursor: pointer; text-align: center; transition: 0.2s; border-radius: 4px; }
        .card:hover { border-color: #00ffcc; background: #252525; transform: scale(1.02); }
        .selected { border-color: #fcc419 !important; background: #333 !important; }

        .type-tag { font-size: 10px; font-weight: bold; margin-top: 5px; display: block; letter-spacing: 1px; }
        .tag-ranged { color: #00ffcc; }
        .tag-melee { color: #ff3e3e; }

        #hud { position: absolute; top: 20px; width: 100%; display: flex; justify-content: space-between; padding: 0 40px; pointer-events: none; }
        .bar-container { width: 32%; }
        .hp-bar { height: 24px; background: #222; border: 2px solid #fff; position: relative; overflow: hidden; }
        .hp-fill { height: 100%; background: #ff3e3e; transition: width 0.2s; }
        .super-bar { height: 10px; background: #111; border: 1px solid #555; margin-top: 6px; }
        .super-fill { height: 100%; background: #fcc419; width: 0%; box-shadow: 0 0 8px #fcc419; }
        .ammo-status { font-size: 13px; margin-top: 6px; font-weight: bold; text-shadow: 1px 1px #000; }
        
        button { font-family: inherit; padding: 18px 45px; cursor:pointer; font-size: 24px; background: #00ffcc; border:none; font-weight:bold; clip-path: polygon(10% 0, 100% 0, 90% 100%, 0 100%); transition: 0.2s; }
        button:hover { background: #fff; color: #000; transform: scale(1.05); }

        #victory-screen h1 { font-size: 80px; margin: 0; color: #fcc419; text-shadow: 0 0 20px rgba(252, 196, 25, 0.5); }
    </style>
</head>
<body>

    <div id="game-container">
        <canvas id="gameCanvas"></canvas>
        
        <div id="menu" class="overlay">
            <h1 style="font-size: 60px; color: #00ffcc; text-shadow: 4px 4px #7048e8;">PIXEL BRAWLERS</h1>
            <button onclick="showCharSelection()">ENTER ARENA</button>
        </div>

        <div id="char-selection" class="overlay hidden">
            <h2 id="selection-title">P1: SELECT HERO</h2>
            <div class="grid" id="char-grid"></div>
        </div>

        <div id="map-selection" class="overlay hidden">
            <h2>SELECT BATTLEGROUND</h2>
            <div class="grid" id="map-grid"></div>
        </div>

        <div id="victory-screen" class="overlay hidden">
            <h1 id="winner-text">P1 WINS!</h1>
            <button onclick="resetToMenu()">RETURN TO MENU</button>
        </div>

        <div id="hud" class="hidden">
            <div class="bar-container">
                <div id="p1-name" style="color:#00ffcc;">P1</div>
                <div class="hp-bar"><div id="p1-hp" class="hp-fill"></div></div>
                <div class="super-bar"><div id="p1-super" class="super-fill"></div></div>
                <div id="p1-ammo" class="ammo-status" style="color:#00ffcc;"></div>
            </div>
            <div class="bar-container" style="text-align:right;">
                <div id="p2-name" style="color:#7048e8;">P2</div>
                <div class="hp-bar"><div id="p2-hp" class="hp-fill"></div></div>
                <div class="super-bar"><div id="p2-super" class="super-fill"></div></div>
                <div id="p2-ammo" class="ammo-status" style="color:#7048e8;"></div>
            </div>
        </div>
    </div>

<script>
    const canvas = document.getElementById('gameCanvas');
    const ctx = canvas.getContext('2d');
    let W, H, GROUND_Y, P_SCALE;

    function initLayout() {
        W = canvas.width = window.innerWidth;
        H = canvas.height = window.innerHeight;
        GROUND_Y = H * 0.85;
        P_SCALE = Math.max(4, Math.min(W / 180, H / 100));
    }
    window.addEventListener('resize', initLayout);
    initLayout();

    const COLORS = { P:'#7048e8', S:'#ced4da', K:'#ffd8a8', X:'#111', W:'#f8f9fa', r:'#e03131', y:'#fcc419', G:'#495057', B:'#1971c2', V:'#5f0a0a', L:'#74c0fc', M:'#2b8a3e', O:'#e67e22', D:'#343a40' };
    
    const PIXELS = {
        wizard: ["  PPPP  "," PPPPPP "," PPSKPP ","  KKK   "," PPPPPP "," P BBBB "," P BBBB "," PP  PP "],
        tank:   [" SSSSS  "," SSSSS  "," SKS S  "," SSSSS  "," SSSSS  "," SSSSS  "," SSSSS  "," SS  SS "],
        gunner: [" GGGGG  "," GKKKG  "," GGGGG  ","  KKK   "," BBBBB  "," BBBBS  "," BBBBS  "," BB  BB "],
        ninja:  ["  XXXX  "," XXXXXX "," XK XK  ","  XXX   "," XXXXX  "," XXXXX  "," XXXXX  "," XX  XX "],
        blaze:  ["  rrr   "," rrrrr  "," rKSKr  ","  rrr   "," rOrOr  "," rrrrr  "," rrrrr  "," rr  rr "],
        reaper: ["  XXXX  "," XXXXX  "," XGXGX  ","  GGG   "," XXXXXX "," XXXXX  "," XXXXX  "," X    X "],
        medic:  ["  WWWW  "," WWWWW  "," WKWKW  ","  KKK   "," WWWWW  "," WWrWW  "," WWWWW  "," WW  WW "],
        archer: ["  MMMM  "," MMMMMM "," MSKSM  ","  KKK   "," MMMMMM "," MMMMM  "," MMMMM  "," MM  MM "],
        vampire:["  VVVV  "," VVVVV  "," VKSKV  ","  KKK   "," XXXXXX "," X V X  "," X V X  "," X    X "],
        storm:  ["  WWWW  "," WWWWWW "," WSKSW  ","  LLL   "," LLLLLL "," LLLLLL "," LLLLLL "," LL  LL "],
        paladin:["  SSSS  "," SSSSS  "," SSKSW  ","  SSS   "," SSSSS  "," SOSSOS "," SSSSS  "," SS  SS "],
        bomber: ["  GGGG  "," GGGGG  "," GKXKG  ","  GGG   "," DDDDDD "," DDDDDD "," DDDDDD "," DD  DD "],
        ghost:  ["  WWWW  "," WWWWW  "," W B B  ","  WWW   "," WWWWWW "," WWWWW  "," WWWWW  "," W    W "],
        punch:  ["        ","  KKKK  "," KKKKKK "," KKKKKK "," KKKKKK ","  KKKK  ","        ","        "]
    };

    const CLASSES = {
        wizard: { hp: 100, speed: 1.3, type: 'ranged', dmg: 3,  cd: 22 },
        tank:   { hp: 240, speed: 0.7, type: 'melee',  dmg: 18, cd: 60 },
        gunner: { hp: 100, speed: 1.6, type: 'ranged', dmg: 5,  cd: 12 },
        ninja:  { hp: 85,  speed: 2.2, type: 'melee',  dmg: 9,  cd: 15 },
        blaze:  { hp: 110, speed: 1.2, type: 'ranged', dmg: 14, cd: 35 },
        reaper: { hp: 120, speed: 1.1, type: 'ranged', dmg: 22, cd: 55 },
        medic:  { hp: 150, speed: 1.7, type: 'ranged', dmg: 3,  cd: 10 },
        archer: { hp: 90,  speed: 1.5, type: 'ranged', dmg: 7,  cd: 18 },
        vampire:{ hp: 110, speed: 1.4, type: 'melee',  dmg: 12, cd: 25 },
        storm:  { hp: 100, speed: 1.5, type: 'ranged', dmg: 4,  cd: 12 },
        paladin:{ hp: 190, speed: 0.9, type: 'melee',  dmg: 15, cd: 40 },
        bomber: { hp: 120, speed: 1.1, type: 'ranged', dmg: 20, cd: 50 },
        ghost:  { hp: 80,  speed: 1.9, type: 'melee',  dmg: 11, cd: 20 }
    };

    const MAPS = {
        void:    { name: "The Void", bg: "#0d0d16", ground: "#161625", accent: "#333", effect: 'none' },
        volcano: { name: "Magma Chamber", bg: "#2b0a0a", ground: "#4a0000", accent: "#ff4500", effect: 'embers' },
        forest:  { name: "Deep Woods", bg: "#0a1a0a", ground: "#1a2e1a", accent: "#2b8a3e", effect: 'leaves' },
        cyber:   { name: "Neon City", bg: "#0a0a1a", ground: "#001a33", accent: "#00f2ff", effect: 'rain' },
        desert:  { name: "Dust Bowl", bg: "#2e251a", ground: "#3d3224", accent: "#d4a373", effect: 'dust' },
        glacier: { name: "Glacier Peak", bg: "#1a2b3c", ground: "#ffffff", accent: "#74c0fc", effect: 'snow' },
        toxic:   { name: "Toxic Lab", bg: "#0a1a0a", ground: "#1a3a1a", accent: "#a6e22e", effect: 'bubbles' },
        night:   { name: "Midnight Roof", bg: "#1a0a25", ground: "#251a35", accent: "#7048e8", effect: 'none' },
        temple:  { name: "Golden Temple", bg: "#3a1a1a", ground: "#fcc419", accent: "#e03131", effect: 'none' },
        hive:    { name: "The Hive", bg: "#1a1a05", ground: "#222", accent: "#fcc419", effect: 'none' },
        deep:    { name: "Deep Sea", bg: "#051a25", ground: "#0a2a35", accent: "#1971c2", effect: 'bubbles' }
    };

    let gameState = 'MENU', p1, p2, currentMap = MAPS.void;
    let projectiles = [], particles = [], envParticles = [], keys = {}, selectingPlayer = 1, selectedP1 = null;
    let screenShake = 0, flash = 0;

    function showCharSelection() {
        selectingPlayer = 1; selectedP1 = null;
        document.getElementById('menu').classList.add('hidden');
        document.getElementById('victory-screen').classList.add('hidden');
        document.getElementById('char-selection').classList.remove('hidden');
        const grid = document.getElementById('char-grid'); grid.innerHTML = '';
        Object.keys(CLASSES).forEach(key => {
            const data = CLASSES[key];
            const card = document.createElement('div'); card.className = 'card';
            const typeClass = data.type === 'ranged' ? 'tag-ranged' : 'tag-melee';
            card.innerHTML = `<strong>${key.toUpperCase()}</strong><span class="type-tag ${typeClass}">[${data.type.toUpperCase()}]</span>`;
            card.onclick = () => {
                if (selectingPlayer === 1) { selectedP1 = key; selectingPlayer = 2; card.classList.add('selected'); document.getElementById('selection-title').innerText = "P2: SELECT HERO"; }
                else { showMapSelection(selectedP1, key); }
            };
            grid.appendChild(card);
        });
    }

    function showMapSelection(c1, c2) {
        document.getElementById('char-selection').classList.add('hidden');
        document.getElementById('map-selection').classList.remove('hidden');
        const grid = document.getElementById('map-grid'); grid.innerHTML = '';
        Object.keys(MAPS).forEach(key => {
            const card = document.createElement('div'); card.className = 'card';
            card.style.borderLeft = `8px solid ${MAPS[key].accent}`;
            card.innerHTML = `<strong>${MAPS[key].name}</strong>`;
            card.onclick = () => { currentMap = MAPS[key]; startMatch(c1, c2); };
            grid.appendChild(card);
        });
    }

    function startMatch(c1, c2) {
        projectiles = []; particles = []; envParticles = [];
        p1 = new Player(W*0.2, GROUND_Y-50, 1, c1); p2 = new Player(W*0.8, GROUND_Y-50, 2, c2);
        document.getElementById('map-selection').classList.add('hidden');
        document.getElementById('hud').classList.remove('hidden');
        document.getElementById('p1-name').innerText = c1.toUpperCase();
        document.getElementById('p2-name').innerText = c2.toUpperCase();
        gameState = 'PLAYING';
    }

    function resetToMenu() {
        gameState = 'MENU';
        document.getElementById('victory-screen').classList.add('hidden');
        document.getElementById('hud').classList.add('hidden');
        document.getElementById('menu').classList.remove('hidden');
    }

    class Player {
        constructor(x, y, id, classKey) {
            this.id = id; this.classKey = classKey; this.x = x; this.y = y;
            const data = CLASSES[classKey];
            this.hp = data.hp; this.maxHp = data.hp; 
            this.speed = data.speed * (W/500); 
            this.w = P_SCALE * 8; this.h = P_SCALE * 8; this.vx = 0; this.vy = 0;
            this.facing = id === 1 ? 1 : -1; this.grounded = false;
            this.superMeter = 0; this.atkCD = 0; this.shotsFired = 0; this.isReloading = false;
            this.frozen = 0; this.shield = 0; this.invis = 0; this.type = data.type;
            this.punchFrame = 0;
        }

        update(opp) {
            if (this.frozen > 0) { this.frozen--; return; }
            this.facing = (opp.x > this.x) ? 1 : -1;
            const isP1 = this.id === 1;
            const l = isP1 ? keys['a'] : keys['arrowleft'], r = isP1 ? keys['d'] : keys['arrowright'],
                  j = isP1 ? keys['w'] : keys['arrowup'], a = isP1 ? keys['f'] : keys['arrowdown'],
                  s = isP1 ? keys['s'] : keys['shift'];

            if (l) this.vx = -this.speed; else if (r) this.vx = this.speed; else this.vx = 0;
            if (j && this.grounded) { this.vy = -16; this.grounded = false; }
            if (a && this.atkCD <= 0 && !this.isReloading) this.attack(opp);
            if (s && this.superMeter >= 100) this.useSuper(opp);

            this.vy += 0.7; this.x += this.vx; this.y += this.vy;
            if (this.y >= GROUND_Y - this.h) { this.y = GROUND_Y - this.h; this.vy = 0; this.grounded = true; }
            this.x = Math.max(0, Math.min(W - this.w, this.x));
            if (this.atkCD > 0) this.atkCD--;
            if (this.superMeter < 100) this.superMeter += 0.0556;
            if (this.shield > 0) this.shield--;
            if (this.invis > 0) this.invis--;
            if (this.punchFrame > 0) this.punchFrame--;
        }

        attack(opp) {
            const data = CLASSES[this.classKey];
            if (this.type === 'ranged') {
                projectiles.push({ x: this.x + (this.facing === 1 ? this.w : -15), y: this.y + this.h/3, vx: this.facing * 14, owner: this.id, dmg: data.dmg, c: this.classKey });
                this.shotsFired++;
                if (this.shotsFired >= 10) { this.isReloading = true; setTimeout(() => { this.shotsFired = 0; this.isReloading = false; }, 3000); }
            } else {
                this.punchFrame = 10;
                if (Math.abs(this.x - opp.x) < this.w * 2.5 && Math.abs(this.y - opp.y) < this.h) {
                    opp.takeHit(data.dmg);
                    if (this.classKey === 'vampire') this.hp = Math.min(this.maxHp, this.hp + 4);
                }
            }
            this.atkCD = data.cd;
        }

        useSuper(opp) {
            this.superMeter = 0;
            screenShake = 15;
            flash = 5;
            if (this.classKey === 'wizard') opp.frozen = 180;
            else if (this.classKey === 'paladin') this.shield = 400;
            else if (this.classKey === 'ninja' || this.classKey === 'ghost') this.invis = 400;
            else if (this.classKey === 'tank') { if(Math.abs(this.x-opp.x)<250) opp.takeHit(55); }
            else if (this.classKey === 'storm') { opp.takeHit(45); createParticles(opp.x, opp.y, '#74c0fc'); }
            else if (this.classKey === 'medic') this.hp = Math.min(this.maxHp, this.hp + 60);
            else { projectiles.push({ x: this.x, y: this.y + this.h/2, vx: this.facing * 22, owner: this.id, dmg: 50, c: 'super' }); }
        }

        takeHit(dmg) { 
            if (this.shield > 0 || (this.invis > 0 && this.classKey === 'ghost')) return; 
            this.hp -= dmg; 
            screenShake = 5;
            createParticles(this.x+this.w/2, this.y+this.h/2, 'red', 12); 
        }

        draw() {
            let op = this.invis > 0 ? 0.2 : 1;
            drawPixelArt(this.x, this.y, PIXELS[this.classKey], P_SCALE, this.facing === -1, op);
            if (this.punchFrame > 0) {
                const px = this.facing === 1 ? this.x + this.w : this.x - (P_SCALE*8);
                drawPixelArt(px, this.y + (P_SCALE*2), PIXELS.punch, P_SCALE, this.facing === -1, 1);
            }
            if (this.shield > 0) { ctx.strokeStyle = '#fcc419'; ctx.lineWidth = 3; ctx.strokeRect(this.x-4, this.y-4, this.w+8, this.h+8); }
        }
    }

    function drawPixelArt(x, y, arr, scale, flip, op) {
        ctx.save(); ctx.globalAlpha = op; ctx.translate(x + (flip ? scale*8 : 0), y); if(flip) ctx.scale(-1, 1);
        arr.forEach((row, r) => { row.split('').forEach((char, c) => { if(char!==' '){ ctx.fillStyle=COLORS[char] || '#fff'; ctx.fillRect(c*scale, r*scale, scale, scale); } }); });
        ctx.restore();
    }

    function createParticles(x, y, color, count=8) { for(let i=0; i<count; i++) particles.push({x, y, vx:(Math.random()-0.5)*12, vy:(Math.random()-0.5)*12, life:25, color}); }

    function handleEnvEffects() {
        if (Math.random() > 0.9) {
            if (currentMap.effect === 'snow') envParticles.push({x:Math.random()*W, y:-10, vx:(Math.random()-0.5)*2, vy:2+Math.random()*2, size:3, c:'#fff'});
            if (currentMap.effect === 'rain') envParticles.push({x:Math.random()*W, y:-10, vx:0, vy:10, size:2, c:'#74c0fc'});
            if (currentMap.effect === 'embers') envParticles.push({x:Math.random()*W, y:H, vx:(Math.random()-0.5)*4, vy:-(1+Math.random()*2), size:4, c:'#ff4500'});
            if (currentMap.effect === 'bubbles') envParticles.push({x:Math.random()*W, y:H, vx:0, vy:-(2+Math.random()*2), size:5, c:'rgba(255,255,255,0.3)'});
            if (currentMap.effect === 'leaves') envParticles.push({x:Math.random()*W, y:-10, vx:Math.random()*3, vy:2, size:6, c:'#2b8a3e'});
            if (currentMap.effect === 'dust') envParticles.push({x:W, y:GROUND_Y-Math.random()*100, vx:-5, vy:0, size:2, c:'#d4a373'});
        }
        envParticles.forEach((p, i) => {
            p.x += p.vx; p.y += p.vy;
            ctx.fillStyle = p.c;
            ctx.fillRect(p.x, p.y, p.size, p.size);
            if (p.y > H || p.y < -50 || p.x > W || p.x < -50) envParticles.splice(i, 1);
        });
    }

    function loop() {
        ctx.save();
        if (screenShake > 0) {
            ctx.translate((Math.random()-0.5)*screenShake, (Math.random()-0.5)*screenShake);
            screenShake *= 0.9;
            if (screenShake < 0.5) screenShake = 0;
        }

        ctx.fillStyle = currentMap.bg; ctx.fillRect(0, 0, W, H);
        handleEnvEffects();
        ctx.fillStyle = currentMap.ground; ctx.fillRect(0, GROUND_Y, W, H-GROUND_Y);
        ctx.fillStyle = currentMap.accent; ctx.fillRect(0, GROUND_Y, W, 4);

        if (gameState === 'PLAYING') {
            p1.update(p2); p2.update(p1); p1.draw(); p2.draw();
            projectiles.forEach((proj, i) => {
                proj.x += proj.vx; ctx.fillStyle = proj.c === 'super' ? '#fcc419' : '#fff'; ctx.fillRect(proj.x, proj.y, 12, 6);
                const opp = proj.owner === 1 ? p2 : p1;
                if (proj.x > opp.x && proj.x < opp.x+opp.w && proj.y > opp.y && proj.y < opp.y+opp.h) { opp.takeHit(proj.dmg); projectiles.splice(i, 1); }
                if (proj.x < -50 || proj.x > W+50) projectiles.splice(i, 1);
            });
            particles.forEach((part, i) => { part.x+=part.vx; part.y+=part.vy; part.life--; if(part.life<=0) particles.splice(i,1); ctx.fillStyle=part.color; ctx.fillRect(part.x, part.y, 4, 4); });
            document.getElementById('p1-hp').style.width = Math.max(0, (p1.hp/p1.maxHp)*100) + '%';
            document.getElementById('p2-hp').style.width = Math.max(0, (p2.hp/p2.maxHp)*100) + '%';
            document.getElementById('p1-super').style.width = Math.min(100, p1.superMeter) + '%';
            document.getElementById('p2-super').style.width = Math.min(100, p2.superMeter) + '%';
            if(p1.type === 'ranged') document.getElementById('p1-ammo').innerText = p1.isReloading ? "RELOADING" : `AMMO: ${10-p1.shotsFired}`;
            else document.getElementById('p1-ammo').innerText = "MELEE";
            if(p2.type === 'ranged') document.getElementById('p2-ammo').innerText = p2.isReloading ? "RELOADING" : `AMMO: ${10-p2.shotsFired}`;
            else document.getElementById('p2-ammo').innerText = "MELEE";
            if (p1.hp <= 0 || p2.hp <= 0) { gameState = 'OVER'; document.getElementById('winner-text').innerText = p1.hp <= 0 ? "P2 WINS!" : "P1 WINS!"; document.getElementById('victory-screen').classList.remove('hidden'); }
        } else if (gameState === 'OVER') { p1.draw(); p2.draw(); }
        
        if (flash > 0) {
            ctx.fillStyle = `rgba(255,255,255,${flash/10})`;
            ctx.fillRect(0,0,W,H);
            flash--;
        }
        ctx.restore();
        requestAnimationFrame(loop);
    }

    window.addEventListener('keydown', e => keys[e.key.toLowerCase()] = true);
    window.addEventListener('keyup', e => keys[e.key.toLowerCase()] = false);
    loop();
</script>
</body>
</html>
