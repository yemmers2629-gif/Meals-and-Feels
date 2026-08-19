<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Meals and Feels Tracker</title>
    <style>
        :root {
            --bg: #fafafa;
            --card-bg: #ffffff;
            --text: #262626;
            --secondary: #8e8e8e;
            --border: #dbdbdb;
            --primary: #0095f6;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background-color: var(--bg);
            color: var(--text);
            margin: 0;
            padding: 0;
            padding-bottom: 90px;
        }

        header {
            position: sticky;
            top: 0;
            background: var(--card-bg);
            border-bottom: 1px solid var(--border);
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 16px;
            z-index: 100;
        }

        header h1 {
            margin: 0;
            font-size: 18px;
            font-weight: 700;
        }

        .screen {
            display: none;
        }

        .screen.active {
            display: block;
        }

        .form-container {
            padding: 16px;
            max-width: 450px;
            margin: 0 auto;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            font-size: 12px;
            font-weight: 600;
            color: var(--secondary);
            text-transform: uppercase;
            margin-bottom: 8px;
        }

        .camera-trigger {
            border: 2px dashed var(--border);
            border-radius: 12px;
            text-align: center;
            padding: 40px 20px;
            background: #fff;
            cursor: pointer;
        }

        .camera-trigger input {
            display: none;
        }

        .preview-container {
            position: relative;
            display: none;
            width: 100%;
        }

        .preview-img {
            width: 100%;
            max-height: 400px;
            object-fit: cover;
            border-radius: 8px;
            display: block;
        }

        .retake-btn {
            position: absolute;
            top: 10px;
            right: 10px;
            background: rgba(0, 0, 0, 0.7);
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 20px;
            font-size: 12px;
            cursor: pointer;
        }

        input[type="text"], textarea {
            width: 100%;
            background: #fff;
            border: 1px solid var(--border);
            border-radius: 8px;
            color: #000;
            padding: 12px;
            font-size: 14px;
            box-sizing: border-box;
        }

        textarea {
            resize: none;
            height: 70px;
        }

        .heart-picker {
            display: flex;
            gap: 16px;
            font-size: 32px;
            cursor: pointer;
        }

        .emoji-picker {
            display: flex;
            gap: 20px;
            font-size: 32px;
            cursor: pointer;
        }

        .emoji-option {
            padding: 4px;
            border-radius: 50%;
            transition: 0.2s;
            opacity: 0.3;
            background: transparent;
            border: 2px solid transparent;
        }

        .emoji-option.selected {
            opacity: 1;
            background: #e6f2ff;
            transform: scale(1.15);
            border-color: var(--primary);
        }

        .save-btn {
            width: 100%;
            background: #ff3b30;
            color: white;
            border: none;
            padding: 14px;
            border-radius: 8px;
            font-weight: 600;
            font-size: 16px;
            cursor: pointer;
            margin-top: 10px;
        }

        .export-btn {
            width: 100%;
            background: #e0e0e0;
            color: #333;
            border: none;
            padding: 12px;
            border-radius: 8px;
            font-weight: 600;
            font-size: 14px;
            cursor: pointer;
            margin-top: 10px;
        }

        .feed-post {
            background: var(--card-bg);
            border-top: 1px solid var(--border);
            border-bottom: 1px solid var(--border);
            margin-bottom: 16px;
        }

        .feed-post-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 16px;
            font-weight: 600;
            font-size: 14px;
        }

        .feed-img {
            width: 100%;
            max-height: 450px;
            object-fit: cover;
            display: block;
        }

        .feed-content {
            padding: 12px 16px;
        }

        .feed-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 6px;
            font-size: 22px;
        }

        .feed-desc {
            font-size: 14px;
            color: #333;
            margin-top: 6px;
        }

        .feed-date {
            font-size: 11px;
            color: var(--secondary);
            text-transform: uppercase;
        }

        nav {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 100%;
            background: var(--card-bg);
            border-top: 1px solid var(--border);
            display: flex;
            justify-content: space-around;
            padding: 12px 0;
            z-index: 100;
        }

        nav button {
            background: none;
            border: none;
            font-size: 16px;
            font-weight: 600;
            color: #333;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <header>
        <h1 id="headerTitle">Meals and Feels</h1>
    </header>

    <!-- CREATE SCREEN -->
    <div id="createScreen" class="screen active">
        <div class="form-container">
            <div class="form-group">
                <label>Photo</label>
                <div class="camera-trigger" id="cameraTrigger" onclick="document.getElementById('nativeCameraInput').click()">
                    <span style="font-size: 48px;">📸</span>
                    <p style="margin: 8px 0 0 0; font-size: 14px; color: var(--secondary);">Tap to take photo or choose from library</p>
                    <input type="file" id="nativeCameraInput" accept="image/*" capture="environment" onchange="handlePhoto(event)">
                </div>
                
                <div class="preview-container" id="previewContainer">
                    <img id="imagePreview" class="preview-img" alt="Meal Preview">
                    <button class="retake-btn" onclick="triggerRetake()">Retake</button>
                </div>
            </div>

            <div class="form-group">
                <label>Food Name (Optional)</label>
                <input type="text" id="foodName" placeholder="e.g., Homemade Tacos">
            </div>

            <div class="form-group">
                <label>Rating (Hearts)</label>
                <div class="heart-picker" id="heartPicker">
                    <span onclick="setHearts(1)">🤍</span>
                    <span onclick="setHearts(2)">🤍</span>
                    <span onclick="setHearts(3)">🤍</span>
                    <span onclick="setHearts(4)">🤍</span>
                    <span onclick="setHearts(5)">🤍</span>
                </div>
            </div>

            <div class="form-group">
                <label>How do you feel?</label>
                <div class="emoji-picker" id="emojiPicker">
                    <span class="emoji-option" onclick="setEmoji('😍', this)">😍</span>
                    <span class="emoji-option" onclick="setEmoji('😊', this)">😊</span>
                    <span class="emoji-option" onclick="setEmoji('😢', this)">😢</span>
                    <span class="emoji-option" onclick="setEmoji('🤢', this)">🤢</span>
                </div>
            </div>

            <div class="form-group">
                <label>Notes (Optional)</label>
                <textarea id="foodDesc" placeholder="How was the experience?"></textarea>
            </div>

            <button class="save-btn" onclick="saveMealPost()">Save Meal</button>
        </div>
    </div>

    <!-- FEED SCREEN -->
    <div id="feedScreen" class="screen">
        <div id="feedContainer"></div>
        <div style="padding: 0 16px 25px 16px;">
            <button class="export-btn" onclick="exportData()">Export Data (JSON)</button>
        </div>
    </div>

    <!-- BOTTOM NAVIGATION -->
    <nav>
        <button onclick="switchTab('create')">📸 New Meal</button>
        <button onclick="switchTab('feed')">🏠 View Feed</button>
    </nav>

<script>
    let photoDataUrl = '';
    let selectedHeartCount = 0;
    let selectedMoodEmoji = '';

    function switchTab(tab) {
        document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
        if (tab === 'feed') {
            document.getElementById('feedScreen').classList.add('active');
            document.getElementById('headerTitle').innerText = 'Your Meal Feed';
            renderFeed();
        } else {
            document.getElementById('createScreen').classList.add('active');
            document.getElementById('headerTitle').innerText = 'Meals and Feels';
        }
    }

    function handlePhoto(event) {
        const file = event.target.files[0];
        if (file) {
            const reader = new FileReader();
            reader.onload = function(e) {
                photoDataUrl = e.target.result;
                document.getElementById('imagePreview').src = photoDataUrl;
                document.getElementById('cameraTrigger').style.display = 'none';
                document.getElementById('previewContainer').style.display = 'block';
            }
            reader.readAsDataURL(file);
        }
    }

    function triggerRetake() {
        photoDataUrl = '';
        document.getElementById('nativeCameraInput').value = '';
        document.getElementById('previewContainer').style.display = 'none';
        document.getElementById('cameraTrigger').style.display = 'block';
    }

    function setHearts(count) {
        selectedHeartCount = count;
        const hearts = document.querySelectorAll('#heartPicker span');
        hearts.forEach((h, index) => {
            h.innerText = index < count ? '❤️' : '🤍';
        });
    }

    function setEmoji(emoji, element) {
        selectedMoodEmoji = emoji;
        document.querySelectorAll('.emoji-option').forEach(e => e.classList.remove('selected'));
        element.classList.add('selected');
    }

    function saveMealPost() {
        if (!photoDataUrl) {
            alert('Please add a photo first!');
            return;
        }

        const posts = JSON.parse(localStorage.getItem('meals_and_feels_data') || '[]');
        const newPost = {
            image: photoDataUrl,
            name: document.getElementById('foodName').value,
            hearts: '❤️'.repeat(selectedHeartCount) || '🤍',
            emoji: selectedMoodEmoji,
            desc: document.getElementById('foodDesc').value,
            date: new Date().toLocaleDateString()
        };

        posts.unshift(newPost);
        localStorage.setItem('meals_and_feels_data', JSON.stringify(posts));

        // Reset Form Inputs
        photoDataUrl = '';
        selectedHeartCount = 0;
        selectedMoodEmoji = '';
        document.getElementById('nativeCameraInput').value = '';
        document.getElementById('foodName').value = '';
        document.getElementById('foodDesc').value = '';
        document.getElementById('previewContainer').style.display = 'none';
        document.getElementById('cameraTrigger').style.display = 'block';
        document.querySelectorAll('#heartPicker span').forEach(h => h.innerText = '🤍');
        document.querySelectorAll('.emoji-option').forEach(e => e.classList.remove('selected'));

        switchTab('feed');
    }

    function renderFeed() {
        const container = document.getElementById('feedContainer');
        const posts = JSON.parse(localStorage.getItem('meals_and_feels_data') || '[]');

        if (posts.length === 0) {
            container.innerHTML = `<div style="text-align: center; padding: 60px 20px; color: var(--secondary);">No meals logged yet. Tap "New Meal" below to share your first post!</div>`;
            return;
        }

        container.innerHTML = '';
        posts.forEach(p => {
            const postDiv = document.createElement('div');
            postDiv.className = 'feed-post';
            postDiv.innerHTML = `
                <div class="feed-post-header">
                    <span>${p.name || 'Unnamed Meal'}</span>
                    <span style="font-size: 24px;">${p.emoji || ''}</span>
                </div>
                <img src="${p.image}" class="feed-img" alt="Food Photo">
                <div class="feed-content">
                    <div class="feed-row">
                        <span>${p.hearts}</span>
                        <span class="feed-date">${p.date}</span>
                    </div>
                    ${p.desc ? `<div class="feed-desc"><b>${p.name ? p.name + ' — ' : ''}</b>${p.desc}</div>` : (p.name ? `<div class="feed-desc"><b>${p.name}</b></div>` : '')}
                </div>
            `;
            container.appendChild(postDiv);
        });
    }

    function exportData() {
        const data = localStorage.getItem('meals_and_feels_data') || '[]';
        const blob = new Blob([data], { type: 'application/json' });
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = 'meals_and_feels_backup.json';
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
    }
</script>
</body>
</html>
