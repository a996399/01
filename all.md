## 最新导航页代码
```
//需要环境变量BB
//env.CARD_ORDER是KV名称、KV桶自定义
//env.BB是密码
// 定義 HTML 內容，包含前端頁面的結構、樣式和腳本
const HTML_CONTENT = `<!DOCTYPE html><html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SUOU AKI</title> /*这是主题*/
<style>
/* 設置頁面整體高度和基本樣式 */
html, body {
    height: 100%;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
@media (max-width: 600px) {
    body {
        padding: 5px;
        font-size: 15px;
    }
    .sidebar {
        position: static;
        width: 100%;
        margin-bottom: 10px;
        left: 0;
        top: 0;
        border-radius: 8px;
        padding: 8px;
        font-size: 15px;
        max-height: 180px;
        overflow-y: auto;
        scrollbar-width: thin;
    }
    .sidebar::-webkit-scrollbar {
        width: 6px;
    }
    .sidebar::-webkit-scrollbar-thumb {
        background: #b3e0ff;
        border-radius: 3px;
    }
    .card-container {
        grid-template-columns: repeat(2, 1fr);
        gap: 6px;
    }
    .card {
        width: 100%;
        min-width: 0;
        padding: 6px;
        font-size: 13px;
    }
    .section-title {
        font-size: 22px;
    }
    h1 {
        font-size: 22px !important;
    }
    .admin-controls, .customization-controls {
        position: static;
        font-size: 80%;
    }
    #theme-toggle {
        left: unset;
        right: 10px;
        bottom: 10px;
    }
}
/* 頁面主體樣式：設置背景、字體、佈局 */
body {
    font-family: Arial, sans-serif;
    background-color:rgb(199, 255, 255);
    background-image: url('https://mig01.996399.xyz/illust_100271795_20230408_132106.png');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    background-attachment: fixed;
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
    transition: background-color 0.3s ease;
    min-height: 100vh;
}
/* 側邊欄樣式 */
.sidebar {
    width: 200px;
    position: fixed;
    left: 20px;
    top: 20px;
    background-color: rgb(164, 252, 255);
    border-radius: 10px;
    padding: 15px;
    height: fit-content;
    max-height: 70vh;
    overflow-y: auto;
    scrollbar-width: thin;
}
.sidebar::-webkit-scrollbar {
    width: 6px;
}
.sidebar::-webkit-scrollbar-thumb {
    background:rgb(238, 248, 255);
    border-radius: 3px;
}
/* 側邊欄項目樣式 */
.sidebar-item {
    padding: 10px;
    margin: 5px 0;
    cursor: pointer;
    border-radius: 5px;
    transition: background-color 0.2s;
}
.sidebar-item:hover {
    background-color: rgba(0, 123, 255, 0.1);
}
.sidebar-item.active {
    background-color: #007bff;
    color: white;
}
/* 卡片容器 */
.card-container {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    gap: 10px;
}
/* 卡片樣式 */
.card {
    display: flex;
    flex-direction: column;
    position: relative;
    background-color: #a0c9e5;
    padding: 10px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    cursor: grab;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
    width: 200px;
    height: auto;
}
.card-top {
    display: flex;
    align-items: center;
    margin-bottom: 5px;
}
.card-icon {
    width: 24px;
    height: 24px;
    margin-right: 10px;
}
.card-title {
    font-size: 16px;
    font-weight: bold;
}
.card-description {
    color: #555;
    font-size: 12px;
    word-break: break-all;
}
.card.dragging {
    opacity: 0.8;
    transform: scale(1.05);
    cursor: grabbing;
}
.card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}
.delete-btn {
    position: absolute;
    top: -10px;
    right: -10px;
    background-color: red;
    color: white;
    border: none;
    border-radius: 50%;
    width: 20px;
    height: 20px;
    text-align: center;
    font-size: 14px;
    line-height: 20px;
    cursor: pointer;
    display: none;
}
/* 管理員控制面板 */
.admin-controls {
    display: none;
    position: fixed;
    top: 10px;
    right: 10px;
    font-size: 60%;
}
.admin-controls input {
    padding: 5px;
    font-size: 60%;
}
.admin-controls button {
    padding: 5px 10px;
    font-size: 60%;
    margin-left: 10px;
}
/* 新增/刪除/保存控制項 */
.add-remove-controls {
    display: none;
    margin-top: 10px;
    flex-direction: row;
    gap: 10px;
}
.round-btn {
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 50%;
    width: 40px;
    height: 40px;
    text-align: center;
    font-size: 24px;
    line-height: 40px;
    cursor: pointer;
}
/* 主題切換按鈕 */
#theme-toggle {
    position: fixed;
    bottom: 10px;
    left: 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 50%;
    width: 40px;
    height: 40px;
    text-align: center;
    font-size: 24px;
    line-height: 40px;
    cursor: pointer;
}
/* 對話框遮罩 */
#dialog-overlay {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    justify-content: center;
    align-items: center;
}
/* 對話框 */
#dialog-box {
    background: white;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}
#dialog-box label {
    display: block;
    margin-bottom: 5px;
}
#dialog-box input, #dialog-box textarea {
    width: 100%;
    padding: 5px;
    margin-bottom: 10px;
}
/* 勾選框組 */
.checkbox-group {
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 5px;
    display: flex;
    flex-direction: column;
    overflow-y: auto;
    max-height: 200px;
    gap: 6px;
    scrollbar-width: thin;
}
.checkbox-group::-webkit-scrollbar {
    width: 6px;
}
.checkbox-group::-webkit-scrollbar-thumb {
    background: #b3e0ff;
    border-radius: 3px;
}
.checkbox-group label.category-select-label {
    display: flex;
    align-items: center;
    margin-bottom: 2px;
    font-size: 14px;
    padding: 5px 10px;
    border-radius: 6px;
    cursor: pointer;
    user-select: none;
    transition: background 0.2s, color 0.2s;
}
.checkbox-group label.category-select-label.selected {
    background: #007bff;
    color: #fff;
    font-weight: bold;
}
.checkbox-group label.category-select-label:not(.selected):hover {
    background: #e6f0ff;
    color: #007bff;
}
.checkbox-group input {
    margin-right: 5px;
    width: 16px;
    height: 16px;
}
/* 分類區塊 */
.section {
    margin-bottom: 20px;
}
.section-title {
    font-size: 50px;
    font-weight: bold;
    color: rgba(215, 247, 255, 0.78);
    margin-bottom: 15px;
}
/* 自訂控制項 */
.customization-controls {
    display: none;
    margin-top: 10px;
    font-size: 60%;
}
.customization-controls label {
    margin-right: 5px;
}
</style>
</head>
<body>
<div class="sidebar" id="sidebar"></div>
<h1>SUOU AKI 導航頁</h1>
<div class="admin-controls">
    <input type="password" id="admin-password" placeholder="輸入密碼">
    <button id="admin-mode-btn" onclick="toggleAdminMode()">進入管理模式</button>
</div>
<div class="add-remove-controls">
    <button class="round-btn" onclick="showAddDialog()">+</button>
    <button class="round-btn" onclick="toggleRemoveMode()">-</button>
</div>
<div class="customization-controls">
    <label>主標題顏色:</label>
    <input type="color" id="main-title-color">
    <label>主標題大小(px):</label>
    <input type="number" id="main-title-size" min="10" max="50">
    <button onclick="saveMainTitleStyles()">應用</button>
</div>
<div id="sections-container"></div>
<button id="theme-toggle" onclick="toggleTheme()">◑</button>
<div id="dialog-overlay">
    <div id="dialog-box">
        <label for="name-input">名稱</label>
        <input type="text" id="name-input">
        <label for="url-input">地址</label>
        <input type="text" id="url-input">
        <label for="description-input">簡介</label>
        <textarea id="description-input" rows="4"></textarea>
        <label>選擇分類（可多選）</label>
        <div class="checkbox-group" id="category-checkboxes"></div>
<script>
// 滾動到選中的分類（手機體驗優化）
document.addEventListener('click', function(e) {
    if (e.target && e.target.name === 'category') {
        e.target.scrollIntoView({behavior: 'smooth', inline: 'center'});
    }
});
</script>
        <button onclick="addLink()">確定</button>
        <button onclick="hideAddDialog()">取消</button>
    </div>
</div>
<script>
let isAdmin = false;
let removeMode = false;
let isDarkTheme = false;
let links = [];
const categories = {
    "我的服務": [],
    "社交媒體": [],
    "音樂": [],
    "視頻": [],
    "圖站/桌布": [],
    "軟體-Android": [],
    "軟體-ios": [],
    "軟體-windwos": [],
    "測速/IP檢查": [],
    "遊戲娛樂": [],
    "通訊交友": [],
    "金融投資-股票": [],
    "金融投資-虛擬貨幣": [],
    "域名": [],
    "伺服器": [],
    "SIM/ESIM": [],
    "跨境支付": [],
    "境外银行": [],
    "海外購物": [],
    "轉運公司": [],
    "AI": [],
    "技術論壇": [],
    "工具": [],
    "檢索引擎": [],
    "文章推薦": [],
    "友鏈": []
};
const backgroundImages = [
    'https://mig01.996399.xyz/illust_100271795_20230408_132106.png',
    'https://img.996399.xyz/file/1745340768591_illust_79807334_20240509_025559.jpg',
    'https://mig01.996399.xyz/illust_115758338_20240710_045330.png',
    'https://mig01.996399.xyz/illust_92217855_20230408_132312.png',
    'https://mig01.996399.xyz/illust_92246778_20230326_164515.png',
    'https://mig01.996399.xyz/illust_120282671_20240710_034934.png',
    'https://mig01.996399.xyz/illust_109277225_20240420_013312.jpg',
    'https://img.996399.xyz/file/1745516991503_20230321_185007.jpg',
    'https://img.996399.xyz/file/1745517163071_FB_IMG_1726012639501.jpg',
    'https://img.996399.xyz/file/1745517174916_illust_109283065_20240929_022823.jpg',
    'https://img.996399.xyz/file/1745517409647_illust_122809108_20241005_203650.png',
    'https://img.996399.xyz/file/1745517413191_illust_122809108_20241005_203645.png'
];
function setRandomBackground() {
    const randomIndex = Math.floor(Math.random() * backgroundImages.length);
    document.body.style.backgroundImage = 'url(' + backgroundImages[randomIndex] + ')';
}
function startBackgroundRotation() {
    setRandomBackground();
    setInterval(setRandomBackground, 100000);
}
async function loadLinks() {
    const response = await fetch('/api/getLinks?userId=testUser');
    links = await response.json();
    Object.keys(categories).forEach(key => categories[key] = []);
    links.forEach(link => {
        if (link.categories && Array.isArray(link.categories)) {
            link.categories.forEach(category => {
                if (categories[category]) categories[category].push(link);
            });
        }
    });
    await loadStyles();
    loadSections();
    updateCategoryCheckboxes();
    startBackgroundRotation();
    if (window.location.pathname === '/admin') {
        document.querySelector('.admin-controls').style.display = 'block';
    }
}
async function loadStyles() {
    const mainStyles = await fetch('/api/getStyles?userId=testUser&type=mainTitle').then(res => res.json()).catch(() => ({}));
    if (mainStyles.color) {
        document.querySelector('h1').style.color = mainStyles.color;
        document.getElementById('main-title-color').value = mainStyles.color;
    }
    if (mainStyles.fontSize) {
        document.querySelector('h1').style.fontSize = mainStyles.fontSize + 'px';
        document.getElementById('main-title-size').value = mainStyles.fontSize;
    }
}
function loadSections() {
    const container = document.getElementById('sections-container');
    const sidebar = document.getElementById('sidebar');
    container.innerHTML = '';
    sidebar.innerHTML = '';
    Object.keys(categories).forEach(category => {
        const sidebarItem = document.createElement('div');
        sidebarItem.className = 'sidebar-item';
        sidebarItem.textContent = category;
        sidebarItem.dataset.category = category;
        sidebarItem.onclick = function() {
            document.getElementById(category).scrollIntoView({ behavior: 'smooth' });
            sidebar.querySelectorAll('.sidebar-item').forEach(item => item.classList.remove('active'));
            sidebarItem.classList.add('active');
        };
        sidebar.appendChild(sidebarItem);
        const section = document.createElement('div');
        section.className = 'section';
        section.id = category;
        const title = document.createElement('div');
        title.className = 'section-title';
        title.textContent = category;
        const cardContainer = document.createElement('div');
        cardContainer.className = 'card-container';
        cardContainer.id = category;
        section.appendChild(title);
        section.appendChild(cardContainer);
        categories[category].forEach(link => createCard(link, cardContainer));
        container.appendChild(section);
    });
    if (sidebar.children.length > 0) sidebar.children[0].classList.add('active');
}
function createCard(link, container) {
    const card = document.createElement('div');
    card.className = 'card';
    card.setAttribute('draggable', isAdmin);
    const cardTop = document.createElement('div');
    cardTop.className = 'card-top';
    const icon = document.createElement('img');
    icon.className = 'card-icon';
    icon.src = 'https://favicon.zhusl.com/ico?url=' + link.url;
    icon.alt = '網站圖標';
    const title = document.createElement('div');
    title.className = 'card-title';
    title.textContent = link.name;
    cardTop.appendChild(icon);
    cardTop.appendChild(title);
    const description = document.createElement('div');
    description.className = 'card-description';
    description.textContent = link.description || '無簡介';
    card.appendChild(cardTop);
    card.appendChild(description);
    function correctUrl(url) {
        if (url.startsWith('http://') || url.startsWith('https://')) return url;
        return 'http://' + url;
    }
    let correctedUrl = correctUrl(link.url);
    if (!isAdmin) {
        card.addEventListener('click', () => window.open(correctedUrl, '_blank'));
    }
    const deleteBtn = document.createElement('button');
    deleteBtn.textContent = '–';
    deleteBtn.className = 'delete-btn';
    deleteBtn.onclick = function(event) {
        event.stopPropagation();
        removeCard(card, link, container.id);
    };
    card.appendChild(deleteBtn);
    if (isDarkTheme) {
        card.style.backgroundColor = '#1e1e1e';
        card.style.color = '#ffffff';
        card.style.boxShadow = '0 4px 8px rgba(0, 0, 0, 0.5)';
    } else {
        card.style.backgroundColor = '#a0c9e5';
        card.style.color = '#333';
        card.style.boxShadow = '0 4px 8px rgba(0, 0, 0, 0.1)';
    }
    card.addEventListener('dragstart', dragStart);
    card.addEventListener('dragover', dragOver);
    card.addEventListener('dragend', dragEnd);
    card.addEventListener('drop', drop);
    if (isAdmin && removeMode) deleteBtn.style.display = 'block';
    container.appendChild(card);
}
function updateCategoryCheckboxes() {
    const checkboxGroup = document.getElementById('category-checkboxes');
    checkboxGroup.innerHTML = '';
    // 记录已选分类
    if (!window.selectedCategories) window.selectedCategories = [];
    Object.keys(categories).forEach(category => {
        const label = document.createElement('label');
        label.textContent = category;
        label.className = 'category-select-label';
        if (window.selectedCategories.includes(category)) {
            label.classList.add('selected');
        }
        label.onclick = function() {
            const idx = window.selectedCategories.indexOf(category);
            if (idx === -1) {
                window.selectedCategories.push(category);
                label.classList.add('selected');
            } else {
                window.selectedCategories.splice(idx, 1);
                label.classList.remove('selected');
            }
        };
        checkboxGroup.appendChild(label);
    });
}
async function saveLinks() {
    const uniqueLinks = [];
    const seen = new Set();
    for (const category in categories) {
        categories[category].forEach(link => {
            const linkKey = link.name + '|' + link.url + '|' + link.description;
            if (!seen.has(linkKey)) {
                seen.add(linkKey);
                uniqueLinks.push(link);
            }
        });
    }
    await fetch('/api/saveOrder', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ userId: 'testUser', links: uniqueLinks })
    });
}
async function saveMainTitleStyles() {
    const color = document.getElementById('main-title-color').value;
    const fontSize = document.getElementById('main-title-size').value;
    document.querySelector('h1').style.color = color;
    document.querySelector('h1').style.fontSize = fontSize + 'px';
    await fetch('/api/saveStyles', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ userId: 'testUser', type: 'mainTitle', styles: { color, fontSize } })
    });
}
async function saveChanges() {
    if (!isAdmin) return;
    await saveCardOrder();
    await saveLinks();
}
function addLink() {
    const name = document.getElementById('name-input').value;
    const url = document.getElementById('url-input').value;
    const description = document.getElementById('description-input').value;
    const selectedCategories = window.selectedCategories || [];
    if (name && url && selectedCategories.length > 0) {
        const newLink = { name, url, description, categories: selectedCategories.slice() };
        selectedCategories.forEach(category => {
            if (categories[category]) {
                categories[category].push(newLink);
                const container = document.getElementById(category);
                createCard(newLink, container);
            }
        });
        links.push(newLink);
        saveLinks();
        document.getElementById('name-input').value = '';
        document.getElementById('url-input').value = '';
        document.getElementById('description-input').value = '';
        window.selectedCategories = [];
        updateCategoryCheckboxes();
        hideAddDialog();
    } else {
        alert('請填寫名稱、地址並至少選擇一個分類');
    }
}
function removeCard(card, link, category) {
    console.log('Removing card from category:', category, link);
    link.categories = link.categories.filter(cat => cat !== category);
    console.log('Updated categories:', link.categories);
    categories[category] = categories[category].filter(l => l !== link);
    if (link.categories.length === 0) {
        const index = links.findIndex(l => l.name === link.name && l.url === link.url && l.description === link.description);
        if (index !== -1) {
            links.splice(index, 1);
        }
    }
    card.remove();
    saveLinks();
}
let draggedCard = null;
function dragStart(event) {
    if (!isAdmin) return;
    draggedCard = event.target;
    draggedCard.dataset.originalContainer = draggedCard.parentElement.id;
    draggedCard.classList.add('dragging');
    event.dataTransfer.effectAllowed = "move";
}
function dragOver(event) {
    if (!isAdmin) return;
    event.preventDefault();
    const target = event.target.closest('.card') || event.target.closest('.card-container');
    if (target && target !== draggedCard) {
        const container = target.className.includes('card-container') ? target : target.parentElement;
        const mousePositionX = event.clientX;
        if (target.className.includes('card')) {
            const targetRect = target.getBoundingClientRect();
            if (mousePositionX < targetRect.left + targetRect.width / 2) {
                container.insertBefore(draggedCard, target);
            } else {
                container.insertBefore(draggedCard, target.nextSibling);
            }
        } else {
            container.appendChild(draggedCard);
        }
    }
}
function drop(event) {
    if (!isAdmin) return;
    event.preventDefault();
    draggedCard.classList.remove('dragging');
    const newContainer = draggedCard.parentElement;
    const oldContainer = draggedCard.dataset.originalContainer;
    const link = links.find(l => l.name === draggedCard.querySelector('.card-title').textContent);
    if (newContainer.id !== oldContainer && link) {
        link.categories = link.categories.filter(cat => cat !== oldContainer);
        if (!link.categories.includes(newContainer.id)) {
            link.categories.push(newContainer.id);
        }
        categories[oldContainer] = categories[oldContainer].filter(l => l !== link);
        if (!categories[newContainer.id].includes(link)) {
            categories[newContainer.id].push(link);
        }
    }
    draggedCard = null;
    saveCardOrder();
}
function dragEnd(event) {
    if (draggedCard) {
        draggedCard.classList.remove('dragging');
    }
}
async function saveCardOrder() {
    if (!isAdmin) return;
    const containers = document.querySelectorAll('.card-container');
    Object.keys(categories).forEach(category => categories[category] = []);
    containers.forEach(container => {
        const category = container.id;
        [...container.children].forEach(card => {
            const name = card.querySelector('.card-title').textContent;
            const description = card.querySelector('.card-description').textContent;
            const link = links.find(l => l.name === name && (l.description || '無簡介') === description);
            if (link && !categories[category].includes(link)) {
                categories[category].push(link);
            }
        });
    });
    const uniqueLinks = [];
    const seen = new Set();
    for (const category in categories) {
        categories[category].forEach(link => {
            const linkKey = link.name + '|' + link.url + '|' + link.description;
            if (!seen.has(linkKey)) {
                seen.add(linkKey);
                uniqueLinks.push(link);
            }
        });
    }
    links = uniqueLinks;
    await fetch('/api/saveOrder', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ userId: 'testUser', links })
    });
}
function toggleAdminMode() {
    const passwordInput = document.getElementById('admin-password');
    const adminBtn = document.getElementById('admin-mode-btn');
    const addRemoveControls = document.querySelector('.add-remove-controls');
    const customizationControls = document.querySelector('.customization-controls');
    if (!isAdmin) {
        verifyPassword(passwordInput.value).then(isValid => {
            if (isValid) {
                isAdmin = true;
                adminBtn.textContent = "退出管理模式";
                addRemoveControls.style.display = 'flex';
                customizationControls.style.display = 'block';
                reloadCardsAsAdmin();
                if (window.location.pathname === '/admin') {
                    window.history.pushState({}, '', '/');
                }
            }
        });
    } else {
        isAdmin = false;
        removeMode = false;
        adminBtn.textContent = "進入管理模式";
        addRemoveControls.style.display = 'none';
        customizationControls.style.display = 'none';
        const deleteButtons = document.querySelectorAll('.delete-btn');
        deleteButtons.forEach(btn => btn.style.display = 'none');
        reloadCardsAsAdmin();
    }
    passwordInput.value = '';
}
function reloadCardsAsAdmin() {
    document.querySelectorAll('.card-container').forEach(container => container.innerHTML = '');
    loadLinks();
}
function applyDarkTheme() {
    document.body.style.backgroundColor = '#121212';
    document.body.style.color = '#ffffff';
    const cards = document.querySelectorAll('.card');
    cards.forEach(card => {
        card.style.backgroundColor = '#1e1e1e';
        card.style.color = '#ffffff';
        card.style.boxShadow = '0 4px 8px rgba(0, 0, 0, 0.5)';
    });
}
function showAddDialog() {
    document.getElementById('dialog-overlay').style.display = 'flex';
}
function hideAddDialog() {
    document.getElementById('dialog-overlay').style.display = 'none';
}
function toggleRemoveMode() {
    removeMode = !removeMode;
    const deleteButtons = document.querySelectorAll('.delete-btn');
    deleteButtons.forEach(btn => btn.style.display = removeMode ? 'block' : 'none');
}
function toggleTheme() {
    isDarkTheme = !isDarkTheme;
    document.body.style.backgroundColor = isDarkTheme ? '#121212' : '#d8eac4';
    document.body.style.color = isDarkTheme ? '#ffffff' : '#333';
    const cards = document.querySelectorAllPETITE-VUE-CREATE-APP('.card');
    cards.forEach(card => {
        card.style.backgroundColor = isDarkTheme ? '#1e1e1e' : '#a0c9e5';
        card.style.color = isDarkTheme ? '#ffffff' : '#333';
        card.style.boxShadow = isDarkTheme ? '0 4px 8px rgba(0, 0, 0, 0.5)' : '0 4px 8px rgba(0, 0, 0, 0.1)';
    });
    const dialogBox = document.getElementById('dialog-box');
    dialogBox.style.backgroundColor = isDarkTheme ? '#1e1e1e' : '#ffffff';
    dialogBox.style.color = isDarkTheme ? '#ffffff' : '#333';
    const inputs = dialogBox.querySelectorAll('input, textarea');
    inputs.forEach(input => {
        input.style.backgroundColor = isDarkTheme ? '#333333' : '#ffffff';
        input.style.color = isDarkTheme ? '#ffffff' : '#333';
    });
}
async function verifyPassword(inputPassword) {
    const response = await fetch('/api/verifyPassword', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ password: inputPassword })
    });
    const result = await response.json();
    return result.valid;
}
loadLinks();
</script>
</body>
</html>`;

// Cloudflare Worker 處理請求
export default {
    async fetch(request, env) {
        const url = new URL(request.url);
        if (url.pathname === '/' || url.pathname === '/admin') {
            return new Response(HTML_CONTENT, {
                headers: { 'Content-Type': 'text/html' }
            });
        }
        if (url.pathname === '/api/getLinks') {
            const userId = url.searchParams.get('userId');
            const links = await env.CARD_ORDER.get(userId);
            return new Response(links || JSON.stringify([]), { status: 200 });
        }
        if (url.pathname === '/api/saveOrder' && request.method === 'POST') {
            const { userId, links } = await request.json();
            await env.CARD_ORDER.put(userId, JSON.stringify(links));
            return new Response(JSON.stringify({ success: true }), { status: 200 });
        }
        if (url.pathname === '/api/verifyPassword' && request.method === 'POST') {
            const { password } = await request.json();
            const isValid = password === env.BB; /*环境变量密码*/
            return new Response(JSON.stringify({ valid: isValid }), {
                status: isValid ? 200 : 403,
                headers: { 'Content-Type': 'application/json' }
            });
        }
        if (url.pathname === '/api/getStyles') {
            const userId = url.searchParams.get('userId');
            const type = url.searchParams.get('type');
            const styles = await env.CARD_ORDER.get(userId + '_' + type);
            return new Response(styles || JSON.stringify({}), { status: 200 });
        }
        if (url.pathname === '/api/saveStyles' && request.method === 'POST') {
            const { userId, type, styles } = await request.json();
            await env.CARD_ORDER.put(userId + '_' + type, JSON.stringify(styles));
            return new Response(JSON.stringify({ success: true }), { status: 200 });
        }
        return new Response('未找到', { status: 404 });
    }
};

```

