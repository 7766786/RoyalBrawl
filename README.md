import * as THREE from 'three';
import './style.css';

const heroes = {
  RAVEN: {
    name: 'RAVEN',
    className: 'Shredder',
    hp: 4000,
    damage: 660,
    speed: 7.3,
    range: 34,
    reload: 1.2,
    weapon: 'ENERGY BLASTER',
    ability: 'DASH',
    ultimate: 'OVERDRIVE',
    color: '#66e2ff',
    accent: '#7f9bff',
    skinColors: {
      helmet: '#61d9ff',
      armor: '#4f7dff',
      sleeves: '#143d60',
      pants: '#1b2638',
      gloves: '#7fe4ff',
      weapon: '#8be5ff',
      glow: '#71dfff',
      energy: '#aef4ff'
    }
  },
  VOLT: {
    name: 'VOLT',
    className: 'Assaulter',
    hp: 3400,
    damage: 610,
    speed: 8.2,
    range: 28,
    reload: 1.0,
    weapon: 'VOLT PISTOL',
    ability: 'ELECTRO DASH',
    ultimate: 'ELECTRIC BURST',
    color: '#ffe26f',
    accent: '#f2ff3b',
    skinColors: {
      helmet: '#f9dc64',
      armor: '#e5d36a',
      sleeves: '#6e5f1a',
      pants: '#2b2f3d',
      gloves: '#ffef9a',
      weapon: '#f5f6ae',
      glow: '#fff2a8',
      energy: '#fff1a8'
    }
  },
  IRON: {
    name: 'IRON',
    className: 'Tank',
    hp: 5200,
    damage: 540,
    speed: 5.8,
    range: 26,
    reload: 1.5,
    weapon: 'HEAVY CANNON',
    ability: 'BARRIER DASH',
    ultimate: 'ENERGY SHIELD',
    color: '#d0d4db',
    accent: '#8ad4ff',
    skinColors: {
      helmet: '#dfe7f9',
      armor: '#7d93af',
      sleeves: '#394d62',
      pants: '#202c3d',
      gloves: '#c9d9f8',
      weapon: '#dfe9ff',
      glow: '#b2d6ff',
      energy: '#d9edff'
    }
  },
  FROST: {
    name: 'FROST',
    className: 'Controller',
    hp: 3600,
    damage: 590,
    speed: 6.8,
    range: 32,
    reload: 1.25,
    weapon: 'FROST BLASTER',
    ability: 'ICE DASH',
    ultimate: 'FREEZE ZONE',
    color: '#7fe2ff',
    accent: '#d4f2ff',
    skinColors: {
      helmet: '#b6e4ff',
      armor: '#8bc8ff',
      sleeves: '#2d526f',
      pants: '#1f2d40',
      gloves: '#dceaef',
      weapon: '#dcefff',
      glow: '#b0e8ff',
      energy: '#dbf6ff'
    }
  }
};

const maps = {
  'IRON VALLEY': {
    name: 'IRON VALLEY',
    description: 'Green fields, barns, roads, warehouses and fortified industrial lines.',
    players: 10,
    biome: 'industrial',
    colors: { ground: '#6e7d45', wall: '#3c4631', detail: '#8a9d62' }
  },
  'NEON CITY': {
    name: 'NEON CITY',
    description: 'Night streets, glowing signs, alleys, rooftops and perfect angles for flanks.',
    players: 10,
    biome: 'city',
    colors: { ground: '#1d2637', wall: '#101827', detail: '#4be7ff' }
  },
  'FROST BASE': {
    name: 'FROST BASE',
    description: 'Snowy military base with ice walls, trenches and bleak openings.',
    players: 10,
    biome: 'frost',
    colors: { ground: '#bfd8f0', wall: '#6e86a5', detail: '#ecf5ff' }
  },
  'DESERT RUINS': {
    name: 'DESERT RUINS',
    description: 'An old sand-blasted canyon, stone ruins and broken fortifications.',
    players: 10,
    biome: 'desert',
    colors: { ground: '#9f7a4c', wall: '#6f5434', detail: '#d4ae62' }
  }
};

const skinSets = {
  RAVEN: [
    { name: 'Base', colors: { helmet: '#6fe2ff', armor: '#2d5ad5', sleeves: '#1f3058', pants: '#141d31', gloves: '#c7f8ff', weapon: '#8ae8ff', glow: '#9be8ff', energy: '#cbffff' } },
    { name: 'Neon', colors: { helmet: '#21f6ff', armor: '#4f7cff', sleeves: '#1a2b5d', pants: '#0e152d', gloves: '#dafcff', weapon: '#77f9ff', glow: '#7efaff', energy: '#d4ffff' } },
    { name: 'Shadow', colors: { helmet: '#7a88b8', armor: '#2d384e', sleeves: '#121922', pants: '#0b1018', gloves: '#a1afd8', weapon: '#7c8ab7', glow: '#c8d7ff', energy: '#dfe8ff' } },
    { name: 'Inferno', colors: { helmet: '#ff8720', armor: '#9f3b2d', sleeves: '#4f1d1c', pants: '#1b1416', gloves: '#ffb374', weapon: '#ff9c4d', glow: '#ffca7a', energy: '#ffe0a8' } }
  ],
  VOLT: [
    { name: 'Base', colors: { helmet: '#ffde77', armor: '#d7b642', sleeves: '#5b4417', pants: '#282a2b', gloves: '#ffeaa0', weapon: '#f4f8a8', glow: '#fff7a8', energy: '#fff9bb' } },
    { name: 'Neon', colors: { helmet: '#fff36d', armor: '#c9ff39', sleeves: '#4a5520', pants: '#222b13', gloves: '#faffb9', weapon: '#f2ff88', glow: '#f7ff9d', energy: '#f3ffb9' } },
    { name: 'Shadow', colors: { helmet: '#e0e8ff', armor: '#6b7ba9', sleeves: '#1d2238', pants: '#111827', gloves: '#c5d2ff', weapon: '#dbe5ff', glow: '#dce8ff', energy: '#eff6ff' } },
    { name: 'Inferno', colors: { helmet: '#ffad5f', armor: '#a65a2d', sleeves: '#492711', pants: '#1e1410', gloves: '#ffd7ad', weapon: '#ffbc72', glow: '#ffcf8a', energy: '#ffe5ba' } }
  ],
  IRON: [
    { name: 'Base', colors: { helmet: '#dfeaf4', armor: '#82a6c8', sleeves: '#3d4d60', pants: '#1c2537', gloves: '#edf5ff', weapon: '#cfe8ff', glow: '#b7d6ff', energy: '#edf8ff' } },
    { name: 'Neon', colors: { helmet: '#7cd8ff', armor: '#5ca8ff', sleeves: '#20355a', pants: '#0f1727', gloves: '#d0f0ff', weapon: '#96dfff', glow: '#a2ddff', energy: '#dffbff' } },
    { name: 'Shadow', colors: { helmet: '#bec4d2', armor: '#55687f', sleeves: '#202a37', pants: '#0d121b', gloves: '#d9e0f2', weapon: '#b2bfd9', glow: '#d2dff8', energy: '#edf3ff' } },
    { name: 'Inferno', colors: { helmet: '#ffb48a', armor: '#b86243', sleeves: '#4b2b1f', pants: '#1a1110', gloves: '#ffd8b8', weapon: '#ffc994', glow: '#ffdca5', energy: '#ffeacf' } }
  ],
  FROST: [
    { name: 'Base', colors: { helmet: '#d7f4ff', armor: '#7bc8ff', sleeves: '#2d496b', pants: '#1d2d3b', gloves: '#effcff', weapon: '#dff5ff', glow: '#bfeeff', energy: '#ebfbff' } },
    { name: 'Neon', colors: { helmet: '#f0f6ff', armor: '#89f0ff', sleeves: '#1a465c', pants: '#102136', gloves: '#f4fbff', weapon: '#a9f1ff', glow: '#baf6ff', energy: '#e0fdff' } },
    { name: 'Shadow', colors: { helmet: '#bcd3f0', armor: '#5d7ca8', sleeves: '#1c2a42', pants: '#101821', gloves: '#dbe8ff', weapon: '#c5d9ff', glow: '#dfeeff', energy: '#edf7ff' } },
    { name: 'Inferno', colors: { helmet: '#ffd5a6', armor: '#d96d46', sleeves: '#57241a', pants: '#1c1412', gloves: '#ffe3c2', weapon: '#ffc79d', glow: '#ffd2a0', energy: '#ffe8d0' } }
  ]
};

const state = {
  screen: 'menu',
  selectedHero: 'RAVEN',
  selectedSkin: 'Base',
  selectedMap: 'IRON VALLEY',
  save: loadSave(),
  menuPulse: 0,
  battle: null,
  result: null,
  pointer: { x: 0, y: 0 },
  input: {
    joystick: { active: false, x: 0, y: 0 },
    aim: { x: 0, y: 0 },
    moveDown: false,
    fire: false,
    run: false,
    dash: false,
    ultimate: false,
    reload: false
  }
};

const app = document.querySelector('#app');
app.innerHTML = `
  <div id="game-root">
    <canvas id="game-canvas"></canvas>
    <div id="menu-screen" class="screen active">
      <div class="topbar">
        <div class="profile">
          <div class="avatar">RB</div>
          <div class="profile-text">
            <span class="profile-name">Player One</span>
            <span class="profile-level">Level 21</span>
          </div>
        </div>
        <div class="wallet">
          <div class="coin"><span></span> 1250</div>
          <div class="coin"><span style="background:linear-gradient(180deg,#8ce6ff,#4da8ff)"></span> 480</div>
          <div class="coin"><span style="background:linear-gradient(180deg,#ffd3a0,#ff8d52)"></span> 18</div>
        </div>
      </div>
      <div class="menu-title">ROYALBRAWL</div>
      <div id="menuHeroPreview" class="center-hero"></div>
      <div class="menu-actions">
        <button class="menubtn primary" data-action="battle">В БІЙ!</button>
        <button class="menubtn" data-action="heroes">БІЙЦІ</button>
        <button class="menubtn" data-action="skins">СКІНИ</button>
        <button class="menubtn" data-action="maps">КАРТИ</button>
        <button class="menubtn" data-action="shop">МАГАЗИН</button>
        <button class="menubtn" data-action="profile">ПРОФІЛЬ</button>
      </div>
    </div>

    <div id="hero-screen" class="screen">
      <div class="selection-panel">
        <div class="panel-header">
          <h2>БІЙЦІ</h2>
          <button class="secondary-btn" data-action="back-menu">Назад</button>
        </div>
        <div id="hero-grid" class="hero-grid"></div>
      </div>
    </div>

    <div id="skin-screen" class="screen">
      <div class="selection-panel">
        <div class="panel-header">
          <h2>СКІНИ</h2>
          <button class="secondary-btn" data-action="back-menu">Назад</button>
        </div>
        <div id="skin-grid" class="skin-grid"></div>
      </div>
    </div>

    <div id="map-screen" class="screen">
      <div class="selection-panel">
        <div class="panel-header">
          <h2>ВИБІР КАРТИ</h2>
          <button class="secondary-btn" data-action="back-menu">Назад</button>
        </div>
        <div id="map-grid" class="map-grid"></div>
      </div>
    </div>

    <div id="battle-screen" class="screen">
      <div class="hud">
        <div class="hud-top">
          <div class="stat-strip">
            <span class="icon">❤️</span>
            <div style="flex:1">
              <div style="font-size:0.7rem; letter-spacing:0.08em; text-transform:uppercase; color:#dfeeff">HP</div>
              <div class="healthbar"><div id="player-healthbar" class="healthbar-fill"></div></div>
            </div>
            <div id="player-health-text" style="font-weight:800; min-width:80px; text-align:right;">4000/4000</div>
          </div>
          <div class="stat-strip">
            <span class="icon">🛡</span>
            <div style="flex:1">
              <div style="font-size:0.7rem; letter-spacing:0.08em; text-transform:uppercase; color:#dfeeff">Броня</div>
              <div class="armorbar"><div id="player-armorbar" class="armorbar-fill"></div></div>
            </div>
            <div id="player-armor-text" style="font-weight:800; min-width:60px; text-align:right;">100</div>
          </div>
          <div class="stat-strip">
            <span class="icon">👥</span>
            <span id="alive-count" style="font-weight:800; min-width:70px; text-align:center;">10</span>
          </div>
        </div>

        <div class="status-panel">
          <div class="header"><span>Боти</span><span id="enemy-count">9</span></div>
          <div id="enemy-list"></div>
        </div>

        <div class="hud-center">
          <div id="countdown" class="countdown hidden">3</div>
          <div id="zone-warning" class="zone-warning hidden">Зона зменшується</div>
        </div>

        <div class="hud-left">
          <div id="move-joystick" class="joystick">
            <div class="joystick-thumb"></div>
          </div>
        </div>

        <div class="hud-right">
          <div id="aim-pad" class="hidden"><div class="aim-dot"></div></div>
          <button class="action-btn primary" data-key="fire">🔫</button>
          <button class="action-btn" data-key="aim">🎯</button>
          <button class="action-btn warning" data-key="run">🏃</button>
          <button class="action-btn" data-key="jump">⬆</button>
          <button class="action-btn" data-key="crouch">⬇</button>
          <button class="action-btn small" data-key="reload">🔄</button>
          <button class="action-btn small" data-key="dash">⚡</button>
          <button class="action-btn small danger" data-key="ultimate">💥</button>
        </div>

        <div class="hud-bottom">
          <button class="action-btn small" data-key="reload">🔄</button>
          <button class="action-btn small" data-key="dash">⚡</button>
          <button class="action-btn small danger" data-key="ultimate">💥</button>
        </div>
      </div>
    </div>

    <div id="result-screen" class="screen">
      <div class="result-panel active">
        <div class="result-box">
          <h2 id="result-title">Перемога</h2>
          <div class="result-stats">
            <div class="result-stat"><span class="label">Вбивства</span><span id="kills-stat" class="value">0</span></div>
            <div class="result-stat"><span class="label">Шкода</span><span id="damage-stat" class="value">0</span></div>
            <div class="result-stat"><span class="label">Час</span><span id="time-stat" class="value">00:00</span></div>
            <div class="result-stat"><span class="label">Нагорода</span><span id="reward-stat" class="value">200</span></div>
          </div>
          <div class="result-actions">
            <button class="primary-btn" data-action="play-again">Зіграти ще</button>
            <button class="secondary-btn" data-action="back-menu">В меню</button>
          </div>
        </div>
      </div>
    </div>
  </div>
`;

const ui = {
  menuScreen: document.getElementById('menu-screen'),
  heroScreen: document.getElementById('hero-screen'),
  skinScreen: document.getElementById('skin-screen'),
  mapScreen: document.getElementById('map-screen'),
  battleScreen: document.getElementById('battle-screen'),
  resultScreen: document.getElementById('result-screen'),
  heroGrid: document.getElementById('hero-grid'),
  skinGrid: document.getElementById('skin-grid'),
  mapGrid: document.getElementById('map-grid'),
  menuHeroPreview: document.getElementById('menuHeroPreview'),
  countdown: document.getElementById('countdown'),
  zoneWarning: document.getElementById('zone-warning'),
  aliveCount: document.getElementById('alive-count'),
  enemyList: document.getElementById('enemy-list'),
  enemyCount: document.getElementById('enemy-count'),
  playerHealthbar: document.getElementById('player-healthbar'),
  playerArmorbar: document.getElementById('player-armorbar'),
  playerHealthText: document.getElementById('player-health-text'),
  playerArmorText: document.getElementById('player-armor-text'),
  resultTitle: document.getElementById('result-title'),
  killsStat: document.getElementById('kills-stat'),
  damageStat: document.getElementById('damage-stat'),
  timeStat: document.getElementById('time-stat'),
  rewardStat: document.getElementById('reward-stat')
};

const renderer = new THREE.WebGLRenderer({ canvas: document.getElementById('game-canvas'), antialias: true, alpha: true });
renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
renderer.setSize(window.innerWidth, window.innerHeight);
renderer.shadowMap.enabled = true;
renderer.shadowMap.type = THREE.PCFSoftShadowMap;

const scene = new THREE.Scene();
scene.background = new THREE.Color('#07141f');
scene.fog = new THREE.Fog('#07141f', 18, 90);

const camera = new THREE.PerspectiveCamera(58, window.innerWidth / window.innerHeight, 0.1, 300);
camera.position.set(0, 6, 12);

const ambient = new THREE.HemisphereLight('#98baff', '#070b13', 1.15);
scene.add(ambient);

const dirLight = new THREE.DirectionalLight('#f2f6ff', 1.24);
dirLight.position.set(8, 18, 10);
dirLight.castShadow = true;
dirLight.shadow.mapSize.set(1024, 1024);
scene.add(dirLight);

const menuGroup = new THREE.Group();
scene.add(menuGroup);

function createFloor(color = '#2f3e2a') {
  const floor = new THREE.Mesh(
    new THREE.CylinderGeometry(18, 18, 1, 40),
    new THREE.MeshStandardMaterial({ color, roughness: 0.92, metalness: 0.1 })
  );
  floor.position.y = -0.5;
  floor.receiveShadow = true;
  return floor;
}

const menuFloor = createFloor('#1c2f2d');
menuGroup.add(menuFloor);

function makeArenaDecor() {
  const decor = new THREE.Group();
  for (let i = 0; i < 30; i += 1) {
    const column = new THREE.Mesh(
      new THREE.CylinderGeometry(0.3 + Math.random() * 0.4, 0.4 + Math.random() * 0.6, 3 + Math.random() * 5, 12),
      new THREE.MeshStandardMaterial({ color: i % 2 === 0 ? '#314667' : '#1a2337', metalness: 0.7, roughness: 0.55 })
    );
    column.position.set((Math.random() - 0.5) * 26, 1.5 + Math.random() * 2, (Math.random() - 0.5) * 26);
    column.castShadow = true;
    decor.add(column);
  }

  for (let i = 0; i < 28; i += 1) {
    const light = new THREE.Mesh(
      new THREE.BoxGeometry(0.6, 0.2, 0.6),
      new THREE.MeshStandardMaterial({ emissive: i % 2 === 0 ? '#5cb8ff' : '#ff9af7', emissiveIntensity: 2.6, color: '#1d2430' })
    );
    light.position.set((Math.random() - 0.5) * 24, 4 + Math.random() * 4, (Math.random() - 0.5) * 24);
    decor.add(light);
  }
  return decor;
}

menuGroup.add(makeArenaDecor());

function createParticleField() {
  const count = 210;
  const geometry = new THREE.BufferGeometry();
  const positions = new Float32Array(count * 3);
  for (let i = 0; i < count; i += 1) {
    positions[i * 3] = (Math.random() - 0.5) * 35;
    positions[i * 3 + 1] = Math.random() * 10 + 1.5;
    positions[i * 3 + 2] = (Math.random() - 0.5) * 35;
  }
  geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
  const material = new THREE.PointsMaterial({ color: '#8cc9ff', size: 0.09, transparent: true, opacity: 0.9 });
  const points = new THREE.Points(geometry, material);
  menuGroup.add(points);
  return points;
}

const menuParticles = createParticleField();

function createHeroModel(colorSet = heroes.RAVEN.skinColors) {
  const group = new THREE.Group();

  const bodyMaterial = new THREE.MeshStandardMaterial({ color: colorSet.armor, metalness: 0.5, roughness: 0.34 });
  const accentMaterial = new THREE.MeshStandardMaterial({ color: colorSet.glow, emissive: colorSet.glow, emissiveIntensity: 1.3, metalness: 0.4, roughness: 0.3 });
  const darkMetal = new THREE.MeshStandardMaterial({ color: colorSet.helmet, metalness: 0.68, roughness: 0.36 });
  const weaponMaterial = new THREE.MeshStandardMaterial({ color: colorSet.weapon, emissive: colorSet.energy, emissiveIntensity: 1.2, metalness: 0.7, roughness: 0.28 });

  const torso = new THREE.Mesh(new THREE.BoxGeometry(1.1, 1.4, 0.56), bodyMaterial);
  torso.position.y = 2.3;
  torso.castShadow = true;
  group.add(torso);

  const head = new THREE.Mesh(new THREE.SphereGeometry(0.5, 24, 24), new THREE.MeshStandardMaterial({ color: '#dcbfa8', roughness: 0.88 }));
  head.position.y = 3.6;
  head.castShadow = true;
  group.add(head);

  const helmet = new THREE.Mesh(new THREE.SphereGeometry(0.54, 24, 22, 0, Math.PI * 2, 0, Math.PI * 1.05), darkMetal);
  helmet.position.y = 3.75;
  helmet.scale.set(1.08, 1.05, 1.08);
  helmet.castShadow = true;
  group.add(helmet);

  const leftArm = new THREE.Mesh(new THREE.BoxGeometry(0.34, 1.2, 0.34), bodyMaterial);
  leftArm.position.set(-0.8, 2.3, 0.06);
  leftArm.castShadow = true;
  group.add(leftArm);

  const rightArm = new THREE.Mesh(new THREE.BoxGeometry(0.34, 1.2, 0.34), bodyMaterial);
  rightArm.position.set(0.8, 2.3, 0.06);
  rightArm.castShadow = true;
  group.add(rightArm);

  const leftForearm = new THREE.Mesh(new THREE.BoxGeometry(0.22, 1, 0.22), bodyMaterial);
  leftForearm.position.set(-0.94, 1.2, 0.08);
  leftForearm.castShadow = true;
  group.add(leftForearm);

  const rightForearm = new THREE.Mesh(new THREE.BoxGeometry(0.22, 1, 0.22), bodyMaterial);
  rightForearm.position.set(0.94, 1.2, 0.08);
  rightForearm.castShadow = true;
  group.add(rightForearm);

  const leftLeg = new THREE.Mesh(new THREE.BoxGeometry(0.41, 1.4, 0.41), new THREE.MeshStandardMaterial({ color: colorSet.pants, metalness: 0.34, roughness: 0.72 }));
  leftLeg.position.set(-0.26, 0.75, 0);
  leftLeg.castShadow = true;
  group.add(leftLeg);

  const rightLeg = leftLeg.clone();
  rightLeg.position.x = 0.26;
  group.add(rightLeg);

  const leftBoot = new THREE.Mesh(new THREE.BoxGeometry(0.48, 0.28, 0.82), new THREE.MeshStandardMaterial({ color: colorSet.gloves, metalness: 0.3, roughness: 0.5 }));
  leftBoot.position.set(-0.26, -0.1, 0.18);
  leftBoot.castShadow = true;
  group.add(leftBoot);

  const rightBoot = leftBoot.clone();
  rightBoot.position.x = 0.26;
  group.add(rightBoot);

  const weapon = new THREE.Mesh(new THREE.BoxGeometry(0.18, 1.45, 0.52), weaponMaterial);
  weapon.position.set(1.22, 1.7, 0.35);
  weapon.rotation.z = 0.18;
  weapon.castShadow = true;
  group.add(weapon);

  const muzzle = new THREE.Mesh(new THREE.SphereGeometry(0.08, 16, 16), accentMaterial);
  muzzle.position.set(1.25, 2.3, 0.72);
  group.add(muzzle);

  const backpack = new THREE.Mesh(new THREE.BoxGeometry(0.74, 1.1, 0.26), new THREE.MeshStandardMaterial({ color: colorSet.armor, metalness: 0.56, roughness: 0.46 }));
  backpack.position.set(0, 2.5, -0.52);
  backpack.castShadow = true;
  group.add(backpack);

  group.userData = { torso, head, helmet, leftArm, rightArm, leftLeg, rightLeg, leftForearm, rightForearm, weapon, muzzle, bodyMaterial, darkMetal, weaponMaterial };
  return group;
}

const menuHero = createHeroModel(heroes.RAVEN.skinColors);
menuHero.scale.setScalar(1.12);
menuHero.position.set(0, 0.15, 0);
menuHero.rotation.y = Math.PI * 0.5;
menuGroup.add(menuHero);

function applySkinToHero(hero, skinColors) {
  if (!hero || !hero.userData) return;
  const { torso, helmet, leftArm, rightArm, leftLeg, rightLeg, leftForearm, rightForearm, weapon, muzzle, backpack } = hero.userData;
  const bodyMaterial = new THREE.MeshStandardMaterial({ color: skinColors.armor, metalness: 0.55, roughness: 0.34 });
  const darkMetal = new THREE.MeshStandardMaterial({ color: skinColors.helmet, metalness: 0.72, roughness: 0.35 });
  const weaponMaterial = new THREE.MeshStandardMaterial({ color: skinColors.weapon, emissive: skinColors.energy, emissiveIntensity: 1.2, metalness: 0.75, roughness: 0.25 });
  const glowMaterial = new THREE.MeshStandardMaterial({ color: skinColors.glow, emissive: skinColors.glow, emissiveIntensity: 1.6, metalness: 0.32, roughness: 0.28 });

  torso.material = bodyMaterial;
  leftArm.material = bodyMaterial;
  rightArm.material = bodyMaterial;
  leftForearm.material = bodyMaterial;
  rightForearm.material = bodyMaterial;
  leftLeg.material = new THREE.MeshStandardMaterial({ color: skinColors.pants, metalness: 0.3, roughness: 0.74 });
  rightLeg.material = leftLeg.material;
  helmet.material = darkMetal;
  backpack.material = bodyMaterial;
  weapon.material = weaponMaterial;
  muzzle.material = glowMaterial;
  const bootMat = new THREE.MeshStandardMaterial({ color: skinColors.gloves, metalness: 0.3, roughness: 0.55 });
  hero.children.forEach((child) => {
    if (child.geometry && child.geometry.type === 'BoxGeometry' && child.position.y < 0.2) {
      child.material = bootMat;
    }
  });
}

const heroDefinitions = Object.keys(heroes);
function renderHeroCards() {
  ui.heroGrid.innerHTML = heroDefinitions.map((key) => {
    const hero = heroes[key];
    const selected = key === state.selectedHero ? 'selected' : '';
    return `
      <div class="card ${selected}" data-hero="${key}">
        <div class="thumb" style="background:linear-gradient(135deg, ${hero.color}66, ${hero.accent}66);"></div>
        <div class="small-tag">${hero.className}</div>
        <h3>${hero.name}</h3>
        <p>${hero.weapon} • ${hero.ability}</p>
        <div class="stats">
          <span class="pill">HP ${hero.hp}</span>
          <span class="pill">DMG ${hero.damage}</span>
          <span class="pill">SPD ${hero.speed}</span>
        </div>
        <div class="card-actions">
          <button class="primary-btn" data-hero-select="${key}">ВИБРАТИ</button>
        </div>
      </div>
    `;
  }).join('');
}

function renderSkinCards() {
  const currentSkins = skinSets[state.selectedHero];
  ui.skinGrid.innerHTML = currentSkins.map((skin) => {
    const active = skin.name === state.selectedSkin ? 'selected' : '';
    return `
      <div class="card ${active}" data-skin-name="${skin.name}">
        <div class="thumb" style="background:linear-gradient(135deg, ${skin.colors.helmet}, ${skin.colors.armor});"></div>
        <h3>${skin.name}</h3>
        <p>Один з готових стильних забарвлень героя ${state.selectedHero}</p>
        <div class="card-actions">
          <button class="primary-btn" data-skin-select="${skin.name}">Застосувати</button>
        </div>
      </div>
    `;
  }).join('');
}

function renderMapCards() {
  const keys = Object.keys(maps);
  ui.mapGrid.innerHTML = keys.map((name) => {
    const map = maps[name];
    const active = name === state.selectedMap ? 'selected' : '';
    return `
      <div class="card ${active}" data-map="${name}">
        <div class="thumb" style="background:linear-gradient(135deg, ${map.colors.ground}, ${map.colors.detail});"></div>
        <h3>${name}</h3>
        <p>${map.description}</p>
        <div class="stats">
          <span class="pill">${map.players} гравців</span>
          <span class="pill">${map.biome}</span>
        </div>
        <div class="card-actions">
          <button class="primary-btn" data-map-select="${name}">ВИБРАТИ</button>
        </div>
      </div>
    `;
  }).join('');
}

function setScreen(screen) {
  state.screen = screen;
  ui.menuScreen.classList.toggle('active', screen === 'menu');
  ui.heroScreen.classList.toggle('active', screen === 'heroes');
  ui.skinScreen.classList.toggle('active', screen === 'skins');
  ui.mapScreen.classList.toggle('active', screen === 'maps');
  ui.battleScreen.classList.toggle('active', screen === 'battle');
  ui.resultScreen.classList.toggle('active', screen === 'result');
}

function selectHero(heroName) {
  state.selectedHero = heroName;
  state.selectedSkin = skinSets[heroName][0].name;
  renderHeroCards();
  renderSkinCards();
  const previewColors = skinSets[heroName].find((s) => s.name === state.selectedSkin)?.colors ?? heroes[heroName].skinColors;
  applySkinToHero(menuHero, previewColors);
}

function selectSkin(skinName) {
  state.selectedSkin = skinName;
  renderSkinCards();
  const colors = skinSets[state.selectedHero].find((skin) => skin.name === skinName)?.colors ?? heroes[state.selectedHero].skinColors;
  applySkinToHero(menuHero, colors);
}

function selectMap(name) {
  state.selectedMap = name;
  renderMapCards();
}

function setupButtons() {
  document.querySelectorAll('[data-action]').forEach((button) => {
    button.addEventListener('click', () => {
      const action = button.dataset.action;
      if (action === 'heroes') setScreen('heroes');
      if (action === 'skins') setScreen('skins');
      if (action === 'maps') setScreen('maps');
      if (action === 'battle') startBattle();
      if (action === 'back-menu') setScreen('menu');
      if (action === 'play-again') startBattle();
    });
  });

  document.querySelectorAll('[data-hero-select]').forEach((button) => {
    button.addEventListener('click', () => selectHero(button.dataset.heroSelect));
  });

  document.querySelectorAll('[data-skin-select]').forEach((button) => {
    button.addEventListener('click', () => selectSkin(button.dataset.skinSelect));
  });

  document.querySelectorAll('[data-map-select]').forEach((button) => {
    button.addEventListener('click', () => selectMap(button.dataset.mapSelect));
  });

  document.querySelectorAll('[data-key]').forEach((button) => {
    const key = button.dataset.key;
    const press = (isDown) => {
      if (key === 'fire') state.input.fire = isDown;
      if (key === 'aim') state.input.aim.x = isDown ? 1 : 0;
      if (key === 'run') state.input.run = isDown;
      if (key === 'jump') state.input.moveDown = isDown;
      if (key === 'crouch') state.input.moveDown = isDown;
      if (key === 'reload') state.input.reload = isDown;
      if (key === 'dash') state.input.dash = isDown;
      if (key === 'ultimate') state.input.ultimate = isDown;
      button.classList.toggle('active', isDown);
    };

    button.addEventListener('pointerdown', (event) => {
      event.preventDefault();
      press(true);
    });
    button.addEventListener('pointerup', () => press(false));
    button.addEventListener('pointerleave', () => press(false));
  });
}

function loadSave() {
  const saved = localStorage.getItem('royalbrawl-save');
  if (!saved) {
    return { coins: 1500, crystals: 450, xp: 0, wins: 0, kills: 0 };
  }
  try {
    return JSON.parse(saved);
  } catch {
    return { coins: 1500, crystals: 450, xp: 0, wins: 0, kills: 0 };
  }
}

function saveProgress() {
  localStorage.setItem('royalbrawl-save', JSON.stringify(state.save));
}

function createBattleScene() {
  const battleScene = new THREE.Group();
  scene.add(battleScene);

  const mapName = state.selectedMap;
  const map = maps[mapName];
  const colors = map.colors;
  const ground = createFloor(colors.ground);
  ground.scale.set(1.8, 1, 1.8);
  battleScene.add(ground);

  for (let i = 0; i < 24; i += 1) {
    const wall = new THREE.Mesh(
      new THREE.BoxGeometry(3.2 + Math.random() * 1.8, 2.2 + Math.random() * 2.2, 2.8 + Math.random() * 2.4),
      new THREE.MeshStandardMaterial({ color: colors.wall, roughness: 0.8, metalness: 0.15 })
    );
    const x = (Math.random() - 0.5) * 44;
    const z = (Math.random() - 0.5) * 44;
    if (Math.abs(x) < 6 && Math.abs(z) < 6) continue;
    wall.position.set(x, wall.geometry.parameters.height / 2, z);
    wall.castShadow = true;
    wall.receiveShadow = true;
    battleScene.add(wall);
  }

  for (let i = 0; i < 18; i += 1) {
    const crate = new THREE.Mesh(
      new THREE.BoxGeometry(1.4, 1.4, 1.4),
      new THREE.MeshStandardMaterial({ color: colors.detail, roughness: 0.9, metalness: 0.12 })
    );
    crate.position.set((Math.random() - 0.5) * 28, 0.7, (Math.random() - 0.5) * 28);
    crate.castShadow = true;
    crate.receiveShadow = true;
    battleScene.add(crate);
  }

  for (let i = 0; i < 22; i += 1) {
    const tree = new THREE.Group();
    const trunk = new THREE.Mesh(
      new THREE.CylinderGeometry(0.18, 0.28, 2, 8),
      new THREE.MeshStandardMaterial({ color: '#5c4d39', roughness: 0.9 })
    );
    trunk.position.y = 1;
    const crown = new THREE.Mesh(
      new THREE.SphereGeometry(1.2 + Math.random() * 0.5, 14, 14),
      new THREE.MeshStandardMaterial({ color: '#438b5a', roughness: 0.9 })
    );
    crown.position.y = 2.8;
    tree.add(trunk, crown);
    tree.position.set((Math.random() - 0.5) * 40, 0, (Math.random() - 0.5) * 40);
    tree.traverse((node) => { if (node.isMesh) { node.castShadow = true; node.receiveShadow = true; } });
    battleScene.add(tree);
  }

  return battleScene;
}

function spawnPlayer() {
  const heroData = heroes[state.selectedHero];
  const model = createHeroModel(skinSets[state.selectedHero].find((skin) => skin.name === state.selectedSkin)?.colors ?? heroData.skinColors);
  const player = {
    type: 'player',
    group: model,
    health: heroData.hp,
    armor: 100,
    speed: heroData.speed,
    baseSpeed: heroData.speed,
    damage: heroData.damage,
    range: heroData.range,
    reloadTime: heroData.reload,
    fireCooldown: 0,
    dashCooldown: 0,
    ultimateCharge: 0,
    ultimateReady: false,
    position: new THREE.Vector3(0, 0, 8),
    velocity: new THREE.Vector3(),
    yaw: 0,
    aimYaw: 0,
    radius: 1.2,
    kills: 0,
    damageDone: 0,
    alive: true,
    visible: true,
    dashActive: 0,
    abilityBoost: 0,
    id: 'player'
  };

  model.position.copy(player.position);
  model.rotation.y = Math.PI;
  model.castShadow = true;
  scene.add(model);
  return player;
}

function spawnBot(index) {
  const heroNames = Object.keys(heroes);
  const heroName = heroNames[index % heroNames.length];
  const heroData = heroes[heroName];
  const model = createHeroModel(skinSets[heroName][1].colors);
  const bot = {
    type: 'bot',
    group: model,
    name: `BOT-${index + 1}`,
    health: heroData.hp * (0.88 + Math.random() * 0.25),
    armor: 52,
    speed: heroData.speed * (0.85 + Math.random() * 0.22),
    baseSpeed: heroData.speed * (0.85 + Math.random() * 0.22),
    damage: heroData.damage * (0.7 + Math.random() * 0.28),
    range: heroData.range,
    reloadTime: heroData.reload * (0.92 + Math.random() * 0.5),
    fireCooldown: 0.7 + Math.random() * 0.7,
    dashCooldown: 2 + Math.random() * 2,
    ultimateCharge: 0,
    alive: true,
    radius: 1.1,
    position: new THREE.Vector3((Math.random() - 0.5) * 18, 0, (Math.random() - 0.5) * 18),
    velocity: new THREE.Vector3(),
    yaw: Math.random() * Math.PI * 2,
    cooldown: Math.random() * 1.5,
    retreating: false,
    target: null,
    attackBias: Math.random() * 10,
    id: `bot-${index}`
  };

  model.position.copy(bot.position);
  model.rotation.y = Math.PI;
  scene.add(model);
  return bot;
}

function spawnLoot() {
  const lootTypes = ['ammo', 'armor', 'medkit', 'energy', 'weapon'];
  const items = [];
  for (let i = 0; i < 18; i += 1) {
    const type = lootTypes[i % lootTypes.length];
    const mesh = new THREE.Mesh(
      new THREE.BoxGeometry(0.8, 0.8, 0.8),
      new THREE.MeshStandardMaterial({
        color: type === 'ammo' ? '#ffcc67' : type === 'armor' ? '#7cc7ff' : type === 'medkit' ? '#ff8f80' : type === 'energy' ? '#8bffec' : '#d5f0ff',
        emissive: type === 'ammo' ? '#d99a00' : type === 'armor' ? '#2a71ff' : type === 'medkit' ? '#ff683a' : type === 'energy' ? '#21e4dc' : '#8de0ff',
        emissiveIntensity: 0.9,
        metalness: 0.35,
        roughness: 0.35
      })
    );
    mesh.position.set((Math.random() - 0.5) * 30, 0.8, (Math.random() - 0.5) * 30);
    mesh.castShadow = true;
    mesh.receiveShadow = true;
    scene.add(mesh);
    items.push({ type, mesh, picked: false, label: type });
  }
  return items;
}

function updateEnemyList() {
  const enemies = state.battle?.bots.filter((bot) => bot.alive) ?? [];
  ui.enemyList.innerHTML = enemies.slice(0, 4).map((bot) => `
    <div class="enemy-card">
      <span class="enemy-badge"></span>
      <span class="enemy-name">${bot.name}</span>
      <span class="enemy-hp">${Math.ceil(bot.health)}</span>
    </div>
  `).join('');
  ui.enemyCount.textContent = String(enemies.length);
}

function formatCountdown(value) {
  ui.countdown.textContent = String(value);
  ui.countdown.classList.remove('hidden');
  setTimeout(() => ui.countdown.classList.add('hidden'), 550);
}

function showResult(win) {
  state.battle.resultVisible = true;
  const stats = state.battle.stats;
  ui.resultTitle.textContent = win ? 'ПЕРЕМОГА!' : 'ПОРАЗКА';
  ui.killsStat.textContent = String(stats.kills);
  ui.damageStat.textContent = String(Math.round(stats.damageDone));
  ui.timeStat.textContent = formatTimer(stats.timeElapsed);
  ui.rewardStat.textContent = win ? '250' : '50';
  setScreen('result');
}

function formatTimer(seconds) {
  const m = String(Math.floor(seconds / 60)).padStart(2, '0');
  const s = String(Math.floor(seconds % 60)).padStart(2, '0');
  return `${m}:${s}`;
}

function startBattle() {
  scene.clear();
  scene.background = new THREE.Color('#0a1421');
  scene.fog = new THREE.Fog('#0a1421', 18, 120);
  scene.add(ambient);
  scene.add(dirLight);
  const mapGroup = createBattleScene();
  scene.add(mapGroup);

  const player = spawnPlayer();
  const bots = [];
  for (let i = 0; i < 9; i += 1) {
    bots.push(spawnBot(i));
  }
  const loot = spawnLoot();
  const safeZone = {
    center: new THREE.Vector3(0, 0, 0),
    radius: 30,
    targetRadius: 10,
    shrinkTimer: 0,
    phase: 0
  };

  state.battle = {
    mapGroup,
    player,
    bots,
    loot,
    safeZone,
    matchTime: 0,
    countdown: 3,
    started: false,
    resultVisible: false,
    stats: { kills: 0, damageDone: 0, timeElapsed: 0 },
    activeTimer: 0,
    alivePlayers: bots.length + 1
  };

  ui.playerHealthText.textContent = `${player.health}/${player.health}`;
  ui.playerArmorText.textContent = String(player.armor);
  setScreen('battle');

  setTimeout(() => {
    state.battle.started = true;
    state.battle.countdown = 0;
    ui.countdown.classList.add('hidden');
    ui.zoneWarning.classList.remove('hidden');
  }, 3000);

  setTimeout(() => formatCountdown(3), 250);
  setTimeout(() => formatCountdown(2), 1250);
  setTimeout(() => formatCountdown(1), 2250);
}

function updateHUD() {
  if (!state.battle) return;
  const player = state.battle.player;
  const healthPercent = (player.health / heroes[state.selectedHero].hp) * 100;
  const armorPercent = Math.max(0, (player.armor / 100) * 100);
  ui.playerHealthbar.style.width = `${Math.max(0, healthPercent)}%`;
  ui.playerArmorbar.style.width = `${Math.max(0, armorPercent)}%`;
  ui.playerHealthText.textContent = `${Math.max(0, Math.ceil(player.health))}/${heroes[state.selectedHero].hp}`;
  ui.playerArmorText.textContent = String(Math.ceil(player.armor));
  ui.aliveCount.textContent = String(state.battle.bots.filter((bot) => bot.alive).length + (player.alive ? 1 : 0));
  updateEnemyList();
}

function applyDamage(target, incomingDamage, sourceType = 'player') {
  if (!target.alive) return;
  if (target.type === 'player') {
    const remainingDamage = incomingDamage - Math.min(target.armor, incomingDamage * 0.32);
    target.armor = Math.max(0, target.armor - incomingDamage * 0.32);
    target.health -= Math.max(0, remainingDamage);
    if (sourceType === 'bot') {
      target.group.rotation.z = 0.22;
    }
    if (target.health <= 0) {
      target.alive = false;
      target.group.visible = false;
      state.battle.resultVisible = true;
      showResult(false);
    }
    return;
  }

  const remainingDamage = incomingDamage - Math.min(target.armor, incomingDamage * 0.28);
  target.armor = Math.max(0, target.armor - incomingDamage * 0.28);
  target.health -= Math.max(0, remainingDamage);
  if (target.health <= 0) {
    target.alive = false;
    target.group.visible = false;
    if (sourceType === 'player') {
      state.battle.stats.kills += 1;
      state.battle.player.kills += 1;
      state.battle.player.damageDone += incomingDamage;
      state.battle.stats.damageDone += incomingDamage;
      state.save.kills += 1;
      state.save.coins += 45;
      saveProgress();
    }
  }
}

function checkLootPickup() {
  if (!state.battle) return;
  const player = state.battle.player;
  for (const item of state.battle.loot) {
    if (item.picked) continue;
    const dist = item.mesh.position.distanceTo(player.group.position);
    if (dist < 2.2) {
      item.picked = true;
      item.mesh.visible = false;
      if (item.type === 'ammo') {
        player.damage += 15;
      }
      if (item.type === 'armor') {
        player.armor = Math.min(100, player.armor + 25);
      }
      if (item.type === 'medkit') {
        player.health = Math.min(heroes[state.selectedHero].hp, player.health + 450);
      }
      if (item.type === 'energy') {
        player.ultimateCharge = Math.min(100, player.ultimateCharge + 25);
      }
      if (item.type === 'weapon') {
        player.damage += 80;
      }
    }
  }
}

function spawnProjectile(origin, direction, owner, speed = 34, damage = 80, color = '#7ae0ff') {
  if (!state.battle) return;
  const projectile = new THREE.Mesh(
    new THREE.SphereGeometry(0.12, 12, 12),
    new THREE.MeshStandardMaterial({ color, emissive: color, emissiveIntensity: 1.2, metalness: 0.4, roughness: 0.25 })
  );
  const startPos = origin.clone();
  projectile.position.copy(startPos);
  projectile.castShadow = true;
  scene.add(projectile);
  state.battle.projectiles = state.battle.projectiles || [];
  state.battle.projectiles.push({
    mesh: projectile,
    velocity: direction.clone().multiplyScalar(speed),
    owner,
    damage,
    ttl: 2.2,
    color
  });
}

function firePlayerWeapon() {
  if (!state.battle || !state.battle.player.alive) return;
  const player = state.battle.player;
  if (player.fireCooldown > 0) return;
  const aimDir = new THREE.Vector3(Math.sin(player.yaw), 0, Math.cos(player.yaw)).normalize();
  const muzzle = new THREE.Vector3(player.group.position.x + aimDir.x * 1.4, 2.6, player.group.position.z + aimDir.z * 1.4);
  const color = heroes[state.selectedHero].color;
  spawnProjectile(muzzle, aimDir, 'player', 34, player.damage, color);
  player.fireCooldown = Math.max(0.12, 0.18);
  player.group.userData.weapon.rotation.z = 0.45;
  player.group.userData.weapon.rotation.x = 0.18;
  state.battle.stats.damageDone += player.damage * 0.15;
}

function fireBotWeapon(bot) {
  if (!bot.alive) return;
  const dir = new THREE.Vector3().subVectors(state.battle.player.group.position, bot.group.position).normalize();
  const muzzle = bot.group.position.clone().add(dir.clone().multiplyScalar(1.4)).setY(2.2);
  spawnProjectile(muzzle, dir, 'bot', 25, bot.damage, '#ffb36d');
  bot.fireCooldown = bot.reloadTime * (0.8 + Math.random() * 0.6);
}

function updateProjectiles(delta) {
  if (!state.battle || !state.battle.projectiles) return;
  const list = state.battle.projectiles;
  for (let i = list.length - 1; i >= 0; i -= 1) {
    const p = list[i];
    p.mesh.position.addScaledVector(p.velocity, delta);
    p.ttl -= delta;

    if (p.owner === 'player') {
      for (const bot of state.battle.bots) {
        if (!bot.alive) continue;
        if (p.mesh.position.distanceTo(bot.group.position) < 1.3) {
          applyDamage(bot, p.damage, 'player');
          if (!bot.alive) {
            state.battle.stats.kills += 1;
            state.battle.player.kills += 1;
            state.battle.player.damageDone += p.damage;
          }
          scene.remove(p.mesh);
          list.splice(i, 1);
          return;
        }
      }
    } else {
      const player = state.battle.player;
      if (p.mesh.position.distanceTo(player.group.position) < 1.4) {
        applyDamage(player, p.damage, 'bot');
        scene.remove(p.mesh);
        list.splice(i, 1);
        return;
      }
    }

    if (p.ttl <= 0 || Math.abs(p.mesh.position.x) > 60 || Math.abs(p.mesh.position.z) > 60) {
      scene.remove(p.mesh);
      list.splice(i, 1);
    }
  }
}

function handleInput(delta) {
  if (!state.battle || !state.battle.started) return;
  const player = state.battle.player;
  const move = new THREE.Vector2(state.input.joystick.x, state.input.joystick.y);
  const speedMultiplier = state.input.run ? 1.6 : 1;
  let movement = new THREE.Vector3(move.x, 0, move.y);
  if (movement.lengthSq() > 0.001) {
    movement.normalize();
    const forward = new THREE.Vector3(Math.sin(player.yaw), 0, Math.cos(player.yaw));
    const right = new THREE.Vector3(forward.z, 0, -forward.x);
    const adjusted = new THREE.Vector3();
    adjusted.addScaledVector(forward, movement.y);
    adjusted.addScaledVector(right, movement.x);
    adjusted.normalize();
    player.position.addScaledVector(adjusted, (player.speed * speedMultiplier) * delta);
    player.group.position.copy(player.position);
    player.group.rotation.y = -player.yaw + Math.PI;
  }

  if (state.input.fire) firePlayerWeapon();

  player.fireCooldown = Math.max(0, player.fireCooldown - delta);
  player.group.userData.weapon.rotation.z = THREE.MathUtils.lerp(player.group.userData.weapon.rotation.z, 0.18, 0.2);
  player.group.userData.weapon.rotation.x = THREE.MathUtils.lerp(player.group.userData.weapon.rotation.x, 0.04, 0.2);

  if (state.input.dash) {
    const dashVec = new THREE.Vector3(Math.sin(player.yaw), 0, Math.cos(player.yaw)).normalize();
    player.position.addScaledVector(dashVec, 6.5);
    player.group.position.copy(player.position);
    state.input.dash = false;
  }

  if (state.input.ultimate) {
    if (!player.ultimateReady && player.ultimateCharge >= 100) {
      player.ultimateReady = true;
      player.speed *= 1.5;
      player.fireCooldown = 0;
      player.damage *= 1.4;
      player.ultimateReady = true;
      state.input.ultimate = false;
      player.ultimateCharge = 0;
    }
  }

  player.ultimateCharge = Math.min(100, player.ultimateCharge + delta * 7);
  if (state.input.reload) {
    if (player.fireCooldown <= 0.12) {
      player.fireCooldown = 0.25;
      state.input.reload = false;
    }
  }

  const lookVector = new THREE.Vector3(state.input.aim.x, 0, state.input.aim.y || 0.1).normalize();
  if (lookVector.lengthSq() > 0.01) {
    player.yaw = Math.atan2(lookVector.x, lookVector.z);
  }
  player.group.rotation.y = -player.yaw + Math.PI;
  player.group.position.y = 0;
}

function updateBots(delta) {
  if (!state.battle) return;
  const player = state.battle.player;
  const aliveBots = state.battle.bots.filter((bot) => bot.alive);

  for (const bot of state.battle.bots) {
    if (!bot.alive) continue;
    const distance = bot.group.position.distanceTo(player.group.position);
    const dirToPlayer = new THREE.Vector3().subVectors(player.group.position, bot.group.position).normalize();

    bot.fireCooldown = Math.max(0, bot.fireCooldown - delta);
    bot.cooldown -= delta;

    if (distance < 10) {
      bot.retreating = bot.health < 150;
      if (distance < 7 && bot.fireCooldown <= 0) {
        fireBotWeapon(bot);
      }
      if (distance > 5) {
        bot.group.position.addScaledVector(dirToPlayer, bot.speed * delta);
      } else if (bot.retreating) {
        bot.group.position.addScaledVector(dirToPlayer, -bot.speed * 0.4 * delta);
      }
    } else {
      bot.group.position.add(new THREE.Vector3(Math.sin(bot.attackBias + state.battle.matchTime * 0.5), 0, Math.cos(bot.attackBias + state.battle.matchTime * 0.5)).multiplyScalar(1.4 * delta));
    }

    bot.group.rotation.y = -Math.atan2(dirToPlayer.x, dirToPlayer.z) + Math.PI;
    bot.group.position.y = 0;

    if (distance < 12 && bot.fireCooldown <= 0) {
      fireBotWeapon(bot);
    }
  }

  if (aliveBots.length === 0 && !state.battle.resultVisible) {
    showResult(true);
    state.battle.player.kills = state.battle.stats.kills;
  }
}

function updateSafeZone(delta) {
  if (!state.battle) return;
  const battle = state.battle;
  const player = battle.player;
  const zone = battle.safeZone;
  zone.shrinkTimer += delta;
  const radiusOffset = Math.max(10, 30 - Math.floor(zone.shrinkTimer / 5) * 2.5);
  zone.radius = Math.max(8, radiusOffset);
  if (zone.radius < 14) ui.zoneWarning.textContent = 'ЗОНА КРИТИЧНА';

  const dist = player.group.position.length();
  if (dist > zone.radius) {
    player.health -= 18 * delta;
  }
}

function updateMenu(delta) {
  menuHero.rotation.y += delta * 0.7;
  menuHero.position.y = Math.sin(state.menuPulse) * 0.22;
  state.menuPulse += delta * 2.4;
  menuParticles.rotation.y += delta * 0.12;
}

function resetJoysticks() {
  const movePad = document.getElementById('move-joystick');
  const joystickThumb = movePad.querySelector('.joystick-thumb');
  const moveRect = movePad.getBoundingClientRect();
  movePad.addEventListener('pointerdown', (event) => {
    event.preventDefault();
    const centerX = moveRect.left + moveRect.width / 2;
    const centerY = moveRect.top + moveRect.height / 2;
    const dx = event.clientX - centerX;
    const dy = event.clientY - centerY;
    const len = Math.min(42, Math.hypot(dx, dy));
    const angle = Math.atan2(dy, dx);
    const x = Math.cos(angle) * len;
    const y = Math.sin(angle) * len;
    joystickThumb.style.transform = `translate(${x}px, ${y}px)`;
    const normX = x / 42;
    const normY = y / 42;
    state.input.joystick.x = Math.max(-1, Math.min(1, normX));
    state.input.joystick.y = Math.max(-1, Math.min(1, normY));
    movePad.setPointerCapture(event.pointerId);
  });

  movePad.addEventListener('pointermove', (event) => {
    if (!movePad.hasPointerCapture(event.pointerId)) return;
    const rect = movePad.getBoundingClientRect();
    const cx = rect.left + rect.width / 2;
    const cy = rect.top + rect.height / 2;
    let dx = event.clientX - cx;
    let dy = event.clientY - cy;
    const len = Math.hypot(dx, dy);
    const max = 42;
    if (len > max) {
      const scale = max / len;
      dx *= scale;
      dy *= scale;
    }
    joystickThumb.style.transform = `translate(${dx}px, ${dy}px)`;
    state.input.joystick.x = Math.max(-1, Math.min(1, dx / max));
    state.input.joystick.y = Math.max(-1, Math.min(1, dy / max));
  });

  movePad.addEventListener('pointerup', () => {
    joystickThumb.style.transform = 'translate(-50%, -50%)';
    state.input.joystick.x = 0;
    state.input.joystick.y = 0;
  });

  movePad.addEventListener('pointercancel', () => {
    joystickThumb.style.transform = 'translate(-50%, -50%)';
    state.input.joystick.x = 0;
    state.input.joystick.y = 0;
  });

  const aimPad = document.getElementById('aim-pad');
  const aimDot = aimPad.querySelector('.aim-dot');
  aimPad.addEventListener('pointerdown', (event) => {
    event.preventDefault();
    aimPad.setPointerCapture(event.pointerId);
    handleAim(event, aimPad, aimDot);
  });
  aimPad.addEventListener('pointermove', (event) => {
    if (aimPad.hasPointerCapture(event.pointerId)) handleAim(event, aimPad, aimDot);
  });
  aimPad.addEventListener('pointerup', () => {
    aimDot.style.transform = 'translate(-50%, -50%)';
    state.input.aim.x = 0;
    state.input.aim.y = 0;
  });
}

function handleAim(event, pad, dot) {
  const rect = pad.getBoundingClientRect();
  const cx = rect.left + rect.width / 2;
  const cy = rect.top + rect.height / 2;
  const dx = event.clientX - cx;
  const dy = event.clientY - cy;
  const max = 34;
  const len = Math.hypot(dx, dy);
  const scale = len > max ? max / len : 1;
  const x = dx * scale;
  const y = dy * scale;
  dot.style.left = `${50 + (x / max) * 100}%`;
  dot.style.top = `${50 + (y / max) * 100}%`;
  state.input.aim.x = Math.max(-1, Math.min(1, x / max));
  state.input.aim.y = Math.max(-1, Math.min(1, y / max));
}

function animate() {
  requestAnimationFrame(animate);
  const delta = Math.min(0.033, 1 / 60);

  if (state.screen === 'menu') {
    updateMenu(delta);
  }

  if (state.screen === 'battle' && state.battle) {
    if (state.battle.started) {
      state.battle.matchTime += delta;
      state.battle.stats.timeElapsed = state.battle.matchTime;
      handleInput(delta);
      updateBots(delta);
      updateProjectiles(delta);
      updateSafeZone(delta);
      checkLootPickup();
      updateHUD();
      if (state.battle.player.health <= 0 && !state.battle.resultVisible) {
        showResult(false);
      }
    }
  }

  const cameraTarget = state.battle && state.battle.started ? state.battle.player.group.position.clone() : menuHero.position.clone();
  const idealCameraPos = cameraTarget.clone().add(new THREE.Vector3(0, 4, 9));
  camera.position.lerp(idealCameraPos, 0.08);
  camera.lookAt(cameraTarget.clone().add(new THREE.Vector3(0, 2.2, 0)));
  renderer.render(scene, camera);
}

renderHeroCards();
renderSkinCards();
renderMapCards();
setupButtons();
resetJoysticks();
selectHero('RAVEN');
selectSkin('Base');
selectMap('IRON VALLEY');
setScreen('menu');
animate();

window.addEventListener('resize', () => {
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(window.innerWidth, window.innerHeight);
});

window.addEventListener('keydown', (event) => {
  const key = event.key.toLowerCase();
  if (key === 'w' || key === 'arrowup') state.input.joystick.y = -1;
  if (key === 's' || key === 'arrowdown') state.input.joystick.y = 1;
  if (key === 'a' || key === 'arrowleft') state.input.joystick.x = -1;
  if (key === 'd' || key === 'arrowright') state.input.joystick.x = 1;
  if (key === ' ') state.input.fire = true;
  if (key === 'shift') state.input.run = true;
  if (key === 'q') state.input.dash = true;
  if (key === 'e') state.input.ultimate = true;
});

window.addEventListener('keyup', (event) => {
  const key = event.key.toLowerCase();
  if (['w', 's', 'arrowup', 'arrowdown'].includes(key)) state.input.joystick.y = 0;
  if (['a', 'd', 'arrowleft', 'arrowright'].includes(key)) state.input.joystick.x = 0;
  if (key === ' ') state.input.fire = false;
  if (key === 'shift') state.input.run = false;
  if (key === 'q') state.input.dash = false;
  if (key === 'e') state.input.ultimate = false;
});

window.addEventListener('pointermove', (event) => {
  if (state.screen !== 'battle') return;
  if (state.battle && state.battle.started) {
    const x = (event.clientX / window.innerWidth) * 2 - 1;
    const y = (event.clientY / window.innerHeight) * 2 - 1;
    state.input.aim.x = x;
    state.input.aim.y = y;
  }
});

window.addEventListener('pointerdown', (event) => {
  if (state.screen === 'battle' && state.battle && state.battle.started) {
    state.input.fire = true;
  }
});

window.addEventListener('pointerup', () => {
  state.input.fire = false;
});

function formatCountdown(value) {
  ui.countdown.textContent = String(value);
  ui.countdown.classList.remove('hidden');
  setTimeout(() => ui.countdown.classList.add('hidden'), 600);
}

export default null;

