{
  "rewrites": [
    { "source": "/(.*)", "destination": "/" }
  ]
}
index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Growth Purpose 🪴 - Personal Development Hub</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #001F3F 0%, #7A3FF2 100%);
            color: white;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
        }

        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            background: linear-gradient(45deg, #fff, #7A3FF2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .header p {
            font-size: 1.2rem;
            opacity: 0.9;
        }

        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 30px;
            margin-bottom: 30px;
        }

        .feature-card {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .feature-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 40px rgba(122, 63, 242, 0.3);
        }

        .feature-title {
            font-size: 1.5rem;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .feature-icon {
            font-size: 1.8rem;
        }

        .input-group {
            margin-bottom: 15px;
        }

        .input-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: 500;
        }

        .input-group input, .input-group textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid rgba(255, 255, 255, 0.3);
            border-radius: 10px;
            background: rgba(255, 255, 255, 0.1);
            color: white;
            font-size: 16px;
        }

        .input-group input::placeholder, .input-group textarea::placeholder {
            color: rgba(255, 255, 255, 0.6);
        }

        .btn {
            background: linear-gradient(45deg, #7A3FF2, #001F3F);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 10px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            width: 100%;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(122, 63, 242, 0.4);
        }

        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .entries-list {
            max-height: 300px;
            overflow-y: auto;
            margin-top: 20px;
        }

        .entry-item {
            background: rgba(255, 255, 255, 0.1);
            padding: 12px;
            border-radius: 8px;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .delete-btn {
            background: #ff4757;
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 12px;
        }

        .tip-item {
            background: rgba(255, 255, 255, 0.1);
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .tip-icon {
            font-size: 2rem;
            margin-bottom: 10px;
            display: block;
        }

        .result-box {
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 10px;
            padding: 20px;
            margin-top: 20px;
            display: none;
        }

        .result-box.show {
            display: block;
        }

        .error-message {
            background: rgba(255, 71, 87, 0.2);
            border: 1px solid #ff4757;
            color: #ff4757;
            padding: 15px;
            border-radius: 10px;
            margin-top: 15px;
        }

        .success-message {
            background: rgba(46, 213, 115, 0.2);
            border: 1px solid #2ed573;
            color: #2ed573;
            padding: 15px;
            border-radius: 10px;
            margin-top: 15px;
        }

        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(5px);
        }

        .modal-content {
            background: linear-gradient(135deg, #001F3F 0%, #7A3FF2 100%);
            margin: 10% auto;
            padding: 0;
            border-radius: 20px;
            width: 90%;
            max-width: 500px;
            border: 2px solid rgba(255, 255, 255, 0.3);
            animation: modalSlide 0.3s ease-out;
        }

        @keyframes modalSlide {
            from { transform: translateY(-50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        .modal-header {
            padding: 25px 30px 0;
            text-align: center;
        }

        .modal-header h2 {
            color: white;
            margin: 0;
            font-size: 1.8rem;
        }

        .modal-body {
            padding: 20px 30px;
            color: white;
            text-align: center;
        }

        .modal-body p {
            margin: 10px 0;
            line-height: 1.6;
        }

        .blocked-url {
            background: rgba(255, 255, 255, 0.1);
            padding: 10px;
            border-radius: 8px;
            margin: 15px 0;
            font-size: 0.9rem;
            word-break: break-all;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .modal-footer {
            padding: 0 30px 30px;
            display: flex;
            gap: 15px;
            justify-content: center;
        }

        .btn-override {
            background: linear-gradient(45deg, #ff4757, #ff6b7a);
            flex: 1;
        }

        .btn-stay {
            background: linear-gradient(45deg, #2ed573, #7bed9f);
            flex: 1;
        }

        .blocker-status {
            display: grid;
            grid-template-columns: 1fr;
            gap: 15px;
        }

        .entry-timestamp {
            font-size: 0.8rem;
            opacity: 0.7;
            margin-top: 5px;
        }

        @media (max-width: 768px) {
            .features-grid {
                grid-template-columns: 1fr;
            }
            
            .header h1 {
                font-size: 2rem;
            }

            .modal-content {
                width: 95%;
                margin: 5% auto;
            }

            .modal-footer {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>The Growth Purpose 🪴</h1>
            <p>Your Personal Development Hub - Track, Learn & Grow</p>
        </div>

        <div class="features-grid">
            <!-- Screen Time Tracker -->
            <div class="feature-card">
                <h2 class="feature-title">
                    <span class="feature-icon">📱</span>
                    Screen Time Tracker
                </h2>
                <div class="input-group">
                    <label for="app-name">App Name</label>
                    <input type="text" id="app-name" placeholder="e.g., Instagram, TikTok, YouTube">
                </div>
                <div class="input-group">
                    <label for="time-spent">Time Used</label>
                    <input type="text" id="time-spent" placeholder="e.g., 2 hours, 45 minutes">
                </div>
                <button class="btn" onclick="addScreenTime()">Add Entry</button>
                
                <div class="entries-list" id="screen-time-list">
                    <!-- Screen time entries will be populated here -->
                </div>
            </div>

            <!-- Reels & Shorts Blocker -->
            <div class="feature-card">
                <h2 class="feature-title">
                    <span class="feature-icon">🚫</span>
                    Reels & Shorts Blocker
                </h2>
                <p style="margin-bottom: 20px; opacity: 0.9;">Automatically blocks Instagram Reels and YouTube Shorts</p>
                
                <div class="blocker-status">
                    <div class="tip-item">
                        <span class="tip-icon">🛡️</span>
                        <strong>Protection Active</strong>
                        <p>Blocking Instagram Reels and YouTube Shorts automatically</p>
                    </div>
                    <div class="tip-item">
                        <span class="tip-icon">⚠️</span>
                        <strong>Override Available</strong>
                        <p>Click override on warning to temporarily access blocked content</p>
                    </div>
                </div>
            </div>

            <!-- Feedback Feature -->
            <div class="feature-card">
                <h2 class="feature-title">
                    <span class="feature-icon">💬</span>
                    Feedback
                </h2>
                <div class="input-group">
                    <label for="feedback-text">Your Feedback</label>
                    <textarea id="feedback-text" placeholder="Share your thoughts, suggestions, or report issues..." rows="4"></textarea>
                </div>
                <button class="btn" onclick="submitFeedback()" id="feedback-btn">Submit Feedback</button>
                
                <div class="result-box" id="feedback-result">
                    <div id="feedback-message"></div>
                </div>
            </div>
        </div>

        <!-- Blocker Modal -->
        <div id="blocker-modal" class="modal">
            <div class="modal-content">
                <div class="modal-header">
                    <h2>🚫 Content Blocked</h2>
                </div>
                <div class="modal-body">
                    <p><strong>Reels/Shorts are blocked—stay productive!</strong></p>
                    <p>You tried to access distracting short-form content. Stay focused on your goals!</p>
                    <div class="blocked-url" id="blocked-url"></div>
                </div>
                <div class="modal-footer">
                    <button class="btn btn-override" onclick="overrideBlock()">Override (5 min access)</button>
                    <button class="btn btn-stay" onclick="closeBlockerModal()">Stay Productive</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Screen Time Tracker Functions
        let screenTimeEntries = [];

        async function addScreenTime() {
            const appName = document.getElementById('app-name').value.trim();
            const timeSpent = document.getElementById('time-spent').value.trim();
            
            if (!appName || !timeSpent) {
                showMessage('Please fill in both app name and time spent', 'error');
                return;
            }

            try {
                const response = await fetch('/add_screen_time', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        app_name: appName,
                        time_spent: timeSpent
                    })
                });

                const data = await response.json();
                
                if (data.success) {
                    data.entry.timestamp = new Date().toLocaleString();
                    screenTimeEntries.push(data.entry);
                    updateScreenTimeList();
                    document.getElementById('app-name').value = '';
                    document.getElementById('time-spent').value = '';
                    showMessage('Screen time entry added successfully!', 'success');
                } else {
                    showMessage(data.error || 'Failed to add entry', 'error');
                }
            } catch (error) {
                showMessage('Error adding screen time entry', 'error');
            }
        }

        async function deleteScreenTime(entryId) {
            try {
                const response = await fetch(`/delete_screen_time/${entryId}`, {
                    method: 'DELETE'
                });

                const data = await response.json();
                
                if (data.success) {
                    screenTimeEntries = screenTimeEntries.filter(entry => entry.id !== entryId);
                    updateScreenTimeList();
                    showMessage('Entry deleted successfully!', 'success');
                } else {
                    showMessage('Failed to delete entry', 'error');
                }
            } catch (error) {
                showMessage('Error deleting entry', 'error');
            }
        }

        function updateScreenTimeList() {
            const listContainer = document.getElementById('screen-time-list');
            
            if (screenTimeEntries.length === 0) {
                listContainer.innerHTML = '<p style="text-align: center; opacity: 0.7; margin-top: 20px;">No entries yet. Add your first screen time entry above!</p>';
                return;
            }

            listContainer.innerHTML = screenTimeEntries.map(entry => `
                <div class="entry-item">
                    <div>
                        <strong>${entry.app_name}</strong><br>
                        <small>${entry.time_spent}</small>
                        <div class="entry-timestamp">${entry.timestamp || 'Just now'}</div>
                    </div>
                    <button class="delete-btn" onclick="deleteScreenTime(${entry.id})">Delete</button>
                </div>
            `).join('');
        }

        // Reels & Shorts Blocker Functions
        let overrideActive = false;
        let overrideTimer = null;

        function checkForBlockedContent() {
            const currentUrl = window.location.href;
            const blockedPatterns = [
                /instagram\.com\/reels\//,
                /instagram\.com\/.*\/reels\//,
                /youtube\.com\/shorts\//,
                /youtu\.be\/.*shorts/,
                /m\.youtube\.com\/shorts\//
            ];

            if (!overrideActive && blockedPatterns.some(pattern => pattern.test(currentUrl))) {
                showBlockerModal(currentUrl);
                return true;
            }
            return false;
        }

        function showBlockerModal(blockedUrl) {
            const modal = document.getElementById('blocker-modal');
            const blockedUrlDiv = document.getElementById('blocked-url');
            blockedUrlDiv.textContent = `Blocked URL: ${blockedUrl}`;
            modal.style.display = 'block';
        }

        function closeBlockerModal() {
            const modal = document.getElementById('blocker-modal');
            modal.style.display = 'none';
            window.location.href = '/';
        }

        function overrideBlock() {
            overrideActive = true;
            const modal = document.getElementById('blocker-modal');
            modal.style.display = 'none';
            
            overrideTimer = setTimeout(() => {
                overrideActive = false;
                showMessage('Override expired. Blocking is now active again.', 'info');
            }, 5 * 60 * 1000);
            
            showMessage('Override active for 5 minutes. Use this time wisely!', 'success');
        }

        function monitorUrlChanges() {
            let currentUrl = window.location.href;
            setInterval(() => {
                if (window.location.href !== currentUrl) {
                    currentUrl = window.location.href;
                    checkForBlockedContent();
                }
            }, 1000);
        }

        // Feedback Functions
        async function submitFeedback() {
            const feedbackText = document.getElementById('feedback-text').value.trim();
            const btn = document.getElementById('feedback-btn');
            const resultBox = document.getElementById('feedback-result');
            const messageDiv = document.getElementById('feedback-message');
            
            if (!feedbackText) {
                showMessage('Please enter your feedback before submitting', 'error');
                return;
            }

            btn.disabled = true;
            btn.textContent = 'Submitting...';
            
            try {
                const response = await fetch('/feedback', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        feedback: feedbackText
                    })
                });

                const data = await response.json();
                
                if (data.success) {
                    messageDiv.innerHTML = `
                        <div class="success-message">
                            <strong>Thank you for your feedback!</strong><br>
                            Your input helps us improve the app. We appreciate you taking the time to share your thoughts.
                        </div>
                    `;
                    resultBox.classList.add('show');
                    document.getElementById('feedback-text').value = '';
                } else {
                    messageDiv.innerHTML = `
                        <div class="error-message">
                            <strong>Error:</strong> ${data.error || 'Failed to submit feedback'}
                        </div>
                    `;
                    resultBox.classList.add('show');
                }
            } catch (error) {
                messageDiv.innerHTML = `
                    <div class="error-message">
                        <strong>Network Error:</strong> Unable to submit feedback. Please try again.
                    </div>
                `;
                resultBox.classList.add('show');
            } finally {
                btn.disabled = false;
                btn.textContent = 'Submit Feedback';
            }
        }

        // Utility Functions
        function showMessage(message, type) {
            const existingMessages = document.querySelectorAll('.error-message, .success-message');
            existingMessages.forEach(msg => {
                if (!msg.closest('.result-box')) {
                    msg.remove();
                }
            });

            const messageDiv = document.createElement('div');
            messageDiv.className = type === 'error' ? 'error-message' : 'success-message';
            messageDiv.textContent = message;
            
            const firstCard = d<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Growth Purpose 🪴 - Personal Development Hub</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #001F3F 0%, #7A3FF2 100%);
            color: white;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
        }

        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            background: linear-gradient(45deg, #fff, #7A3FF2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .header p {
            font-size: 1.2rem;
            opacity: 0.9;
        }

        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 30px;
            margin-bottom: 30px;
        }

        .feature-card {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .feature-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 40px rgba(122, 63, 242, 0.3);
        }

        .feature-title {
            font-size: 1.5rem;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .feature-icon {
            font-size: 1.8rem;
        }

        .input-group {
            margin-bottom: 15px;
        }

        .input-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: 500;
        }

        .input-group input, .input-group textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid rgba(255, 255, 255, 0.3);
            border-radius: 10px;
            background: rgba(255, 255, 255, 0.1);
            color: white;
            font-size: 16px;
        }

        .input-group input::placeholder, .input-group textarea::placeholder {
            color: rgba(255, 255, 255, 0.6);
        }

        .btn {
            background: linear-gradient(45deg, #7A3FF2, #001F3F);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 10px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            width: 100%;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(122, 63, 242, 0.4);
        }

        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .entries-list {
            max-height: 300px;
            overflow-y: auto;
            margin-top: 20px;
        }

        .entry-item {
            background: rgba(255, 255, 255, 0.1);
            padding: 12px;
            border-radius: 8px;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .delete-btn {
            background: #ff4757;
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 12px;
        }

        .tip-item {
            background: rgba(255, 255, 255, 0.1);
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .tip-icon {
            font-size: 2rem;
            margin-bottom: 10px;
            display: block;
        }

        .result-box {
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 10px;
            padding: 20px;
            margin-top: 20px;
            display: none;
        }

        .result-box.show {
            display: block;
        }

        .error-message {
            background: rgba(255, 71, 87, 0.2);
            border: 1px solid #ff4757;
            color: #ff4757;
            padding: 15px;
            border-radius: 10px;
            margin-top: 15px;
        }

        .success-message {
            background: rgba(46, 213, 115, 0.2);
            border: 1px solid #2ed573;
            color: #2ed573;
            padding: 15px;
            border-radius: 10px;
            margin-top: 15px;
        }

        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(5px);
        }

        .modal-content {
            background: linear-gradient(135deg, #001F3F 0%, #7A3FF2 100%);
            margin: 10% auto;
            padding: 0;
            border-radius: 20px;
            width: 90%;
            max-width: 500px;
            border: 2px solid rgba(255, 255, 255, 0.3);
            animation: modalSlide 0.3s ease-out;
        }

        @keyframes modalSlide {
            from { transform: translateY(-50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        .modal-header {
            padding: 25px 30px 0;
            text-align: center;
        }

        .modal-header h2 {
            color: white;
            margin: 0;
            font-size: 1.8rem;
        }

        .modal-body {
            padding: 20px 30px;
            color: white;
            text-align: center;
        }

        .modal-body p {
            margin: 10px 0;
            line-height: 1.6;
        }

        .blocked-url {
            background: rgba(255, 255, 255, 0.1);
            padding: 10px;
            border-radius: 8px;
            margin: 15px 0;
            font-size: 0.9rem;
            word-break: break-all;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .modal-footer {
            padding: 0 30px 30px;
            display: flex;
            gap: 15px;
            justify-content: center;
        }

        .btn-override {
            background: linear-gradient(45deg, #ff4757, #ff6b7a);
            flex: 1;
        }

        .btn-stay {
            background: linear-gradient(45deg, #2ed573, #7bed9f);
            flex: 1;
        }

        .blocker-status {
            display: grid;
            grid-template-columns: 1fr;
            gap: 15px;
        }

        .entry-timestamp {
            font-size: 0.8rem;
            opacity: 0.7;
            margin-top: 5px;
        }

        @media (max-width: 768px) {
            .features-grid {
                grid-template-columns: 1fr;
            }
            
            .header h1 {
                font-size: 2rem;
            }

            .modal-content {
                width: 95%;
                margin: 5% auto;
            }

            .modal-footer {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>The Growth Purpose 🪴</h1>
            <p>Your Personal Development Hub - Track, Learn & Grow</p>
        </div>

        <div class="features-grid">
            <!-- Screen Time Tracker -->
            <div class="feature-card">
                <h2 class="feature-title">
                    <span class="feature-icon">📱</span>
                    Screen Time Tracker
                </h2>
                <div class="input-group">
                    <label for="app-name">App Name</label>
                    <input type="text" id="app-name" placeholder="e.g., Instagram, TikTok, YouTube">
                </div>
                <div class="input-group">
                    <label for="time-spent">Time Used</label>
                    <input type="text" id="time-spent" placeholder="e.g., 2 hours, 45 minutes">
                </div>
                <button class="btn" onclick="addScreenTime()">Add Entry</button>
                
                <div class="entries-list" id="screen-time-list">
                    <!-- Screen time entries will be populated here -->
                </div>
            </div>

            <!-- Reels & Shorts Blocker -->
            <div class="feature-card">
                <h2 class="feature-title">
                    <span class="feature-icon">🚫</span>
                    Reels & Shorts Blocker
                </h2>
                <p style="margin-bottom: 20px; opacity: 0.9;">Automatically blocks Instagram Reels and YouTube Shorts</p>
                
                <div class="blocker-status">
                    <div class="tip-item">
                        <span class="tip-icon">🛡️</span>
                        <strong>Protection Active</strong>
                        <p>Blocking Instagram Reels and YouTube Shorts automatically</p>
                    </div>
                    <div class="tip-item">
                        <span class="tip-icon">⚠️</span>
                        <strong>Override Available</strong>
                        <p>Click override on warning to temporarily access blocked content</p>
                    </div>
                </div>
            </div>

            <!-- Feedback Feature -->
            <div class="feature-card">
                <h2 class="feature-title">
                    <span class="feature-icon">💬</span>
                    Feedback
                </h2>
                <div class="input-group">
                    <label for="feedback-text">Your Feedback</label>
                    <textarea id="feedback-text" placeholder="Share your thoughts, suggestions, or report issues..." rows="4"></textarea>
                </div>
                <button class="btn" onclick="submitFeedback()" id="feedback-btn">Submit Feedback</button>
                
                <div class="result-box" id="feedback-result">
                    <div id="feedback-message"></div>
                </div>
            </div>
        </div>

        <!-- Blocker Modal -->
        <div id="blocker-modal" class="modal">
            <div class="modal-content">
                <div class="modal-header">
                    <h2>🚫 Content Blocked</h2>
                </div>
                <div class="modal-body">
                    <p><strong>Reels/Shorts are blocked—stay productive!</strong></p>
                    <p>You tried to access distracting short-form content. Stay focused on your goals!</p>
                    <div class="blocked-url" id="blocked-url"></div>
                </div>
                <div class="modal-footer">
                    <button class="btn btn-override" onclick="overrideBlock()">Override (5 min access)</button>
                    <button class="btn btn-stay" onclick="closeBlockerModal()">Stay Productive</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Screen Time Tracker Functions
        let screenTimeEntries = [];

        async function addScreenTime() {
            const appName = document.getElementById('app-name').value.trim();
            const timeSpent = document.getElementById('time-spent').value.trim();
            
            if (!appName || !timeSpent) {
                showMessage('Please fill in both app name and time spent', 'error');
                return;
            }

            try {
                const response = await fetch('/add_screen_time', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        app_name: appName,
                        time_spent: timeSpent
                    })
                });

                const data = await response.json();
                
                if (data.success) {
                    data.entry.timestamp = new Date().toLocaleString();
                    screenTimeEntries.push(data.entry);
                    updateScreenTimeList();
                    document.getElementById('app-name').value = '';
                    document.getElementById('time-spent').value = '';
                    showMessage('Screen time entry added successfully!', 'success');
                } else {
                    showMessage(data.error || 'Failed to add entry', 'error');
                }
            } catch (error) {
                showMessage('Error adding screen time entry', 'error');
            }
        }

        async function deleteScreenTime(entryId) {
            try {
                const response = await fetch(`/delete_screen_time/${entryId}`, {
                    method: 'DELETE'
                });

                const data = await response.json();
                
                if (data.success) {
                    screenTimeEntries = screenTimeEntries.filter(entry => entry.id !== entryId);
                    updateScreenTimeList();
                    showMessage('Entry deleted successfully!', 'success');
                } else {
                    showMessage('Failed to delete entry', 'error');
                }
            } catch (error) {
                showMessage('Error deleting entry', 'error');
            }
        }

        function updateScreenTimeList() {
            const listContainer = document.getElementById('screen-time-list');
            
            if (screenTimeEntries.length === 0) {
                listContainer.innerHTML = '<p style="text-align: center; opacity: 0.7; margin-top: 20px;">No entries yet. Add your first screen time entry above!</p>';
                return;
            }

            listContainer.innerHTML = screenTimeEntries.map(entry => `
                <div class="entry-item">
                    <div>
                        <strong>${entry.app_name}</strong><br>
                        <small>${entry.time_spent}</small>
                        <div class="entry-timestamp">${entry.timestamp || 'Just now'}</div>
                    </div>
                    <button class="delete-btn" onclick="deleteScreenTime(${entry.id})">Delete</button>
                </div>
            `).join('');
        }

        // Reels & Shorts Blocker Functions
        let overrideActive = false;
        let overrideTimer = null;

        function checkForBlockedContent() {
            const currentUrl = window.location.href;
            const blockedPatterns = [
                /instagram\.com\/reels\//,
                /instagram\.com\/.*\/reels\//,
                /youtube\.com\/shorts\//,
                /youtu\.be\/.*shorts/,
                /m\.youtube\.com\/shorts\//
            ];

            if (!overrideActive && blockedPatterns.some(pattern => pattern.test(currentUrl))) {
                showBlockerModal(currentUrl);
                return true;
            }
            return false;
        }

        function showBlockerModal(blockedUrl) {
            const modal = document.getElementById('blocker-modal');
            const blockedUrlDiv = document.getElementById('blocked-url');
            blockedUrlDiv.textContent = `Blocked URL: ${blockedUrl}`;
            modal.style.display = 'block';
        }

        function closeBlockerModal() {
            const modal = document.getElementById('blocker-modal');
            modal.style.display = 'none';
            window.location.href = '/';
        }

        function overrideBlock() {
            overrideActive = true;
            const modal = document.getElementById('blocker-modal');
            modal.style.display = 'none';
            
            overrideTimer = setTimeout(() => {
                overrideActive = false;
                showMessage('Override expired. Blocking is now active again.', 'info');
            }, 5 * 60 * 1000);
            
            showMessage('Override active for 5 minutes. Use this time wisely!', 'success');
        }

        function monitorUrlChanges() {
            let currentUrl = window.location.href;
            setInterval(() => {
                if (window.location.href !== currentUrl) {
                    currentUrl = window.location.href;
                    checkForBlockedContent();
                }
            }, 1000);
        }

        // Feedback Functions
        async function submitFeedback() {
            const feedbackText = document.getElementById('feedback-text').value.trim();
            const btn = document.getElementById('feedback-btn');
            const resultBox = document.getElementById('feedback-result');
            const messageDiv = document.getElementById('feedback-message');
            
            if (!feedbackText) {
                showMessage('Please enter your feedback before submitting', 'error');
                return;
            }

            btn.disabled = true;
            btn.textContent = 'Submitting...';
            
            try {
                const response = await fetch('/feedback', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        feedback: feedbackText
                    })
                });

                const data = await response.json();
                
                if (data.success) {
                    messageDiv.innerHTML = `
                        <div class="success-message">
                            <strong>Thank you for your feedback!</strong><br>
                            Your input helps us improve the app. We appreciate you taking the time to share your thoughts.
                        </div>
                    `;
                    resultBox.classList.add('show');
                    document.getElementById('feedback-text').value = '';
                } else {
                    messageDiv.innerHTML = `
                        <div class="error-message">
                            <strong>Error:</strong> ${data.error || 'Failed to submit feedback'}
                        </div>
                    `;
                    resultBox.classList.add('show');
                }
            } catch (error) {
                messageDiv.innerHTML = `
                    <div class="error-message">
                        <strong>Network Error:</strong> Unable to submit feedback. Please try again.
                    </div>
                `;
                resultBox.classList.add('show');
            } finally {
                btn.disabled = false;
                btn.textContent = 'Submit Feedback';
            }
        }

        // Utility Functions
        function showMessage(message, type) {
            const existingMessages = document.querySelectorAll('.error-message, .success-message');
            existingMessages.forEach(msg => {
                if (!msg.closest('.result-box')) {
                    msg.remove();
                }
            });

            const messageDiv = document.createElement('div');
            messageDiv.className = type === 'error' ? 'error-message' : 'success-message';
            messageDiv.textContent = message;
            
            const firstCard = d
