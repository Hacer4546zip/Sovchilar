<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Autoresponder Kirish</title>
    <style>
        /* Ranglar uchun o'zgaruvchilar */
        :root {
            --fuschia: #ff0081;
            --button-bg: var(--fuschia);
            --button-text-color: #fff;
            --baby-blue: #f8faff;
            --chat-height: 300px; /* Chat maydonining balandligi */
        }

        body {
            font-size: 16px;
            font-family: 'Helvetica', 'Arial', sans-serif;
            text-align: center;
            background-color: var(--baby-blue);
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .container {
            width: 400px;
            padding: 20px;
            background: rgba(255, 255, 255, 0.15);
            border-radius: 15px;
            box-shadow: 0 15px 45px rgba(0, 0, 0, 0.5);
            margin-bottom: 20px;
        }

        h2 {
            font-size: 2em;
            color: #000; /* Matn rangini qora rangga o'zgartirdik */
            margin-bottom: 20px;
        }

        .label {
            font-size: 1em;
            color: #000; /* Matn rangini qora rangga o'zgartirdik */
            display: block;
            margin-bottom: 10px;
        }

        input[type="text"] {
            width: 100%;
            padding: 15px;
            margin-bottom: 10px;
            border: none;
            border-radius: 10px;
            background-color: #fff;
            box-shadow: inset 0 2px 10px rgba(0, 0, 0, 0.2);
            font-size: 1em;
            color: #000; /* Kiritish maydonidagi matn rangini qora rangga o'zgartirdik */
        }

        .bubbly-button {
            font-family: 'Helvetica', 'Arial', sans-serif;
            display: inline-block;
            font-size: 1em;
            padding: 1em 2em;
            margin-top: 20px;
            -webkit-appearance: none;
            appearance: none;
            background-color: var(--button-bg);
            color: var(--button-text-color);
            border-radius: 4px;
            border: none;
            cursor: pointer;
            position: relative;
            transition: transform ease-in 0.1s, box-shadow ease-in 0.25s;
            box-shadow: 0 2px 25px rgba(255, 0, 130, 0.5);
        }

        .bubbly-button:focus {
            outline: 0;
        }

        .bubbly-button:before, .bubbly-button:after {
            position: absolute;
            content: '';
            display: block;
            width: 140%;
            height: 100%;
            left: -20%;
            z-index: -1000;
            transition: all ease-in-out 0.5s;
            background-repeat: no-repeat;
        }

        .bubbly-button:before {
            display: none;
            top: -75%;
            background-image:  
                radial-gradient(circle, var(--button-bg) 20%, transparent 20%),
                radial-gradient(circle, transparent 20%, var(--button-bg) 20%, transparent 30%),
                radial-gradient(circle, var(--button-bg) 20%, transparent 20%), 
                radial-gradient(circle, var(--button-bg) 20%, transparent 20%),
                radial-gradient(circle, transparent 10%, var(--button-bg) 15%, transparent 20%),
                radial-gradient(circle, var(--button-bg) 20%, transparent 20%),
                radial-gradient(circle, var(--button-bg) 20%, transparent 20%);
            background-size: 10% 10%, 20% 20%, 15% 15%, 20% 20%, 18% 18%, 10% 10%, 15% 15%;
        }

        .bubbly-button:after {
            display: none;
            bottom: -75%;
            background-image:  
                radial-gradient(circle, var(--button-bg) 20%, transparent 20%), 
                radial-gradient(circle, var(--button-bg) 20%, transparent 20%),
                radial-gradient(circle, transparent 10%, var(--button-bg) 15%, transparent 20%),
                radial-gradient(circle, var(--button-bg) 20%, transparent 20%),
                radial-gradient(circle, var(--button-bg) 20%, transparent 20%),
                radial-gradient(circle, var(--button-bg) 20%, transparent 20%);
            background-size: 15% 15%, 20% 20%, 18% 18%, 20% 20%, 15% 15%, 10% 10%;
        }

        .bubbly-button:active {
            transform: scale(0.9);
            background-color: #d4006a;
            box-shadow: 0 2px 25px rgba(255, 0, 130, 0.2);
        }

        .bubbly-button.animate:before {
            display: block;
            animation: topBubbles ease-in-out 0.75s forwards;
        }

        .bubbly-button.animate:after {
            display: block;
            animation: bottomBubbles ease-in-out 0.75s forwards;
        }

        .chat-area {
            max-height: var(--chat-height); /* Chat maydonini belgilash */
            overflow-y: auto; /* Vertikal skroll bo'yicha */
            background: rgba(255, 255, 255, 0.9); /* Oq fon boshqaruv */
            border: 1px solid #ccc; /* Chekka */
            border-radius: 10px; /* Burchaklarni yumshatish */
            padding: 10px; /* Ichki bo'shliq */
            margin-bottom: 20px; /* Tugmalar orasidagi bo'shliq */
        }

        .info-message {
            font-size: 1em;
            color: #000; /* Qora rangda */
            margin-bottom: 15px; /* Pastga bo'shliq */
        }

        .bot-message, .customer-message {
            margin: 5px 0; /* Bo'shliq */
        }

        .bot-name {
            color: #ff0000; /* Qizil rang bot ismi uchun */
        }

        .customer-message {
            color: #4caf50; /* Zamonaviy rang mijoz xabari uchun */
            text-align: right; /* O'ngga qaratish */
        }

        .hidden {
            display: none;
        }
        
        .success-message {
            color: green;
            display: none; /* Dastlab yashirin */
        }
    </style>
</head>
<body>
    <div class="container" id="login-section">
        <h2>👇 Salom To'g'ri 🔐 Parol Kodi 123 Tering...🟢</h2>
        <div class="input-group">
            <span class="label">Parolni kiriting:</span>
            <input type="text" id="password" placeholder="123" maxlength="3">
        </div>
        <button class="bubbly-button" id="login-button">Kirish</button>
    </div>

    <div class="container hidden" id="main-section">
        <!-- Online foydalanuvchilar haqida tasodifiy ma'lumot -->
        <div class="info-message" id="online-users-info">
            🟢 Onlayn Erkaklar <span id="online-men">0</span> ta, 🟢 Onlayn Ayollar <span id="online-women">0</span> ta.
        </div>
        
        <div class="chat-area" id="chat-area"></div> <!-- Chat zonasini o'zgartirdik -->
        <div class="input-group">
            <span class="label">🟢 Online Chat 🟢:</span>
            <input type="text" id="customer-message" placeholder="Xabar yozing chatga....">
        </div>
        <button class="bubbly-button" id="send-button">Xabarni Chatga Joylash ✋️</button>

        <div class="input-group" style="margin-top: 20px;">
            <span class="label">👰‍♂️Келин Номзодга ёзиш учун 🔐 Кодни ёзинг Код Йокми Сотиб Олинг уни 💰 :</span>
            <input type="text" id="additional-password" placeholder="Сотиб Олингар Паролни Теринг ....♥️" maxlength="3">
            <button class="bubbly-button" id="check-password-button">Terilgan Kodni Tasdiqlash</button>
            <!-- Yana bir tugma qo'shamiz -->
            <a href="https://t.me/Vovo_Admen" target="_blank">
                <button class="bubbly-button">Kod Sotib Olish 🔐</button>
             <!-- 🎱 Yana bir tugma qo'shildi 💞 -->
            <a href="https://t.me/Vovo_Admen" target="_blank">
                <button class="bubbly-button">✋️Элон Бериш 📢</button>
            </a>
        </div>
        <div id="link-area" class="hidden"></div>
        <div id="success-message" class="success-message">🟢 Tog'ri Parol 🟢</div>
    </div>

    <script>
        const correctPassword = "123"; // Kirish paroli
        const additionalPassword = "769"; // Qo'shimcha parol
        const bots = [
            "Dilorom", "Yulduz", "Asal", "Oqil", "Dilshod", "Shohruh", 
            "Nargiza", "Aziz", "Nilufar", "Jasur" // O'zbek ismlari
        ];

        const responses = [
            "Kicha Mazza Qildim 2 soat gaplashdim telfonda 🥰",
            "Vay iflos xaromi ekan lichkamga mani sukib chorniga solib uzi qochib kitibdi",
            "Manga Poxxuy ☺️",
            "Usha erkakni topsam tashog'ini putidan ayiraman 😏",
            "Kicha Paynet qilgandim mg tugab qoldi 😪",
            "Tanishamizmi jon",
            "Raxmat shart mas umuman kiragi yoq",
            "telfon raqamizni bering manga",
            "tel raqamimni bersam telfon qilib bezor qilasilar shu uchun bermayman",
            "Nima hohlaysiz mandan uzi siz",
            "Kicha Mazza Qildim 2 soat gaplashdim telfonda 🥰",
            "Vay iflos xaromi ekan lichkamga mani sukib chorniga solib uzi qochib kitibdi",
            "Manga Poxxuy ☺️",
            "Usha erkakni topsam tashog'ini putidan ayiraman 😏",
            "Kicha Paynet qilgandim mg tugab qoldi 😪",
            "Tanishamizmi jon",
            "Raxmat shart mas umuman kiragi yoq",
            "telfon raqamizni bering manga",
            "tel raqamimni bersam telfon qilib bezor qilasilar shu uchun bermayman",
            "Nima hohlaysiz mandan uzi siz",
            "Kicha Mazza Qildim 2 soat gaplashdim telfonda 🥰",
            "Vay iflos xaromi ekan lichkamga mani sukib chorniga solib uzi qochib kitibdi",
            "Manga Poxxuy ☺️",
            "Usha erkakni topsam tashog'ini putidan ayiraman 😏",
            "Kicha Paynet qilgandim mg tugab qoldi 😪",
            "Tanishamizmi jon",
            "Raxmat shart mas umuman kiragi yoq",
            "telfon raqamizni bering manga",
            "tel raqamimni bersam telfon qilib bezor qilasilar shu uchun bermayman",
            "Nima hohlaysiz mandan uzi siz"
        ];

        const links = [
            "https://example.com/link1",
            "https://example.com/link2",
            "https://example.com/link3",
            "https://example.com/link4",
            "https://example.com/link5",
            "https://example.com/link6",
            "https://example.com/link7",
            "https://example.com/link8",
            "https://example.com/link9",
            "https://example.com/link10",
            "https://example.cofoydala1",
            "https://example.com/link12",
            "https://example.com/link13",
            "https://examplMath.floor14",
            "https://example.com/link15",
            "https://example.com/link16",
            "https://example.com/link17",
            "https://example.com/link18",
            "https://exampleonline-me19",
            "https://example.com/link20",
            "https://example.com/link21",
            "https://example.com/line22",
            "https://example.com/link23",
            "https://example.com/link24"
        ];

        // Tasodifiy onlayn foydalanuvchilar sonini generatsiya qilish
        function generateOnlineUsers() {
            const onlineMen = Math.floor(Math.random() * (9000 - 1 + 1)) + 1; // 1 dan 9000 gacha
            const onlineWomen = Math.floor(Math.random() * (9000 - 1 + 1)) + 1; // 1 dan 9000 gacha
            document.getElementById("online-men").textContent = onlineMen;
            document.getElementById("online-women").textContent = onlineWomen;
        }

        let customerId;

        document.getElementById("login-button").addEventListener("click", function(e) {
            animateButton(e); // Tugmadagi animatsiyani ishga tushiramiz
            const password = document.getElementById("password").value;
            if (password.length === 3 && /^[0-9]+$/.test(password)) { // Raqamlar tekshiruvi
                if (password === correctPassword) {
                    // Kirish muvaffaqiyatli bo'lsa
                    document.getElementById("login-section").classList.add("hidden");
                    const mainSection = document.getElementById("main-section");
                    mainSection.classList.remove("hidden");

                    const chatArea = document.getElementById("chat-area");
                    chatArea.innerHTML += "<div class='bot-message'>Salom! Sizning xizmatimizdan foydalanayotganingiz uchun rahmat!</div>";

                    // Onlayn foydalanuvchilar sonini generatsiya qilamiz
                    generateOnlineUsers();

                    // Mijozga ID taqdim etish
                    customerId = Math.floor(Math.random() * (99999 - 1000 + 1)) + 1000; // 1000 dan 9999 gacha ID

                    // Tasodifiy botlardan xabarlar yuborish
                    let botInterval = setInterval(() => {
                        const randomBotName = bots[Math.floor(Math.random() * bots.length)];
                        const randomResponse = responses[Math.floor(Math.random() * responses.length)];
                        chatArea.innerHTML += `<div class='bot-message'><span class='bot-name'>${randomBotName}</span>: ${randomResponse}</div>`;
                        chatArea.scrollTop = chatArea.scrollHeight; // Qaytish uchun qidiruv
                    }, 3000); // Har 3 soniyada 

                    document.getElementById("send-button").addEventListener("click", function(e) {
                        animateButton(e); // Tugmadagi animatsiyani ishga tushiramiz
                        const customerMessage = document.getElementById("customer-message").value;
                        if (customerMessage) {
                            chatArea.innerHTML += `<div class='customer-message'>ID ${customerId}: ${customerMessage}</div>`;
                            chatArea.scrollTop = chatArea.scrollHeight; // Qaytish uchun qidiruv
                            document.getElementById("customer-message").value = ''; // Xabarni tozalash
                        } else {
                            alert("Iltimos, xabarni kiriting.");
                        }
                    });

                    // Qo'shimcha parolni tekshirish
                    document.getElementById("check-password-button").addEventListener("click", function(e) {
                        animateButton(e); // Tugmadagi animatsiyani ishga tushiramiz
                        const enteredAdditionalPassword = document.getElementById("additional-password").value.trim();

                        // Qo'shimcha parolni tekshirish shartlari
                        if (enteredAdditionalPassword.length === 3 && /^[0-9]+$/.test(enteredAdditionalPassword)) {
                            if (enteredAdditionalPassword === additionalPassword) {
                                alert("🥰Qo'shimcha parol to'g'ri kiritildi..🟢");

                                // Tasodifiy havola yaratish
                                const randomIndex = Math.floor(Math.random() * links.length);
                                const randomLink = links[randomIndex];

                                const linkArea = document.getElementById("link-area");
                                linkArea.innerHTML = "<h3>Tasodifiy havola:</h3>";
                                linkArea.innerHTML += `<a href="${randomLink}" class="link" target="_blank">${randomLink}</a>`;
                                linkArea.classList.remove("hidden");

                                // Muvaffaqiyat xabarini ko'rsatish
                                const successMessage = document.getElementById("success-message");
                                successMessage.classList.remove("hidden");
                                successMessage.innerText = "🟢 Tog'ri Parol 🟢";
                            } else {
                                alert("🚫Noto'g'ri qo'shimcha parol, iltimos qayta urinib ko'ring.");
                            }
                        } else {
                            alert("🔐 Iltimos, faqat 3 raqamli parolni kiriting.");
                        }
                    });
                } else {
                    alert("🔐 Noto'g'ri parol, iltimos qayta urinib ko'ring.");
                }
            } else {
                alert("Iltimos, faqat 3 raqamli parolni kiriting.");
            }
        });

        // Tugma animatsiya funksiyasi
        var animateButton = function(e) {
            e.preventDefault(); // Default harakatlarni to'xtatish
            // Animatsiyani tiklash
            e.target.classList.remove('animate');
            e.target.classList.add('animate');
            setTimeout(function() {
                e.target.classList.remove('animate');
            }, 700);
        };
    </script>
</body>
</html>
