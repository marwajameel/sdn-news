
index.html
<!DOCTYPE html>
<html lang="ur" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SDN News - بلاک چین پوسٹنگ</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #f4f7f6; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; }
        .card { background: white; padding: 30px; border-radius: 15px; box-shadow: 0 10px 25px rgba(0,0,0,0.1); text-align: center; max-width: 400px; width: 100%; }
        h2 { color: #333; margin-bottom: 20px; }
        .news-input { width: 100%; padding: 10px; margin-bottom: 20px; border: 1px solid #ddd; border-radius: 5px; box-sizing: border-box; }
        #postNewsBtn { background-color: #512da8; color: white; border: none; padding: 12px 25px; font-size: 16px; border-radius: 8px; cursor: pointer; transition: 0.3s; width: 100%; }
        #postNewsBtn:hover { background-color: #311b92; }
        #postNewsBtn:disabled { background-color: #ccc; cursor: not-allowed; }
        .status { margin-top: 15px; font-size: 14px; color: #666; }
    </style>
</head>
<body>

<div class="card">
    <h2>SDN News پورٹل</h2>
    <p>اپنی خبر بلاک چین پر محفوظ کریں</p>
    
    <textarea id="newsContent" class="news-input" rows="4" placeholder="خبر یہاں لکھیں..."></textarea>
    
    <button id="postNewsBtn" onclick="postNewsToBlockchain()">خبر اپ لوڈ کریں</button>
    
    <div id="statusMessage" class="status"></div>
</div>

<script>
    async function postNewsToBlockchain() {
        const btn = document.getElementById('postNewsBtn');
        const status = document.getElementById('statusMessage');
        const content = document.getElementById('newsContent').value;

        if (!content) {
            alert("براہ کرم پہلے خبر لکھیں!");
            return;
        }

        // بٹن کو پروسیسنگ حالت میں لائیں
        btn.disabled = true;
        btn.innerText = "والٹ سے کنیکٹ ہو رہا ہے...";
        status.innerText = "براہ کرم اپنے فینٹم والٹ میں ٹرانزیکشن کنفرم کریں چمیک کریں۔";

        const provider = window.solana;

        if (provider && provider.isPhantom) {
            try {
                // والٹ کنیکٹ کریں
                await provider.connect();
                
                // ٹرانزیکشن کا فرضی وقت (Simulating Transaction)
                // یہاں آپ اپنی اصل Solana Web3 ٹرانزیکشن لاجک ڈالیں گے
                setTimeout(() => {
                    status.innerHTML = "<span style='color: green;'>✔ خبر کامیابی سے بلاک چین پر محفوظ ہو گئی!</span>";
                    btn.innerText = "خبر اپ لوڈ کریں";
                    btn.disabled = false;
                    document.getElementById('newsContent').value = ""; // ٹیکسٹ ایریا خالی کریں
                }, 3000);

            } catch (err) {
                status.innerHTML = "<span style='color: red;'>✘ ٹرانزیکشن منسوخ کر دی گئی۔</span>";
                btn.disabled = false;
                btn.innerText = "خبر اپ لوڈ کریں";
            }
        } else {
            status.innerHTML = "<span style='color: orange;'>فینٹم والٹ نہیں ملا۔</span>";
            window.open("https://phantom.app/", "_blank");
            btn.disabled = false;
            btn.innerText = "خبر اپ لوڈ کریں";
        }
    }
</script>

</body>
</html