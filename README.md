<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MEEN HUB - Unique HWID Key System</title>
    <style>
        body { background-color: #0e0e12; color: #ffffff; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; }
        .card { background: #16161e; padding: 30px; border-radius: 12px; border: 1px solid #ffd700; text-align: center; width: 340px; box-shadow: 0 8px 24px rgba(0,0,0,0.5); }
        h2 { color: #ffd700; margin-bottom: 10px; }
        p { color: #a0a0b0; font-size: 13px; margin-bottom: 20px; }
        .btn { display: inline-block; width: 100%; padding: 12px; background: #00e5ff; color: #0e0e12; font-weight: bold; text-decoration: none; border-radius: 6px; box-sizing: border-box; margin-bottom: 10px; border: none; cursor: pointer; font-size: 14px; }
        .btn:hover { background: #00b3cc; }
        .key-box { background: #0a0a0e; padding: 10px; border-radius: 6px; border: 1px dashed #ffd700; color: #ffd700; font-family: monospace; word-break: break-all; margin-top: 15px; font-size: 13px; font-weight: bold; }
        .error { color: #ff5555; font-size: 12px; margin-top: 10px; }
    </style>
</head>
<body>
    <div class="card">
        <h2>✨ MEEN HUB ✨</h2>
        <p>ระบบคีย์เฉพาะตัว ป้องกันการแชร์คีย์</p>
        
        <button class="btn" id="genBtn" onclick="generateHWIDKey()">🔗 สร้างคีย์สำหรับเครื่องคุณ</button>
        
        <div class="key-box" id="keyDisplay">รอกดสร้างคีย์...</div>
        <div class="error" id="errorMsg"></div>
    </div>

    <script>
        // ดึง HWID ที่ส่งมาจากสคริปต์ Roblox ผ่าน URL (เช่น website.com/?hwid=xxxx)
        const urlParams = new URLSearchParams(window.location.search);
        const userHWID = urlParams.get('hwid');

        if (!userHWID) {
            document.getElementById('errorMsg').innerText = "⚠️ กรุณารันผ่านสคริปต์ในเกม เพื่อรับคีย์เฉพาะของคุณ!";
            document.getElementById('genBtn').style.display = "none";
            document.getElementById('keyDisplay').style.display = "none";
        }

        function generateHWIDKey() {
            if (!userHWID) return;
            
            // นำ HWID มาแปลงเป็นคีย์เฉพาะตัวที่ไม่ซ้ำใคร
            let hash = 0;
            const combinedString = userHWID + "-MEEN-VIP-SECRET";
            for (let i = 0; i < combinedString.length; i++) {
                hash = ((hash << 5) - hash) + combinedString.charCodeAt(i);
                hash |= 0;
            }
            const uniqueKey = "MEEN-" + Math.abs(hash).toString(36).toUpperCase();
            
            document.getElementById('keyDisplay').innerText = "คีย์ของคุณ: " + uniqueKey;
            document.getElementById('genBtn').style.display = "none";
        }
    </script>
</body>
</html>
