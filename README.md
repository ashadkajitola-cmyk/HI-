<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cricket Schedule Subscription System</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f7f6;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 500px;
            margin: 20px auto;
            background: #ffffff;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }
        .admin-box {
            background: #e8f5e9;
            border: 2px dashed #2e7d32;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            text-align: center;
        }
        .payment-box {
            text-align: center;
        }
        .price {
            font-size: 24px;
            color: #28a745;
            font-weight: bold;
            margin: 15px 0;
        }
        .qr-box img {
            width: 180px;
            height: 180px;
            border: 2px solid #ddd;
            padding: 5px;
            border-radius: 8px;
        }
        .btn {
            display: block;
            width: 100%;
            background-color: #512da8;
            color: white;
            padding: 12px;
            border: none;
            border-radius: 6px;
            font-weight: bold;
            font-size: 16px;
            cursor: pointer;
            text-decoration: none;
            text-align: center;
            margin-top: 15px;
        }
        .btn:hover { background-color: #381e72; }
        .input-field {
            width: 100%;
            padding: 10px;
            margin: 8px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
            box-sizing: border-box;
        }
    </style>
</head>
<body>

    <div class="container">
        <!-- Simulating User Login Check (Real website me yeh Backend se aayega) -->
        <div id="app-content">
            <!-- Yahan dynamic content load hoga script ke zariye -->
        </div>
    </div>

    <script>
        // Maan lijiye current logged-in user ka mobile number yeh hai (Real app me yeh session/database se aayega)
        // Aap yahan apna number daal kar test kar sakte hain: "7355055313" ya koi aur number
        let loggedInUserMobile = "7355055313"; // Apna number yahan check karne ke liye rakha hai

        const appContent = document.getElementById('app-content');

        if (loggedInUserMobile === "7355055313") {
            // ================= ADMIN / FREE ACCESS VIEW =================
            appContent.innerHTML = `
                <div class="admin-box">
                    <h3 style="color: #2e7d32; margin-top: 0;">👑 Welcome Admin!</h3>
                    <p>Aapka number (<strong>7355055313</strong>) registered hai. Aapko <strong>Free Access</strong> mil gaya hai!</p>
                </div>

                <h2>Cricket Schedule Generator</h2>
                <a href="create-schedule.html" class="btn" style="background-color: #2e7d32;">Bina Roka-Toka Schedule Banayein (Go)</a>

                <hr style="margin: 25px 0; border: 0; border-top: 1px solid #ddd;">

                <h3>➕ Naya Subscription Manually Add Karein</h3>
                <p style="font-size: 13px; color: #555;">Agar kisi user ne payment kiya hai aur aap uska plan manually activate karna chahte hain:</p>
                
                <label>User ka Mobile Number:</label>
                <input type="text" id="targetUser" class="input-field" placeholder="User ka mobile number daalein">
                
                <label>Plan Kitne Din ka dena hai?</label>
                <select id="planDays" class="input-field">
                    <option value="30">1 Mahina (30 Days)</option>
                    <option value="365">1 Saal (365 Days)</option>
                </select>

                <button class="btn" onclick="addNewSubscription()">Subscription Activate Karein</button>
            `;
        } else {
            // ================= NORMAL USER VIEW (Payment Required) =================
            appContent.innerHTML = `
                <div class="payment-box">
                    <h2>Cricket Schedule Plan</h2>
                    <p style="color: #666; font-size: 14px;">Unlimited Schedule banane ke liye subscription lein.</p>
                    
                    <div class="price">₹499 / Month</div>
                    
                    <div class="qr-box">
                        <img src="your-qr-code.png" alt="QR Code">
                    </div>
                    <p style="font-size: 13px; color: #555;">UPI ID: <strong>7355055313@ibl</strong></p>

                    <a href="upi://pay?pa=7355055313@ibl&pn=CricketSchedule&am=499.00&cu=INR&tn=Subscription" class="btn">
                        Pay ₹499 via PhonePe / Paytm
                    </a>

                    <div style="margin-top: 20px; text-align: left; border-top: 1px solid #eee; padding-top: 15px;">
                        <label style="font-size: 14px; font-weight: bold;">Payment ke baad UTR / Transaction ID dalein:</label>
                        <input type="text" id="utr" class="input-field" placeholder="12-digit UTR number">
                        <button class="btn" style="background-color: #28a745;" onclick="submitUTR()">Verify & Submit</button>
                    </div>
                </div>
            `;
        }

        function addNewSubscription() {
            let userNum = document.getElementById('targetUser').value;
            let days = document.getElementById('planDays').value;
            if(userNum.trim() === "") {
                alert("Kripya user ka mobile number daalein!");
                return;
            }
            alert("Success! User (" + userNum + ") ka subscription " + days + " dino ke liye activate kar diya gaya hai.");
            document.getElementById('targetUser').value = "";
        }

        function submitUTR() {
            let utr = document.getElementById('utr').value;
            if(utr.trim() === "") {
                alert("Kripya UTR number daalein!");
                return;
            }
            alert("Aapka UTR (" + utr + ") submit ho gaya hai. Admin verification ke baad plan chalu ho jayega.");
            document.getElementById('utr').value = "";
        }
    </script>

</body>
</html>
