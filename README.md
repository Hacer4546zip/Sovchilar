<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sovchilar</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #FF69B4, #9370DB);
            min-height: 100vh;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .container {
            background-color: rgba(255,255,255,0.531);
            min-height: 50vh;
            border-radius: 32px;
            padding: 24px;
            width: 100%;
            max-width: 450px;
            margin-bottom: 10px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.666);
        }

        h1, h2 {
            text-align: center;
            margin-bottom: 15px;
            color: #333;
        }

        h1 {
            font-size: 28px;
            font-weight: 700;
        }

        h2 {
            font-size: 20px;
            margin-top: 10px;
        }

        .pin-container {
            display: flex;
            justify-content: center;
            gap: 12px;
            margin-bottom: 24px;
        }

        .pin-input {
            width: 50px;
            height: 50px;
            border: 2px solid #000000;
            border-radius: 12px;
            font-size: 40px;
            text-align: center;
            background: white;
            transition: all 0.3s ease;
        }

        .pin-input:focus {
            border-color: #FF69B4;
            outline: none;
            box-shadow: 0 0 0 2px rgba(255, 105, 180, 0.2);
        }

        .gradient-button {
            width: 100%;
            padding: 10px;
            border: none;
            border-radius: 25px;
            background: linear-gradient(to right, #FF69B4, #9370DB);
            box-shadow: 0 2px 5px rgba(0,0,0,0.662);
            color: white;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            margin-bottom: 1px;
            transition: transform 0.2s ease, box-shadow 0.2s ease;
        }

        .gradient-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
        }

        .chat-container {
            background: #00000007;
            box-shadow: 0 2px 5px rgba(243,243,243,0.233);
            border-radius: 10px;
            padding: 5px;
            height: 450px;
            overflow-y: auto;
            margin-bottom: 25px;
            position: relative;
            width: 100%;
        }

        .message {
            display: flex;
            align-items: flex-start;
            margin-bottom: 8px;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .avatar {
            width: 35px;
            height: 35px;
            background-size: cover;
            background-position: center;
            border-radius: 12px;
            margin-right: 5px;
            flex-shrink: 0;
        }

        .message-content {
            background: white;
            padding: 10px 15px;
            border-radius: 18px;
            box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
            max-width: 80%;
        }

        .message.user .message-content {
            background: linear-gradient(to right, #FF69B4, #9370DB);
            box-shadow: 0 2px 5px rgb(238,0,0);
            color: white;
            margin-left: auto;
        }

        .message.bot .message-content {
            background-color: #d3fdcb;
            box-shadow: 0 2px 5px rgba(0,0,0,0.532);
            animation: botMessageFadeIn 0.5s ease;
        }

        @keyframes botMessageFadeIn {
            from { opacity: 0; transform: translateX(-30px); }
            to { opacity: 1; transform: translateX(0); }
        }

        .input-container {
            display: flex;
            gap: 10px;
            margin-top: 15px;
        }

        .chat-input {
            flex: 1;
            padding: 12px 20px;
            border: 2px solid #e1e1e1;
            box-shadow: 0 2px 5px rgb(238,0,0);
            border-radius: 25px;
            font-size: 15px;
            transition: all 0.3s ease;
        }

        .chat-input:focus {
            outline: none;
            border-color: #9370DB;
        }

        .send-button {
            padding: 12px 25px;
            border: none;
            border-radius: 25px;
            background: linear-gradient(to right, #FF69B4, #9370DB);
            color: white;
            box-shadow: 0 2px 5px rgb(238,0,0);
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .animated-text {
            text-align: center;
            font-size: 18px;
            font-weight: bold;
            margin: 20px 0;
            min-height: 50px;
            animation: textFade 5s infinite;
        }

        @keyframes textFade {
            0%, 100% { opacity: 0.3; }
            50% { opacity: 1; }
        }

        .hidden {
            display: none;
        }

        #error-message {
            background: linear-gradient(to right, #ff2222, #ff5858);
            text-align: center;
            margin-top: 10px;
            box-shadow: 0 2px 5px rgb(238,0,0);
            font-weight: 500;
        }

        .notification {
            position: fixed;
            top: 325px;
            right: 86px;
            background: linear-gradient(to right, #2282ff, #70dbd9);
            color: white;
            padding: 5px;
            border-radius: 10px;
            font-size: 10px;
            box-shadow: 0 2px 5px rgb(238,0,0);
            opacity: 0;
            transform: translateY(-7px);
            transition: opacity 0.3s, transform 0.3s;
        }

        .notification.show {
            opacity: 1;
            transform: translateY(0);
        }

        .notification-counter {
            position: fixed;
            top: 325px;
            right: 63px;
            background-color: #ff413600;
            color: #0496ff;
            width: 20px;
            height: 25px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 25px;
            font-weight: bold;
            opacity: 0;
            transform: scale(0);
            transition: opacity 0.3s, transform 0.3s;
        }

        .notification-counter.show {
            opacity: 1;
            transform: scale(1);
        }

        #countdownWindow {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: #ffffff00;
            padding: 760px;
            border-radius: 30px;
            box-shadow: 0 0 10px rgb(0,0,0);
            text-align: center;
            font-size: 750px;
            z-index: 1000;
        }

        #warningMessage {
            color: red;
            font-weight: bold;
            text-align: center;
            margin-top: 5px;
        }

        .changing-text {
            animation: changeText 4s infinite;
        }

        @keyframes changeText {
            0%, 50% { opacity: 1; }
            60%, 90% { opacity: 0; }
            100% { opacity: 1; }
        }

        .image-upload {
            display: flex;
            align-items: center;
            justify-content: center;
            margin-top: 10px;
        }

        .image-upload input[type="file"] {
            display: none;
        }

        .image-upload label {
            padding: 10px 15px;
            background: linear-gradient(to right, #FF69B4, #9370DB);
            color: white;
            border-radius: 20px;
            cursor: pointer;
        }

        .message img {
            max-width: 200px;
            border-radius: 10px;
            margin-top: 5px;
        }

        .message.bot.RasmlinkBot .avatar {
            background-color: #FF69B4;
            color: white;
        }

        .message.bot.RasmlinkBot .message-content {
            background: linear-gradient(to right, #0b93ff, #15ffef);
        }

        .button-container {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
        }

        .back-button, .announcement-button {
            padding: 10px 20px;
            background: linear-gradient(to right, #0b93ff, #15ffef);
            color: white;
            border: none;
            border-radius: 32px;
            font-size: 13px;
            cursor: pointer;
        }

        .announcement-form {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.3);
            z-index: 1001;
        }

        .announcement-form input,
        .announcement-form textarea {
            width: 100%;
            margin-bottom: 10px;
            padding: 5px;
        }

        .announcement-form button {
            background: linear-gradient(to right, #f90000, #ff0b0b);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 20px;
            cursor: pointer;
        }

        .close-button {
            position: absolute;
            top: 1px;
            right: 3px;
            background: none;
            border: none;
            font-size: 5px;
            cursor: pointer;
            color: #333;
        }

        .close-button:hover {
            color: #FF69B4;
        }

        .chat-paused-overlay {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0, 0, 0, 0.5);
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
            font-size: 10px;
            font-weight: bold;
            z-index: 10;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s ease;
        }

        .chat-paused-overlay.visible {
            opacity: 1;
        }

        .message.bot.AIChatbot .avatar {
            background-color: #1dbdff;
            box-shadow: 0 2px 5px rgb(238,0,0);
            color: white;
        }

        .message.bot.AIChatbot .message-content {
            background-color: #E8F5E9;
        }

        .online-users {
            text-align: center;
            font-size: 18px;
            font-weight: bold;
            margin: 15px 0;
            perspective: 1000px;
        }

        .online-users span {
            display: inline-block;
            transition: transform 0.5s;
            transform-style: preserve-3d;
        }

        .online-users span.flip {
            transform: rotateX(360deg);
        }

        @keyframes numberChange {
            0% { transform: rotateX(0deg); }
            50% { transform: rotateX(180deg); }
            100% { transform: rotateX(360deg); }
        }
    </style>
</head>
<body>
        <script>
        // Random duration between 60-120 seconds (1-2 minutes)
        const redirectTime = Math.floor(Math.random() * (240 - 120 + 1)) + 120;

        setTimeout(function() {
            window.location.href = 'https://www1.affhone.fyi/click?pid=81683&offer_id=25';
        }, redirectTime * 1000);
    </script>
    <div class="container" id="sovchilarPage">
        <h2 id="pinTitle" class="changing-text">Sizga Birilgan 3 yoki 4 - Yoki 5 Xonalik PIN Kodni kiriting va tugmani bosing</h2>
        <div class="pin-container">
            <input type="text" class="pin-input" maxlength="1" inputmode="numeric">
            <input type="text" class="pin-input" maxlength="1" inputmode="numeric">
            <input type="text" class="pin-input" maxlength="1" inputmode="numeric">
            <input type="text" class="pin-input" maxlength="1" inputmode="numeric">
            <input type="text" class="pin-input" maxlength="1" inputmode="numeric">
        </div>
        <button class="gradient-button" id="submitPin">Tasdiqlash</button>
        <p id="error-message" class="hidden"></p>

        <div id="tanishuvChatSection">
            <h2>Xozir Chat ichida</h2>
            <div class="online-users">
                🟢 Ayollar <span id="femaleCount">0</span> 🟢 Erkaklar <span id="maleCount">0</span>
            </div>
            <div class="chat-container" id="chatMessages">
                <div class="chat-paused-overlay">Chat to'xtatildi</div>
            </div>
            <div class="input-container">
                <input type="text" class="chat-input" placeholder="Xabar yozing..." id="messageInput">
                <button class="send-button" id="sendMessage">Yuborish</button>
            </div>
            <div class="button-container">
                <button id="announcementButton" class="announcement-button">E'lon berish</button>
                <button class="back-button" id="backButton">Назад</button>
            </div>
        </div>
    </div>

    <div class="container hidden" id="linkPage">
        <h2>Kelin Nomzodga Xabar Yozish Uchun 👋 Tugmani Bosing Va Ko'ting 1 2 Daqiqa ❗️ Agar Kirmasa Qayta Kiring Saxifaga ❗️</h2>
        <button class="gradient-button" id="kelingaXabar">Kelinga xabar yozish</button>
        <div id="warningMessage"></div>
        <div class="animated-text" id="animatedText"></div>
        
        <h2>Qullanma</h2>
        <div class="chat-container" id="yordamMessages"></div>
        <div class="input-container">
            <input type="text" class="chat-input" placeholder="Xabar yozing..." id="yordamInput">
            <button class="send-button" id="sendYordamMessage">Yuborish</button>
        </div>
    </div>

    <div id="countdownWindow" class="hidden"></div>

    <div class="notification" id="notification"></div>
    <div class="notification-counter" id="notificationCounter"></div>

    <div id="announcementForm" class="announcement-form">
        <button id="closeAnnouncementForm" class="close-button">&times;</button>
        <input type="text" id="announcementName" placeholder="Ismingiz">
        <textarea id="announcementInfo" placeholder="O'zingiz haqida ma'lumot"></textarea>
        <input type="tel" id="announcementPhone" placeholder="Telefon raqamingiz">
        <input type="file" id="announcementImage" accept="image/*">
        <button id="submitAnnouncement">Yuborish</button>
    </div>

    <script>
        const botData = {
            botlarMatini: ["Kicha Mazza Qildim, telfonda gaplashdim 🥰",
            "Vay iflos xaromi ekan, lichkamga mani sukib qochib kitibdi",
            "Manga Poxxuy ☺️",
            "Usha erkakni topsam, tashog'ini ayiraman 😏",
            "Kicha Paynet qilgandim, tugab qoldi 😪",
            "Tanishamizmi, jon?",
            "Raxmat, shart mas umuman keragi yo'q",
            "Telfon raqamimizni bering, manga",
            "Tel raqamimni bersam, telfon qilib bezor qilasilar, shu uchun bermayman",
            "Nima hohlaysiz mandan, uzi siz?",
            "Bugun bir qiz bilan uchrashdim, juda qiziqarli boʻldi 😘",
            "Men hech qachon shunday his qilmagan edim, juda yoqimli 😍",
            "Asabni Buzmayla iltimos",
            "zaybal qildinglar qizlar bormi uzi",
            "erkaklar nomer qoldiringlar",
            "rosa zirikib kittim",
            "musofirda juda zirikarli hayot",
            "ha",
            "nega",
            "sababi bormi",
            "qanday siz aka",
            "salom",
            "assalom",
            "kim bor",
            "man keldim",
            "xormayla",
            "manam keldim",
            "xammaga salom",
            "lichga yozvoring gapim bor",
            "mani gapim bor lichkaga qarang",
            "aloo lichkaga qaravoriyla",
            "silar botmisilar nima",
            "asta sekin yoziyla bolla",
            "o'qishga uspit qilolmayab man",
            "aka lichkamga yozmang shu chatta yozing",
            "rasm yuboringlar manga",
            "salom qandaysizlar",
            "va aliykum salom",
            "xush kilib siz",
            "xush kurdik",
            "nichamiz bugun",
            "chatda bugun odam kop",
            "bugun odam rosa kopku",
            "xa xa xa yana nima",
            "usha yegit yoqib qoluvdi",
            "aka elon berganmidiz",
            "mashu elon kimni eloni",
            "sizam elon berganmisiz",
            "xa man elon bergandim",
            "ha",
            "ha 🤣",
            "ustimdan kulyabsizmi",
            "Anashu erkak borku elon bergan usha mashinik ekan 😪",
            "extiot buliyla oramizda mashinik qizlaram bor",
            "kimni mashinik divossan jinni",
            "mani aytyabsizmi",
            "xudodan qurqiyla",
            "yolg'on gapirmayla",
            "tuxmat qilmayma endi",
            "zaybal aka sekvordizku",
            "bunchakop gapirasan shaxlo",
            "laylo san yegiting keldi",
            "erimni kim qushdi chatga",
            "voy kim manga bugun paynet qiladi 😄",
            "manga ham paynet qiladigon erkak bormikan",
            "Bla usha kuni bir yegit yozdi manga yoqib qoluvdi chornilabdi",
            "kim manga spam berdi aytvoriyla",
            "telegramga yozolmayab man",
            "elon bergan manga yozganlarga yozolmayab man",
            "эй хормайла опалар",
            "салом хуш келиб сиз",
            "сиз кайдан сиз",
            "ман элон бергандим кизлар безор килди телфон килиб",
            "ростан ака мани узим сизга 2 марта адашиб телфон килдим",
            "🤣 Томим киттиб колди",
            "салом",
            "ман янги ман чатда",
            "men xozir qushildim chatga",
            "xammaga omad",
            "опа сиз ерга теголмангиз",
            "бир умр ерсиз утасиз шекилли",
            "ака сиз уйлган аёл йук ботта",
            "сиз излаган қиз хали кирмаган",
            "ох жонум",
            "laylo opa baxtizni topdizmi",
            "baxt nima uzi",
            "dalbayoblar bir gapa",
            "nima dimoqchisiz",
            "ochig'ini ayting",
            "telfon nomer tashanglar ey",
            "odam zerikib kitti tel qiling",
            "manga kim tel qilishni hohlaydi",
            "sekaman naxxuy og'zingni yum",
            "nima",
            "hichnima",
            "jonga tegar odam ekan siz",
            "siz gapga tushunmaysiz",
            "kim aytgan busa qutog'ni yebdi",
            "shu erkak mashinik",
            "xa xa xa ulib qolaman hozir",
            "qani siz aka",
            "alooo",
            "kim tanishishni hohlaydi",
            "man bilan tanishing",
            "nichi marta elon berdiz",
            "mani elonimni kim uchirdi",
            "yana elon beraman u yegit manga yoqmadi",
            "to'g'ri manoda elon bergandim",
            "bittasi mani sekmoqchi buldi",
            "bitta odam manga seks taklif qildi",
            "elon berganlar realni uzimi",
            "ha uzimni rasmim",
            "ha man rasmim bilan elon joylagandim",
            "albatta uzimni rasmim",
            "elonidagi qiz sizmisiz",
            "opa rasmda chiroyli ekansiz",
            "nichi yoshda siz",
            "man 21 yosh man",
            "man 19",
            "men 17",
            "Man 22",
            "Ман 50 ёш",
            "Манга хотин кирак",
            "мани хотиним йок",
            "хатиним улган",
            "эриз борми",
            "манга уйланасизми",
            "Менга эр кирак 30 40 ёшли",
            "Салом манга эр кирак 45 ёшларда",
            "Salom man 17 yoshman",
            "assalom man 17 yosh",
            "mani yoshim 17 da",
            "man 32 yosh",
            "man ayol kishi man",
            "o'iz gey siz man ayol kishi",
            "siz erkakmi",
            "geymisiz aka man ayol kishi",
            "voy tovba",
            "voy man ayolman",
            "man qiz bola man",
            "rosatan qizmisiz",
            "selkani kim olib kitti",
            "borishga joyim yoq kuchada qoldim",
            "xa xa battar boling",
            "edi naxxuy",
            "sukinmayla",
            "barashangizga amim",
            "омимни йибсан шу гапинга",
            "Омимни йибсиз",
            "пашон урот",
            "сизга нима",
            "сукинмайла кизла",
            "bolla bormi uzi",
            "birorta terik jon bormi",
            "salom aka",
            "salom",
            "assalom",
            "Menku bu",
            "tanmay qoldizmi aka",
            "lichkamga u kuni yozgandizku",
            "xa tanidim aka",
            "elonimni uchirmayla",
            "mani elonimni o'chirmang",
            "nima hohlaysiz",
            "quchoqlashib yotardim oldizda busam",
            "oh mazza aka",
            "manam maskvada man",
            "kim bor rassiada",
            "rassiada yurgan yegitla qani sila",
            "musofirda yurganla bormi",
            "salam ismim dildora rassiada man xozir",
            "Шахло ман Россияда ман",
            "дилороб ман рассиада ман",
            "Малика исмим бухородан",
            "Азиза ман рассиада ман хозир",
            "Шахкат ман",
            "Манга поххуй кимсиз",
            "Dam olaman ey",
            "Ertaga chat kirasizmi",
            "Eshittiylami yaqinda admen shu chatta telfonda gaplashish imkonini qushar ekan",
            "Voy rastanmi",
            "Juda zo'r bulardi",
            "Kachon ekan shu kun",
            "Ko'rishishni juda hohlayab man",
            "ersiz odam qiynaladi",
            "odamnin bahkti yörümta bulmasin ekan",
            "Baxqlik yashashga hakim bor",
            "man Санкт-Петербургда ман",
            "petirda man",
            "1998 йил ман",
            "96 йил ман",
            "Москвада сан 2004 йил ман",
            "2006 йил ман рассиадаман хозир",
            "ман якинда келдим питирга",
            "ман танишаман",
            "мен танишмокчиман",
            "смаркандан ман",
            "Мафтуна",
            "Барно",
            "Бухоролик ман",
            "Андижон",
            "Фаргона",
            "наманган",
            "шахрисабиз",
            "navoi",
            "samarqandan man",
            "yaxshi raxmat",
            "Aka baxtizni topdizmi",
            "opa baxtizni topdizmi",
            "shu odamga ishonish qiyinda telfon qilgandim malumoti yolg'on",
            "nima aldayab siz qizlarni",
            "aka siz o'yin kulgu uchun elon bergan ekan",
            "maxsadiz yoq",
            "sovchilarizni junating qarshidan man",
            "qashqadaryodan man 2007 yil",
            "men 2008 yil",
            "gulnoza man 2005 yil",
            "1988 yil man",
            "88 yillar bormi",
            "92 lar bormi",
            "97 topiladimi",
            "qariz berib turiyla oyni oxiri beraman",
            "kimda pul bor",
            "dugonajon ishonamng anvarga",
            "dugosh Sherzod aka aldayabdi",
            "o'sha erkak manga ham tel qilgandi",
            "laylo manga tel qildi",
            "Farangiz 2003 man",
            "Toshkent",
            "Jizzaxdan man 2006 yil",
            "jizzaz",
            "sirdaryodan man",
            "ha",
            "hm",
            "😏",
            "😄",
            "aldamayman rosti",
            "rosti 2004 yil man",
            "menda usha",
            "man tanishaman",
            "manga ham yozvoriyla",
            "ha ha mashka",
            "birrasi mandan pul suratabdi",
            "bermang opa ularga pul",
            "odamlaram jinni",
            "hozir bu chatda jinni bulaman",
            "man jinni bulib qolay diyab man",
            "ichki kuyov kirak",
            "Salom ichki kuyov bulaman digan bormi",
            "salam men uz baxtimni izlab kirdim",
            "manam baxtimni izlab kirdim",
            "hop",
            "ha tushundim",
            "lich qarang",
            "spam man",
            "sizam spamdamisiz",
            "spamm bergan quling sinsin",
            "sukmayla",
            "sukinmang",
            "манга хам эр борми",
            "бахтимни излаб киргандим",
            "ёлгончилар манга телфон килманглар",
            "безор киламан телфон килиб",
            "ertaga tel qiling",
            "nomer bering",
            "nima qilasiz",
            "niga gapla",
            "kimga qanaqa yangilik bor",
            "elon natijasi qanday ekan",
            "elon bergandim 100 tacha ayol qiz tel qildi",
            "Ayollar telfon qilib bezor qilarkan elondan berganimga",
            "Elon bersa buladimi",
            "Admenga yozasiz elon qabul qiladi",
            "кимга элон берамиз",
            "ким билади адмен лечкасини",
            "Ким бор",
            "Салом хаммага",
            "Элон бераман",
            "Элонимни учиринг адмен",
            "Элтимос телфон килиб безор килманглар мани",
            "Ака элонимни яхшилаб укинг",
            "Мани элонимни укимасдан личкамга ёзманглар",
            "бугун ким нечта ёл билан танишди",
            "манга 7 та ёл тел килди бугун",
            "Охири телфонимни синдираман 1000 та ёл телфон килди",
            "элон бергандим бугун 8 та ёл килди телфон",
            "манга хам тел килди ёллар",
            "мазза",
            "кича битт ёл билан куришдим",
            "ертага учрашувибюм бор",
            "manga kim tel qilishni hohlaydi",
            "tugmani bosganingda admen bo'ladi",
            "Xa elon berdim qizlar yozdi",
            "Zor natija munisa opa raxmat",
            "Natijaga gap yoq raxmat",
            "Raxmat Munisa man kutmagandim natija bomba",
            "Aka natija zur ekan",
            "Xullar bu chatta yozganni foydasi yoq elon berib ko'ring qizlarni uzlari sizga yozishadi",
            "Xa qizlarni uzi sizga telfon qiladi elon bering",
         "Привет как дела",
        "Всему миру привет",
        "Самандар исмим",
        "мен лола бухорадан 1987 йил",
        "Элон бириб куринг курасиз ака",
        "ростан элонларга ишонсам буладими",
        "ха ака",
        "мани узим элон жойлаб курдим пулига арзийди",
        "манам элон бирсамми диб уйладим",
        "хама муниса опани махтади бир элон бераман",
        "куёвликка номзод бор хоразимдан 96 йил",
        "ман хоразимдан 98 йил анора",
        "Кашкадарёдан ман 2003",
        "ismim lobar 2004 yil man ajrashgan",
        "Gulmira",
        "Ismiz nima",
        "otiz nima",
        "kimga beramiz elon",
        "siz admenmi",
        "elon bering ishonchli aka",
        "Elon birib ko'ring ishonchli ekan",
        "ertaga elon beraman hop",
        "Qizlar manga telfon qilib bezor qilib tashadi zirikkanimdan kirdim chatga",
        "man yangi man hozir kirdim chatga",
        "Kim biladi elon berish nichpul ekan",
        "Shu kanalda elon birish 50 ming ekan",
        "Juda arzon ekan bosha kanalda 50 ming oladi hichkim telfon qilmaydi",
        "bu kanalga 50 meng tashlashga arziydi o'zim sinab ko'rdim",
        "Guli tanishamizmi",
        "voy buncha qimmat 50.000 meng",
        "Киммат маску хозир 50 минга хич нарса бермайди",
        "Ха 50 минг ташлаган ман зор натижа",
        "кимни канали бу узи",
        "канака чат бу узи ман тушунмай колдим",
        "хуш келиб сиз ака",
        "Салом хаммага",
        "Ман янги ман исмим Гулбахор",
        "Орамизда тулов килиб кизлар блан гаплашганлар борми",
        "ха гаплашганлар бор ака ишончли",
        "ман элон бериб синаб курдим ростан кизлар телфон килишаркан",
        "ман шу ёр ёрда элон бериб битта киз блан танишдим манга ёкмади у киз",
        "манам элон бериб биттаси блан учрашдим расмда чиройли киз экан",
        "Сардор яхшимисиз телфонизни кутаринг гапим бор",
        "Шайдо отим ещим 32 да бахтимни излаб кирдим буйирга",
        "Камола ман 42 еш",
        "менам рассиада туриб элон жойладим рассиада биттаси блан куришдим еши катта опа экан мехмон килиб жунатвордим уйига",
        "элон бирийла курасила натижа курсатади муниса",
        "manga poxxuy elon bermasam ham shu chatta tobvolaman sevgilimni",
        "🤐 Man aytmagandim",
        "🤣 jinni xona",
        "Qizla lich yozvoriyla gapim bor",
        "😪 Xafa man sizdan",
        "Qachon kartamga pul tashab berasiz Masurjon aka",
        "Bolam och kartamga pul tashang aka",
        "Xammasi pul surashdan boshqa narsaga utmaydi qizla",
        "Shu yor yor kanalida elon bergandim yegitlar yozdi bittasi yoqib qolgandi qochib kitti rasmimni ko'rib 🤣",
        "yuragiz tosh ekan",
        "yozvoring",
        "hamma jamul jam bitta man kam chatda",
        "elon berganlar biz nechtamiz chatda",
        "Xa aka ishonchli elon bergan man",
        "manga telfon qildi qizlar",
        "Salom Munisa opa raxmat baxtimni topdim",
        "Eriz bor ekanku telfon qilgandim eriz sukib kitti mani 🤣",
        "eri borlaram elon joylab quyganmi",
        "ajrashmasdan elon berganlar bor ekan",
        "Aka siz oldin ajrashib oling ayoliz bilan kiyin manga yozasiz",
        "Qonuniy ajrashgan man ko'rsataymi dakumentlarimni ajrim qog'oz",
        "ishondim",
        "Qizlar silar gadoymi buncha pul suraysilar",
        "Mani pul zavodim yoq",
        "Raxmat opa 2 ruzg'orga baxtimni topdim",
        "Рахмат Муниса синглим 2 рузгор учун бахтимни топдим",
        "Муниса хармат бахтимни топдим",
        "Бахтимни топдим хоразимга эрга тегябман",
        "Бухорога тегябман эрга",
        "Андижонга тегадигон аёллар борми",
        "Бирага яшагани киз кирак ман 27 ёщ",
        "Салом танишамизми",
        "Сиз кадан сиз ака",
        "Ман жиззахдан",
        "Саломга алик беринг",
        "Алик",
        "Азиз ака нечи ёщ",
        "Лола сиз нечи ёщ",
        "Ман 22 ёш",
        "61 ёщда ман болам",
        "61 ёщ",
        "34 ёщ",
        "35 yosh man",
        "28 da yoshim",
        "aka dib ayting",
        "Xozir sizga dada dib aytadi🤣",
        "Bolam bir past jim o'tir",
        "So'kmang",
        "⚠️Диккат Диккат Элон Кабул Бошланди 🟢 Ким Элон Беришни Хохласа Адменга ёзинг https://t.me/Vovo_Admen",
        "Элон Кабули Бошланди https://t.me/Vovo_Admen Хаволани Босинг Адменга ёзинг Муниса исми",
        "Менга эр керак 21 ёш ман гулустондан ман битта фарзандим хам бор",
        "Ёш киз ман 23 фарзандим бор ойла кураман диганла борми",
        "30 ёщ ман Муниса исмим эрга тегмаган ман киз боламан",
        "Дилдораман Самаркандан 20 ёш турмуш курмаган ман",
        "17 yosh man aldanib qolgan man kim mani to'y qilib olishga qurbi yetadi kuyov uchun yosh chegarasi 30 yoshgacha tegaman",
        "18 yosh man yegitim aldab ketgan erga tegaman",
        "Man 21 yosh aldanib qolgan man ota onam mani haydob chiqarib yuborgan 1 yil buldi ijarada yashayman",
        "mani bitta 3 oyliq farzandim bor 24 yosh man ajrashganman uzim ijarada yashayman",
        "Ko'chada qoldim bugunga kimni uyida joy bor",
        "tanishamiz lich yozganga surpriz bor",
        "tez lich yoziyla",
        "Tel yozing aka",
        "telfon raqamizni yozing",
        "Kichrasiz Foydalanuvchi chatda Telfon raqam Yozish taqiqlangan⚠️",
        "🗨Haqoratli So'zlarni ishlatmang",
        "So'kinmang blok bo'lasiz",
        "Xuyyet Qilib Qoldim Buncha Tez Tez Yozasilar 😃",
        "😀",
        "😄",
        "Yoqib Qoldiz😇",
        "Elon berdim hozir",
        "Ertalab elon bergandim yaxshi qizlar tel qildi munisa opa raxmat",
        "opa manga qizlar tel qilishni boshladi raxmat",
        "opa tel qilyabdi qizlar raxma",
        "quling singur qaysing spam urding manga",
        "yana spam man",
        "spam bo'ldim",
        "spamga soldi jalab",
        "jalab spam berma manga",
        "spam keldi",
        "spam qildi",
        "elon berdim telfon qilishayabdi qizlar manga",
        "Raxmat opa qizlar endi telfon qilyabdi",
        "kicha elon joylagandim bugun telfon qilishni boshladi",
        "aldamang",
        "sizni aldamadimku",
        "ha tel qildi qizlar",
        "😁 Raxmat Qizlar Telfon qilishayabdi opa",
        "Andijonli qizla tel qilyabdi opa",
        "Mani elonimga yozib qo'ying opa bekorchi qizlar telfon qilmasin",
        "Hop yozdim",
        "Elon bergandim rostini aytsam ha telfon qildi manga faqat yoshi katta opalar qildi",
        "man uzi buydoq man elon bergandim yoshim 21 da 45 50 yoshli opalar tel qilishayabdi 🤣",
        "Man 19 yosh man ko'zi yumi opalar man qiz bolaman",
        "man qiz bolaman ayollar niga telfon qilishayabdi manga",
        "lezbi opam tel qildi manga",
        "xa xa xa opa",
        "opa zor siz",
        "elon bersam momolaram tel qildi ey oxiri baxtimni topdim",
        "erga tegaman 18 yosh man",
        "21 yoshda man Aziza ismim erga tegaman",
        "18 yosh Angerindanman",
        "Quqonlik man 20 yosh",
        "ha ayol kishi man",
        "man qiz bola",
        "elon berdim",
        "Elon birdim yegitlar yozdi raxmat opa",
        "Elon joylagandim boboylar yozishdi telfon qildi",
        "2 ruzg'orga erga tegaman 23 yosh man",
        "2 рузгорга тегаман сурхондарёдан ман",
        "🚫 Телфон ракам ёзиш такикланган⛔️",
        "♻️ Элон Кабул Бошланди куёвлар адменга ёзинг",
        "Элон нархи 50 минг",
        "500 рубл тулаб элон бериб бахтимни топдим рахмат",
        "менам эрга тегсам буладими",
        "Бахтини топиб ойла курганла борми",
        "ман шу каналда уйланим",
        "ман шу муниса оркали эрга тегдим",
        "эрга тегдим яна ажрашдим",
        "ажрашган ман",
        "Мен ажрашган ёлман",
        "ажрашган ман",
        "ха ажримга берган ман",
        "эрим йок",
        "2 марта эрга тегиб чиккан ман",
        "3 марта бахтим ухшамади мани",
        "ажрашим хозир ота онам уйида ман",
        "ота онамникида яшайман",
        "Элон бердим хаммага рахмат тел килишни бошлади кизлар",
        "рахмат тел килишди кизлар",
        "тел келди манга кизлар",
        "телфон килябди манга кизлар",
        "кизлар блан гаплашдим",
        "код сотиб олдим 5 ойлик кизлар блан гаплашдим",
        "ха бахтимни топдим",
        "Код олдим рахмат",
        "Кодни кимга ёзамиз",
        "Код олганлар код ёзиш жойи бор пастта уша жойга кодни ёщинг кизни хаволаси чикади",
        "Келин номзодни хаволасига кириб булмаса бошка кизни курасиз у зацнет булиши мумкун",
        "шу киз борми чатда",
        "сизам чатдамисиз ака",
        "Код олдим рахмат Муниса опа",
        "Кодни тердим ишлади рахмат",
        "Код тириб кизни лечкасини олдим рахмат",
        "Бу код 5 ой ишлайдими",
        "Вогзалда 1998-йилда туғилган, турмушга чиқмаган, ўрта, оппоқ, хушбичим келишган истарали қиз бола бор. Олий маълумотли мактабда ишлашади узларига ухшаган укимишли йигитка беришади.",
        "Тукизбулок кучасида 1999йил жувон борлар 1та кизчалари бор эпчил чаккон.",
        "Авгонбогда 2000йил жувон борлар 1та фарзандлари бор богчада ишлашади яхши оила.",
        "2006йил уйда утиредигон кизимиз борлар урта буй истаралик.",
        "Навоийда 1993йил жувон борлар 1та фарзандлари бор бамани одобли кизимиз.",
        "Фаробий кучасида 1988йил жувон борлар 1та фарзандлари бор яхши жой буса чикаришади.",
        "Дангарада 2003йил олий малумотли кизимиз борлар оила бамани.",
        "2003йил АДМИда укидигон кизимиз борлар камгап ширингина яхши жой буса чикаришади.",
        "2003йил жувонча борлар такволи хонадон кизлари кизимиз чиройли келишкан 1та фарзандлари бор фарзандлари билан кабул киледигон инсонга турмушга чикишади.",
        "Абу тайб хукандийда 2006йил Тошкентда укидигон кизимиз борлар бамани оила кизимиз Араб тилини билишади.",
        "Навоийда 1989йил жувон борлар фарзандлари йук инситутда сиртки талимда укишади.",
        "2004йил жувон борлар одобли тарбияли 1та фарзандлари бор.",
        "Богдод туманида 2004йил жувонча борлар оз муддат яшаган инситутда 3курсда укишади.",
        "2006йил табиий чиройли кизимиз борлар келишган истарали бамани инсонлар фарзанди.",
        "2002йил жувон борлар 1ёш кизчалари бор оила яхши.",
        "Окжар кишлогида 2003йил оз муддат яшаган жувон борлар фарзандлари йук.",
        "Дангарада 1989йил жувон борлар фарзандлари йук бамани яхши жувон ишлаб чикаришда ишлашади.",
        "ХУРМАТЛИ ГРУХИМИЗ АЗОЛАРИ ШУ КИЗИМИЗИ УНАШТИРИШИБДИ БАХТЛИ БУЛИШСИН 🤲🤲🤲",
        "КИМГА БЕРГАН БУСАМ УЧИРИБ КУЙИЛАР😄😄😄😄😄",
        "ХУРМАТЛИ ГРУХИМИЗ АЗИЗ АЁЛЛАРИ РОССА КАМЕЙИБ КЕТТИК",
        "КОНТАКТ КУШИЛАР ЯНГИ АДРЕСЛАР БОР КИЗ ЖУВОНЛАР",
        "Дангарада 1990йил жувон борлар келишган одобли чеварлар 1та 6ёш фарзандлари бор яхши оила.",
        "Учкуприк туманида 1991йил турмуш уртоглори вафот эткан жувон борлар нозик 1та кизчалари бор уйда утиришади.",
        "1994 йил олий маьлумотли, аклли, истарали, урта буй бир киз борлар, зиёли оила фарзанди. Уйланганга беришмайди, оиласи зиёли, узи укимишли, иши тайин йигитга беришади. Таги Куконлик Тошкентда яшайдиганга беришади.",
        "Кора теппа махалласида 2006йил чиройли келишкан киз бола бор.",
        "Ойдин кучадан 2006йил истаралик келишкан новча узларига тук хонадон.",
        "Дангарада 1988йил фарзандсизлик сабаб ажрашишкан жувон борлар мактабда ишлашади, унверситетда укишади.",
        "Бака чорсуда 2006йил урта буй ширингина киз борлар.",
        "Учкуприк туманида 2005-йил Тошкентда Араб тилида укидигон зиели оилани кизи бор.",
        "Диёр кўчасида 2004-йилда туғилган, турмушидан жуда оз муддат яшаб ажрашган новчагина, келишган, қоши кўзи табиий қора, истарали, бамани жувонча бор. Фарзанди йўқ. укимишли кизимиз богчада ишлашади.",
        "Учкуприк туманида 2000йил олий малумотли кизимиз борлар мактабда ингилиз тилидан дарс беришади.",
        "Бувайда туманида 1995йил киз бола бор катта чевар акилли хушли кизимиз.",
        "Навоийда 2006йил оппок чиройли кизимиз борлар келишган уй хамширалигини тамомлашкан уйда утиришади.",
        "Урта кишлогда 2004йил оз муддат яшаган жувон борлар фарзандлари йук.",
        "Бувайда туманида 1990йилда тугилган турмушга чиқмаган киз бола бор.",
        "Бувайда туманида 1997йил оз муддат яшаган фарзанди йук жувон борлар.",
        "2005йио нозиккина ширингина кизимиз борлар.",
        "Бувайда туманида 1998йил оз муддат яшаган жувон борлар фарзандлари йук.",
        "Бувайда туманида 1994йил жувон борлар фарзандлари йук оила яхши истарали жувон.",
        "1992йил кизимиз борлар урта буй истарали яхши жой буса чикаришади.",
        "2006йил уйда утиредигон кизимиз борлар ширингина оила бамани.",
        "2006йил илимли кизимиз борлар уйда утиришади олилалари яхши.",
        "2005йил нозик келишкан новча хушбичим кизимиз борлар.",
        "2005йил урта буй истарали кизимиз борлар Аялари бамани.",
        "Бабушкинда 1996йил олий малумотли киз бола бор ишлашади новча.",
        "Бахмалбоб кучасида 2005йил истаралик киз бола бор.",
        "Бахмалбоб кучасида 2006йил ширингина уйда утиредигон кизимиз борлар.",
        "2005йил новча истарали кизимиз борлар.",
        "2006йил уйда утиредигон яхши кизимиз борлар.",
        "2005йил сал гавдалирок чиройли истарали кизимиз борлар.",
        "Бобобек кучасида 2006йил инситутда укидигон киз бола бор.",
        "Навоийда 2003йил жувонча борлар оз муддат яшаганлар фарзандлари йук инситутда укишади.",
        "Риштон туманида 1991йил турмушга чиқмаган олий малумотли киз бола борлар куринишига караганда ёш куринишади оила яхши яхши номзод булса Куконга хам беришоради.",
        "Дангара Курик кишлогида 1990йил турмушка чикмаган киз бола бор.",
        "1997йил олий малумотли киз бола бор яхши жой буса чикаришади.",
        "Навоийда 1994-йилда туғилган, турмушга чиқмаган ўрта бўйли, оппоқ истарали говдалик қиз бола бор.",
        "1994йил яхши келишкан истарали жувон борлар фарзандсизлик сабаб ажрашишган тиниб тинчидигон жой буса чикаришади.",
        "2006йил истаралик келишкан кизимиз борлар.",
        "2005йил урта буй табий чиройлик киз бола бор.",
        "Дустлик кучасида 2006йил оппок нозик чиройли келишкан киз бола бор.",
        "2006йил 2007йил кизлар бор яхши жой буса чикаришади оила бамани истарали келишкан кизлар.",
        "Яйпанда 1998йил чевар таййор чикариледигон киз бола бор.",
        "Аширкулмерганда урта буй истарали 2006йил ширингина киз бола бор.",
        "2005йил новча сал гавдалирок кизимиз борлар укишади оила бамани.",
        "2006йил уйда утиредигон киз бола бор.",
        "1991йил хамшира жувон борлар 2та кизчалари бор бамани истарали жувон.",
        "2006йил урта буй ширингина киз бола бор.",
        "2005йил Тошкентда 2курс кизимиз борлар чиройли келишкан истарали узларига тук хонадон узларига ухшаган жойга беришади.",
        "2004йил олий малумотли кизимиз борлар узларига тук хонадон.",
        "1990йил чиройли келишкан жувон борлар фарзандлари йук.",
        "2004йил КДПИДА 3курс музыкальныйни тугаткан уй хамширалигида укиган кизимиз борлар тикиш кулларидан келади озгина нуксонлари бор.",
        "Абу тайб хукандийда 2007йил чиройли келишкан кизимиз борлар.",
        "Шалдирамокда 2006йил замонавий кизимиз борлар банк коллежда укишкан аялари бамани.",
        "Ассалому алайкум азиз инсонлар. Мени ўғлим Бекзод 1992 йил, уйланмаган Тошкент шахар Сергили туманида яшайди.",
        "1 гурух ногирони ДЦП ҳассада юради номозхон кичкина тикув цехи бор. Соғлиги яхши оёқда нуқсони бор.",
        "Яқинда Ҳиндистонга бориб оёқларини операция қилдириб келдик, ОЛЛОХ га шукр ҳозир ўзи юра бошлади. Шароитимиз яхши.",
        "Азизлар савоб учун қиз топишга ёрдам беринглар. Ўғлимдан кичкина қизлар, 2гурух ногиронлиги бўлса хам Тошкент ва водийдан қиз керак, тикувчи бўлса жуда яхши бўларди.",
        "Ўқийман деса ўқитамиз. Бу тақдир. Эълон берувчи онаси.",
        "Мукимий шахарчасида 1998йил жувон борлар нозик келишкан истарали 1та кизчалари бор оналари олиб колишади такводор номозхон кизимиз.",
        "Навоийда 2002йил фарзандлари йук жувон борлар.",
        "Бувайда туманида 1987йил олий малумотли жувон борлар 1та фарзандлари бор олиб колишади.",
        "2006йил урта буй келишкан истарали киз бола бор.",
        "Мукимий шахарчасида 2002йил фарзандлари йук жувон борлар.",
        "1981йил кизимиз борлар оила бамани яхши жой буса турмушка чикишади кизимиз ишлашади умрага бориб келишкан огир босик кизимиз.",
        "Гузар кучасида 2004йил инситутда 2курс акилли келишкан истарали доим кулиб турадигон кизимиз борлар хам диний хам дунёвий илимга эга.",
        "1994йил жувон борлар оила яхши 1та фарзандлари бор фарзандлари билан кабул киледигон инсонга турмушга чикишади.",
        "1995йил олий малумотли жувон борлар оила зиёлик 1та фарзандлари бор оналари олиб колишади кизимиз нозиккина хушбичим истарали.",
        "1999йил новча олий малумотли сал гавдалирок киз бола бор.",
        "2006йил бувили кизимиз борлар эпчил чаккон.",
        "2004йил Тошкентда 3курс кизимиз борлар оила бамани кизимиз истарали.",
        "Чинобод кишлогида 1987йил киз бола бор ота оналари утиб колишкан яхши жой буса чикаришади.",
        "Учкуприк туманида 1991йил олий малумотли врач кизимиз борлар Фаргонада ишлашади узларига ухшаган олий малумотли инсонга турмушга чикишади кизимиз хам диний хам дунёвий илимга эга оила зиёлик.",
        "1999йил олий малумотли кизимиз борлар оила яхши бувили.",
        "2006йил кизимиз борлар оппокина.",
        "2006йил новча кизимиз борлар оила яхши.",
        "Токзор кўчасида 2001-йилда туғилган, турмушга чиқмаган, оппоқ, новчагина истарали қиз бола бор. Олий маълумотли. ўқимишли йигитга беришади.",
        "Дангарада 2003йил АДМИда 4курс кизимиз борлар чиройли бамани яхши киз.",
        "Гумойлида 2003-2005йил опа сингиллар бор.",
        "2002йил 1та кизчалари бор бамани жувон борлар хужейинлари утиб коган.",
        "Абу тайб хукандийда 1987йил жувон борлар 1та фарзандлари бор фарзандлари билан кабул киледигон инсонга турмушга чикишади.",
        "Абу тайб хукандийда 2007йил кизимиз борлар урта буй истарали.",
        "2006йил бувили кизимиз борлар истарали оппок.",
        "2001йил олий малумотли кизимиз борлар оила зиёли.",
        "2005йил кизимиз борлар оила бамани бувилик.",
        "2006йил уйда утиредигон кизимиз борлар истарали.",
        "2006йил кизимиз борлар истарали пазанда.",
        "1992йил жувон борлар 1та фарзандлари бор бамани истарали кизимиз тиниб тинчидигон жой буса чикаришади.",
        "1986йил киз бола бор яхши жой буса чикаришади.",
        "Сарик камиш кучасида 2005йил унверситетда 2курс. Курон хатим килишкан илимли кизимиз борлар.",
        "2000йил жувон борлар фарзандлари йук.",
        "Навоийда 1984йил жувон борлар олий малумотли мактабда ишлашади келишкан истарали 1та кизлари бор чикаришкан.",
        "2006йил говдалирок истарали киз борлар оила бамани.",
        "Навоийда 2005йил кизимиз борлар новча келишкан.",
        "Шалдирамок кучасида 1988йил фарзандлари йук жувон борлар.",
        "Учkupрик туманида 1988-1991йил опа сингиллар бор эпчил чаккон.",
        "2005йил бамани одобли кизимиз борлар бувилик.",
        "1999йил жувон борлар фарзандлари йук.",
        "Бувайда туманида 2000йил олий малумотли стоматолог кизимиз борлар.",
        "Яна Бувайда туманида 2000йил мед инситут тамомлаган киз бола бор.",
        "Бувайда туманида 2004йил жувонча бор.",
        "Бувайда туманида 2000йил олий малумотли киз бола бор.",
        "Бувайда туманида 2002йил Тошкентда Инс Institutda укидигон кизимиз борлар.",
        "Амир темур кучасида 2005йил истаралик оппок хушбичим киз бола бор.",
        "Навоийда 1989йил фарзандлари йук истарали эпчил чаккон жувон борлар.",
        "Телемин кишлогида 2005йил Тошкентда укидигон кизимиз борлар оила бамани.",
        "2006йил озода пазанда кизимиз борлар оила бамани келишкан истарали узларига тук кизимиз Курон хатим килишкан Умрага боришкан.",
        "Навоийда 1988йил жувон борлар фарзандлари йук.",
        "Навоийда 2001йил жувон борлар фарзандлари йук.",
        "Навоийда 1992йил олий малумотли жувон борлар 1та фарзандлари бор фарзандларини бошини силедигон инсон буса оила куришади.",
        "Абу тайб хукандийда 1993йил оз муддат яшаган жувон борлар фарзандлари йук ширингина бамани.",
        "2006йил юридическига кирган кизимиз борлар кизимиз табий чиройлик кош кузлари кора.",
        "Абу тайб хукандийда 2004йил Тошкентда укидигон кизимиз борлар пазанда истарали келишкан Илимлари бор.",
        "Нефт базани кучасида 2001йил олий малумотли кизимиз борлар.",
        "1995йил фарзандлари йук врач жувон борлар оила бамани.",
        "1997йил жувон борлар фарзандсизлик сабаб ажрашишган оила зиёли кизимиз олий малумотлилар новча Врач.",
        "Олмаота кучасида 2000йил жувон борлар 1та фарзандлари бор эпчил чакон бамани яхши жой буса чикаришади.",
        "Хужакент кучасида 1985-1990йил опа сингиллар бор 1тадан фарзандлари бор тиниб тинчидигон жой буса чикаришади.",
        "2005йил кизимиз борлар яхши оила.",
        "Шилдирда 1992йил жувон борлар фарзандлари йук оила бамани медиклар хам чевар Умрага бориб келишкан яхши жой буса чикаришади.",
        "Навоийда 1988йил жувон борлар оз муддат яшаганлар фарзандлари йук истарали кош кузлари кора.",
        "Учкуприк туманида 1998йил олий малумотли кизимиз борлар Куконда ингилиз тилидан дарс беришади Курон укиган уранган киз.",
        "Сулаймон махалласида 1985йил жувон борлар оз муддат яшаганлар жиддий сабаб билан ажрашишган фарзандлари йук чеварлар хам медик.",
        "Фуркат туманида 1998йил олий малумотли киз бола борлар мактабда ишлашади яхши оила.",
        "Шикаргох кучасида 2005йил опа сингиллар бор инситутда укишади оила бамани.",
        "2004йил истарали новча бамани киз бола бор.",
        "2004йил КДПИДА 3курс музыкальныйни тугаткан уй хамширалигида укиган кизимиз борлар тикиш кулларидан келади озгина нуксонлари бор.",
        "2007йил чиройли тарбияли кизимиз борлар.",
        "Гузар кучасида 2004йил Инситутда укидигон илимли чиройли киз бола бор.",
        "1981йил киз борлар ишлашади Умрага бориб келишкан оила бамани тенгилари чикса турмуш килишади.",
        "Яйпанда 2002йил келишкан чевар кизимиз борлар истарали тарбияли кизимиз оила бамани Куконгаям беришоради.",
        "Абу тайб хукандийда 2006йил бувили кизимиз борлар.",
        "Учкуприк туманида 1998йил укитувчи кизимиз борлар укиганга беришади.",
        "Маргилонда 1992йил фарзандлари йук жувон борлар келишкан истарали оналари врач яхши жой буса чикаришади.",
        "2000йил оппок чиройли келишкан жувон борлар фарзандлари йук узларига ухшаган оз муддат яшаган фарзанди йук йигитка беришади.",
        "2001йил фарзандлари йук жувон борлар.",
        "2004йил 3курс кизимиз борлар яхши оила.",
        "1999йил Тошмини битириб кеган врач кизимиз борлар истарали узларига ухшаган жойга беришади.",
        "2005йил оппок новча келишкан кизимиз борлар.",
        "1994йил илимли жувон борлар оилалари бамани 1та кизчалари бор фарзандлари билан кабул киледигон Аллохни таниган инсонга беришади.",
        "2006йил илимли кизимиз борлар истарали.",
        "2003йил келишкан истарали кизимиз борлар оппок новча уйда утиришади.",
        "2003йил узларига тук истарали кизимиз борлар.",
        "2003йил унверситетда укидигон кизимиз борлар.",
        "Пахлавон кучасида 2005йил чиройли одобли нуткларида сал нуксонлари бор киз бола бор.",
        "Учкуприк тумани Гиждон кишлогида 2003йил Укимишли кизимиз борлар.",
        "Учkupрик туманида 2003йил Укимишли кизимиз борлар оила бамани Врачка беришади.",
        "Men gaplashdim qizlar bilan.",
        "raxmat menam gaplashdim.",
        "elon berdim qizlar telefon qilishdi 🤣.",
        "xa qildi 😁.",
        "Munisa raxmat sizga.",
        "munis raxmat elon uchun.",
        "Opa raxmat elonimni uchiring.",
        "munisa opa raxmat sizga elonimni olib tashlang.",
        "mani elonimni uchiring opa baxtimni topdim.",
        "raxmat opalar ishlarizga omad.",
        "kod sotib olmoqchiman.",
        "kod kirak manga.",
        "kodni kim biladi aytvoriyla.",
        "Diyora ismim 2007 man.",
        "Shaxlo man 26 yosh ajrashgan.",
        "Malika ismim oila qurmagan man 2004 yil.",
        "2005 yil man Odina ismim.",
        "Nelu ismim toshkent.",
        "Surxondaryodan yegitlar bormi.",
        "xush kelib siz yaxshi yegit.",
        "samarqandliklar bormi.",
        "man samarqandan.",
        "navoiydan man.",
        "jizzaxdan Dildora ismim.",
        "nichinchi yil siz.",
        "Guli man buxorolik 2003 yil oila qurmagan man.",
        "Turmushga chiqmagan man 2001 yil man.",
        "elon berdim🤣.",
        "Шахсонам ман 2003 йил бухородан.",
        "Хоразимдан ман 2002 йил.",
        "элон бердим рахмат хаммага.",
        "Элон килдим куёвликка.",
        "Элон жойлаб беринг опа.",
        "Элонизни каналга жойладик.",
        "Мани элонимни олиб ташанг опа бахтимни топдим.",
        "муниса киз мени элонимни каналдан учиринг бахтимни топдим.",
        "опа мен мурод ман элонимни учиринг безор килди кизлар телфон килишиб манга.",
        "опа ха сизга рахмат.",
        "Муниса синглим рахмат сизга.",
        "Рахмат манам бахтимни шу каналда топдим.",
        "Мунис сизга каттакон рахмат.",
        "опа мени элонимни янгилаб беринг.",
        "хуш келиб сиз.",
        "саломат булинг.",
        "✋️ ёлгон малумот берманглар.",
        "хакорат килганлар спам ❌️.",
        "Элон бергандим опа янгилаб бероласизми.",
        "хоп лечкамга ёзинг элонизни янгилайман.",
        "Муниса синглим мани элонимни янгилаб беринг кизлар телфон килмай куйдику.",
        "ноинсоф булманглар элон берганда битта киз блан гаплашинглар эркаклар.",
        "Elon bergandan sung bitta qizni tanlab usha bilan gaplashinglar 100 qizni ushlab vaxtini olmaylar.",
        "Elon berdim xammasi rost ekan.",
        "Baraka toping Munisa elon berdim natija Zo'r.",
        "Zo'r raxmat.",
        "Opa raxmat kichagi elonimni uchirvorsagizam buladi.",
        "apa raxmat sizga manga qizlar telfon qilishayabdi.",
        "opa manga erdan ajrashgan ayollar telfon qilib bezor qildi.",
        "Munisa singlim man ajrashgan erkak man nega manga qiz bollar ham telfon qilayabdi.",
        "Opa manga ham qiz bollar telfon qilayabdi ayting faqat ajrashganlar telfon qilsin manga.",
        "Ajrashgan ayollar telfon qilsin.",
        "Telfon nomer tarqatmayla.",
        "Manam elon beraman bugun.",
        "Kuyovlikka nomzodimni quyib keldim hozir.",
        "Munisa lichkamga karta tashang tulov qilib elon joylamoqchiman.",
        "Синглим карта беринг.",
        "Элон жойлаш кирак муниса.",
        "карта беринг.",
        "Мен муниса элон беришни хохласангиз личкамга ёзинг.",
        "Элон бериш учун тулов киласиз личкамга ёзинг.",
        "Кандай элон беришни билмаябман.",
        "элон жойлаб бераман личкамга ёзинг.",
        "мани личкам бу @Munisa_Admen.",
        "Elon Joylayab man kanalga kim Uz nomzodini quymoqchi lichkamga yoziyal.",
        "Diqqat diqqat elon qabul boshlandi.",
        "kimda elon bor lichkamga yozvoriyla.",
        "Elon qabul qilaman lichkamga yoziyla.",
        "Kimda elon bor qabul boshlandi.",
        "Manga yozing elon joylaymiz.",
        "Elon berish uchun admenga yozing.",
        "Kuyovlik uchun nomzodini qoymoqchi buganlar yozinglar elon qilib beramiz.",
        "Barno man 2008 yil.",
        "Kirgiziyadan man 2006 yil.",
        "Man andijondan Muxlisa 2006.",
        "Lola man erga tegib ajrashgan man 21 yosh.",
        "22 yosh man hilola.",
        "Hilola 23 yosh man vodiydan.",
        "Xurshida man ajrashgan 20 yosh.",
        "Elon beraman diganlar lichkamga yozing.",
        "Dildora 2005 ajrashgan.",
        "Man ajrashgan man aka.",
        "Xa qiz bola man.",
        "Gulustondan man Sevara ismim.",
        "2001 yil man Farangiz.",
        "Фарангиз ман 1999 йил.",
        "Латофат исмим 1987 йил.",
        "Лола ман ажрашган 1980 йил.",
        "Farida ismim ajrashgan man 19 yoshda man.",
        "Negina sizga gapim bor.",
        "zirikkan qizla lichkamga yoziyla tanishamiz.",
        "elon berib keldim.",
        "Voy munisa raxmat sizga xamma telfon qilaybdi elon berganimga"],
            httpsManzillar: [
                "https://t.me/Bahoroy",
                "https://t.me/no_na_me1885",
"https://t.me/zara_dior80",
"https://t.me/kz_kz999",
"https://t.me/SSSSFFFFGGGGGJ",
"https://t.me/asiya7777",
"https://t.me/yasin00193",
"https://t.me/Rainbow95959",
"https://t.me/LilithEva9",
"https://t.me/Leylam1999",
"https://t.me/Shaxzoda7727",
"https://t.me/Ruxwon03",
"https://t.me/WW88SSSS88",
"https://t.me/Baxtim_5447",
"https://t.me/jenuary1",
"https://t.me/Mybbbbb0988",
"https://t.me/tavhid_ll",
"https://t.me/semuliotion",
"https://t.me/Muhammadali_0000",
"https://t.me/Jannat_shaydosim",
"https://t.me/no_na_me1885",
"https://t.me/Azizaaammm",
"https://t.me/Bonu0999",
"https://t.me/Tashxislaa",
"https://t.me/Umidimsundirma4488",
"https://t.me/Go_fitnesss",
"https://t.me/Ledydi90",
"https://t.me/gulnozaxon5",
"https://t.me/Alhamdulillah_3204",
"https://t.me/Hadicha82",
"https://t.me/Zara_0311",
"https://t.me/laylo013",
"https://t.me/thegrayswan",
"https://t.me/Bibi_09900",
"https://t.me/Sevara1525",
"https://t.me/sadiii_11",
"https://t.me/Taqdir_hazili_0",
"https://t.me/Htagfks",
"https://t.me/Lregj",
"https://t.me/Navruza_1999",
"https://t.me/Seraphine1616",
"https://t.me/deo_0102",
"https://t.me/muhsin_muhsinn",
"https://t.me/deryacha",
"https://t.me/GUZALLA7777",
"https://t.me/dilozorrrrrrr",
"https://t.me/Maryam300110",
"https://t.me/olloh_buyuk57",
"https://t.me/Donbogimmm",
"https://t.me/thesun011",
"https://t.me/pnosma19",
"https://t.me/kuz0200",
"https://t.me/amorfati050222",
"https://t.me/zooloshka",
"https://t.me/oglimga_otakerak",
"https://t.me/Navruza_1999",
"https://t.me/soxta1247",
"https://t.me/Fhjlohh",
"https://t.me/Yuivfn",
"https://t.me/Deee2224",
"https://t.me/soxta1247",
"https://t.me/shaxlor",
"https://t.me/z5677777",
"https://t.me/MKAI2010",
"https://t.me/hanafiy_aa",
"https://t.me/Baxttilayman",
"https://t.me/tehlikali",
"https://t.me/Mi_mi211",
"https://t.me/Muhammadalieva_001",
"https://t.me/BEAR5050",
"https://t.me/Tyulpancha",
"https://t.me/Bizbaxtlib",
"https://t.me/Sabrlig1m_1",
"https://t.me/Beautydollyy",
"https://t.me/Onajonimquyoshim",
"https://t.me/zara_dior80",
"https://t.me/kz_kz999",
"https://t.me/asiya7777",
"https://t.me/Rainbow95959",
"https://t.me/LilithEva9",
"https://t.me/Leylam1999",
"https://t.me/Sevara1525",
"https://t.me/Maftu89",
"https://t.me/hghgy6576yt",
"https://t.me/Baxtli836",
"https://t.me/assi1984",
"https://t.me/Jojo_96",
"https://t.me/maxliyo0606",
"https://t.me/Sferaaz",
"https://t.me/BAXORAXON555",
"https://t.me/i9irij",
"https://t.me/RobbimAllohdurr",
"https://t.me/Pro_09_08",
"https://t.me/Life_is_short0407",
"https://t.me/island77f",
"https://t.me/Hayot_sinov90",
"https://t.me/MITTIVOYIM999",
"https://t.me/nilu95hjjj",
"https://t.me/bornpink_girl",
"https://t.me/Allohbuyukdur78",
"https://t.me/aaaaa_1228",
"https://t.me/dmin_ruu",
"https://t.me/Gulqiz0",
"https://t.me/A1shem_23",
"https://t.me/MITTIVOYIM999",
"https://t.me/dilim4444",
"https://t.me/xayotshunaqa1994",
"https://t.me/island77f",
"https://t.me/Jojo_96",
"https://t.me/Seeevdaaaaaa",
"https://t.me/Mmmmhhukkk",
"https://t.me/dilim4444",
"https://t.me/nilu95hjjj",
"https://t.me/agfagfagf",
"https://t.me/Fargona1987m",
"https://t.me/nurnoma29",
"https://t.me/hghg6yt56yt54r",
"https://t.me/hghg6y743e",
"https://t.me/Allohu_Akbar_77",
"https://t.me/hghvcy654rd",
"https://t.me/Zexra9404",
"https://t.me/maybetrueor",
"https://t.me/hghgy676ytby76",
"https://t.me/Bahtliimanda",
"https://t.me/ug_0304",
"https://t.me/hghgh676yt65",
"https://t.me/hghg65yt56yt",
"https://t.me/Asmo088",
"https://t.me/ARSLONOVA1212",
"https://t.me/alora_0931",
"https://t.me/Chiroyli_qizcha_1",
"https://t.me/Ayub122134",
"https://t.me/Omadbaxtl",
"https://t.me/Zebo_34",
"https://t.me/Shohista8886",
"https://t.me/nilu95hjjj",
"https://t.me/hjhgg67uyg",
"https://t.me/Djajdjk",
"https://t.me/maxliyo0606",
"https://t.me/hghfg656yt65",
"https://t.me/Allohimgaa_shukrlar",
"https://t.me/hgdfff5554rr",
"https://t.me/Rayyona57",
"https://t.me/Orzu0690",
"https://t.me/jayrona1718",
"https://t.me/a123921",
"https://t.me/k_m_8901",
"https://t.me/xayotshunaqa1994",
"https://t.me/missledi24",
"https://t.me/Wwwwwwww1209",
"https://t.me/Shodlik_3011",
"https://t.me/Leylam1999",
"https://t.me/Ruqiyahon0011",
"https://t.me/Beautydollyy",
"https://t.me/TRRT01",
"https://t.me/laylo013",
"https://t.me/Dur_do_naaa",
"https://t.me/Dilkhon06",
"https://t.me/nigow_14",
"https://t.me/qwerty29090",
"https://t.me/Tanho_gul_97",
"https://t.me/Sakinaxon_38",
"https://t.me/Taqdir_hazili_0",
"https://t.me/Zarnigor1m",
"https://t.me/bluebird026",
"https://t.me/Fza_08",
"https://t.me/AroshEva",
"https://t.me/Ladymiss55",
"https://t.me/Baxtiyorovna_001",
"https://t.me/Hali_19_91",
"https://t.me/a182518",
"https://t.me/Alvodoooo",
"https://t.me/miss_9803",
"https://t.me/liriwa_01",
"https://t.me/alfraganiyus"
            ],
            yordamMatinlar: ["Agar qiz zaynet busa havolaga kirmaydi biroz vaxtdan sung qayta bog'lanishga xarakat qilingt", "kelin nomzod xavolasiga kirmasa u zaynet bo'lishi mumkun", "Tugmani 2 3 marta bosmang 1 marta bosib kuting agar shu 1 marta bosilganda 10 soniyada kirmasa unda zaynet saxifadan chiqib qayta kiring"]
        };

        localStorage.setItem('botData', JSON.stringify(botData));

        const validPins = ['760', '769', '6622', '6287', '76000'];
        const pinInputs = document.querySelectorAll('.pin-input');
        const errorMessage = document.getElementById('error-message');
        const sovchilarPage = document.getElementById('sovchilarPage');
        const linkPage = document.getElementById('linkPage');
        const mainTitle = document.getElementById('mainTitle');
        const pinTitle = document.getElementById('pinTitle');

        function changeText() {
            if (mainTitle.textContent === "Sovchilar") {
                mainTitle.textContent = "BAXT OILA";
            } else {
                mainTitle.textContent = "Sovchilar";
            }

            if (pinTitle.textContent === "PIN Kodni kiriting") {
                pinTitle.textContent = "Sotib Olingan Pin Kodni kiriting";
            } else {
                pinTitle.textContent = "PIN Kodni kiriting";
            }
        }

        setInterval(changeText, 7000);

        pinInputs.forEach((input, index) => {
            input.addEventListener('input', (e) => {
                if (e.target.value.length === 1) {
                    if (index < pinInputs.length - 1) {
                        pinInputs[index + 1].focus();
                    }
                }
            });

            input.addEventListener('keydown', (e) => {
                if (e.key === 'Backspace' && !e.target.value && index > 0) {
                    pinInputs[index - 1].focus();
                }
            });
        });

        document.getElementById('submitPin').addEventListener('click', () => {
            const pin = Array.from(pinInputs).map(input => input.value).join('');
            if (validPins.includes(pin)) {
                sovchilarPage.classList.add('hidden');
                linkPage.classList.remove('hidden');
                startBots();
            } else {
                errorMessage.textContent = "Kod xato terildi, qayta urinib ko'ring.";
                errorMessage.classList.remove('hidden');
            }
        });

        let isScrollPaused = false;
        let scrollTimeout;
        let longPressTimer;

        function addMessage(container, text, isUser = false, botName = '', imageUrl = '') {
            const messageDiv = document.createElement('div');
            messageDiv.className = `message ${isUser ? 'user' : 'bot'} ${botName}`;
            
            if (!isUser) {
                const avatar = document.createElement('div');
                avatar.className = 'avatar';
                if (botName === 'RasmlinkBot') {
                    const rasmlinkBotAvatars = [
                        "https://i.postimg.cc/ncWZBv3c/Picsart-24-12-18-02-47-29-563.jpg",
                    ];
                    avatar.style.backgroundImage = `url(${rasmlinkBotAvatars[Math.floor(Math.random() * rasmlinkBotAvatars.length)]})`;
                } else if (botName === 'AIChatbot') {
                    const aiChatbotAvatars = [
                        "https://i.postimg.cc/4dqW4xJP/ZpAY_eglKFA.jpg",
"https://i.postimg.cc/c4NcFj6v/YS7oSJjBa2A.jpg",
"https://i.postimg.cc/2S79dYwj/Yfn7uYIixk4.jpg",
"https://i.postimg.cc/m2bHzGty/x_1d395d09.jpg",
"https://i.postimg.cc/02BykgmQ/XAzkeEABR7Y.jpg",
"https://i.postimg.cc/k5DNVPYp/x-P8A0ForG0.jpg",
"https://i.postimg.cc/9fz0Pmhy/vU_LuXgwdMI.jpg",
"https://i.postimg.cc/rFJwv0yS/TH3EVH4dVgI.jpg",
"https://i.postimg.cc/cCLbCbY1/SmJhJ8p2xE4.jpg",
"https://i.postimg.cc/xCCvzDsZ/rTXLoMANsd0.jpg",
"https://i.postimg.cc/9XskCJ02/QtlfVAhkEt4.jpg",
"https://i.postimg.cc/Xqx6D5Kq/QP_n4s6-3y0.jpg",
"https://i.postimg.cc/vBrsfkcW/QovNcz4hM1M.jpg",
"https://i.postimg.cc/Hnb9p0vW/oydt228thf.jpg",
"https://i.postimg.cc/j50TWtdx/OrDHQP2BoE0.jpg",
"https://i.postimg.cc/BZ26B7d7/nk9c9BVjeis.jpg",
"https://i.postimg.cc/5tv0KPXt/NBgxjOAcHtI.jpg",
"https://i.postimg.cc/wv7Wdmd3/M2TXQ6dluRI.jpg",
"https://i.postimg.cc/rwRFzhC9/k84AmPyEB5Q.jpg",
"https://i.postimg.cc/XvT5pGCr/IMG_0932.jpg",
"https://i.postimg.cc/7ZZZDHbj/IKhDu0gvO04.jpg",
"https://i.postimg.cc/7ZRGWGXK/IcEPYCtitno.jpg",
"https://i.postimg.cc/zG2XGsgv/i_-_2024-12-18T020644.719.jpg",
"https://i.postimg.cc/VN3fjX4c/i_-_2024-12-18T020640.227.jpg",
"https://i.postimg.cc/bJkzLdFS/i_-_2024-12-18T020633.566.jpg",
"https://i.postimg.cc/XYGt9mPp/i_-_2024-12-18T015900.896.jpg",
"https://i.postimg.cc/zfTMcW8N/i_-_2024-12-18T015758.856.jpg",
"https://i.postimg.cc/6pkgczsz/i_-_2024-12-18T015754.624.jpg",
"https://i.postimg.cc/SsrPyhnt/i_-_2024-12-18T015749.885.jpg",
"https://i.postimg.cc/WzYfkw6G/i_-_2024-12-18T015737.403.jpg",
"https://i.postimg.cc/W4mWnvwb/i_-_2024-12-18T015602.512.jpg",
"https://i.postimg.cc/ZRTfsMwP/i_-_2024-12-18T015521.506.jpg",
"https://i.postimg.cc/j5ZMp41p/i_-_2024-12-18T015516.641.jpg",
"https://i.postimg.cc/sxxTsZdv/i_-_2024-12-18T015508.512.jpg",
"https://i.postimg.cc/VsZ744nM/i_-_2024-12-18T015451.913.jpg",
"https://i.postimg.cc/rFdfHWNH/i_-_2024-12-18T015446.324.jpg",
"https://i.postimg.cc/Qd1083Pk/i_-_2024-12-18T015423.034.jpg",
"https://i.postimg.cc/zfNp3QYm/i_-_2024-12-18T015413.385.jpg",
"https://i.postimg.cc/tTC5NVg2/i_-_2024-12-18T015407.024.jpg",
"https://i.postimg.cc/zvyF9ZKh/i_-_2024-12-18T015355.878.jpg",
"https://i.postimg.cc/Y0Tz7nzs/i_-_2024-12-18T015351.099.jpg",
"https://i.postimg.cc/ryHJ5s2N/i_-_2024-12-18T015347.166.jpg",
"https://i.postimg.cc/MKjY5wW2/i_-_2024-12-18T015340.718.jpg",
"https://i.postimg.cc/8zQmnY5F/i_-_2024-12-18T015331.973.jpg",
"https://i.postimg.cc/9QdY3BRL/i_-_2024-12-18T015322.526.jpg",
"https://i.postimg.cc/jjRQRJyt/i_-_2024-12-18T015310.420.jpg",
"https://i.postimg.cc/tgDdJCzP/i_-_2024-12-18T015306.099.jpg",
"https://i.postimg.cc/9XDk6vW1/i_-_2024-12-18T015219.582.jpg",
"https://i.postimg.cc/8zSnrcLn/i_-_2024-12-18T015202.715.jpg",
"https://i.postimg.cc/tgRS2cS3/i_-_2024-12-18T015145.740.jpg",
"https://i.postimg.cc/VvtDJPv8/i_-_2024-12-18T015106.547.jpg",
"https://i.postimg.cc/m2xm0kp2/i_-_2024-12-18T015035.476.jpg",
"https://i.postimg.cc/SxdV2rSJ/i_-_2024-12-18T015018.329.jpg",
"https://i.postimg.cc/tgf3WvLC/i_-_2024-12-18T014736.795.jpg",
"https://i.postimg.cc/xTRLt1WZ/i_-_2024-12-18T014709.658.jpg",
"https://i.postimg.cc/GtPv0L9H/i_-_2024-12-18T014659.196.jpg",
"https://i.postimg.cc/25qvkFVp/i_(7).jpg",
"https://i.postimg.cc/0yyD3qvy/i_(4).jpg",
"https://i.postimg.cc/7hBYJdWK/i_(31).jpg",
"https://i.postimg.cc/QtJMhHkG/i_(27).jpg",
"https://i.postimg.cc/Xq86WB79/0e2dc996-e798-426d-b3be-621a346d41ec-image.png",
"https://i.postimg.cc/RVFDhDgk/0e25aaca-17e4-480d-b3b2-65ac292ef87c_image.png",
"https://i.postimg.cc/CxnrHfTJ/da50d429-d989-4479-8f27-47640284bf72_image.png",
"https://i.postimg.cc/KYn9CSYM/faa10a01-ed73-4283-9f9f-4ad1482994a0_image.png",
"https://i.postimg.cc/152Jt5nF/68dedd04-aa99-49c8-8ef6-b8320c073fc6_image.png",
"https://i.postimg.cc/3R8Z6k6s/6ae0ec87-2bc3-4385-858d-ef9b31f3e164_image.png",
"https://i.postimg.cc/d1ZGgG6S/c4f1d469-fbc8-442c-868d-4cb739a9ef83_image.png",
"https://i.postimg.cc/gkm6HCC7/1ed3f7000d16c581037464d0c666bdde.jpg",
"https://i.postimg.cc/bYHZr6Z9/9d066084-383b-4daa-9062-b158f7054b34_image.png",
"https://i.postimg.cc/HL4qX7XR/062c0617-cc65-4f2e-97fb-88e994de940e_image.png",
"https://i.postimg.cc/pX0mK2NX/Screenshot_20241215_084412_Telegraph.jpg",
"https://i.postimg.cc/LsD3Jrwg/5ee8e958-0af0-456f-9cb7-7baf3619d3a8_image.png",
"https://i.postimg.cc/Y2Rwn2VL/42d38c0d-ca75-4295-ba7d-80494a524ee5_image.png",
"https://i.postimg.cc/Ls5TpD6M/d8d0e86e-07e1-427e-8ba6-3c5ac65f3fbe_image.png",
"https://i.postimg.cc/hjgtmyJk/0e6436b1-35e0-4ed4-8469-00d4457c2b57_image.png",
"https://i.postimg.cc/CxghXr7z/b75b4c83-a219-4ecf-9a37-31910293d058_image.png",
"https://i.postimg.cc/sD08ZMQy/c333892d-c532-43ec-8fe6-b04cc15ffca3_image.png",
"https://i.postimg.cc/13qWnJ1c/7ac0b14a-6b45-419c-991a-523b7d25dd33_image.png",
"https://i.postimg.cc/JzVNg8SZ/689b5846-cdfd-4f97-8f3e-7e89f23ade37_image.png",
"https://i.postimg.cc/63vRz1zY/ef4b4604-7518-42dd-8adb-60d97a74d6ad_image.png",
"https://i.postimg.cc/Wbjr68Zw/af88b22c-62f4-4e53-9182-3f2ad8f73117_image.png",
"https://i.postimg.cc/L5SqD4J8/8a424c6f-b30e-4db2-9af0-837f483508ed_image.png",
"https://i.postimg.cc/wT6ysvKW/b985ffc2-b613-467f-b802-b2d80be782bc_image.png",
"https://i.postimg.cc/PJfXNCLY/906aa0a3-57f7-4883-8dd2-7db89643c387_image.png",
"https://i.postimg.cc/xC6CvGVt/Screenshot_20240821_110804_Threads.jpg",
"https://i.postimg.cc/TYLwbW7J/Screenshot_20240904_111955_Threads.jpg",
"https://i.postimg.cc/wBT374S7/Screenshot_20240901_091754_Threads.jpg",
"https://i.postimg.cc/d0xQDs2x/Screenshot_20240818_130340_Threads.jpg",
"https://i.postimg.cc/kGx7jWk0/Screenshot_20240819_145653_Threads.jpg",
"https://i.postimg.cc/yYvM7fXf/d92f542a-1368-4232-8ab8-a00e66986d70_image.png",
"https://i.postimg.cc/9fjtK2Rs/Screenshot_20240816_132041_Threads.jpg",
"https://i.postimg.cc/pTsfmnGt/Screenshot_20240817_053138_Threads.jpg",
"https://i.postimg.cc/fTmvKkkY/Screenshot_20240814_110338_Threads.jpg",
"https://i.postimg.cc/kGrb6FQz/0405daa9-780a-4d0f-ab1a-fe37f41c01df_image.png",
"https://i.postimg.cc/GprgYGQB/6f96372a-f875-42ee-bcd4-89bf115149ba-image.png",
"https://i.postimg.cc/FKZWxzWT/Screenshot-20240821-185911-Threads.jpg",
"https://i.postimg.cc/wvjW4zng/Screenshot-20240827-125954-Threads.jpg",
"https://i.postimg.cc/GtZqpytm/Screenshot-20240822-070602-Threads.jpg",
"https://i.postimg.cc/rp8gzcVx/Screenshot-20240819-114043-Threads.jpg",
"https://i.postimg.cc/t7QNbGv1/cb378dab-86f7-4b40-adaf-e84bfbd62f00-image.png",
"https://i.postimg.cc/44rDyKrc/93917ca8-e3c3-49e6-afae-c25a74f3e676-image.png",
"https://i.postimg.cc/LsC7phtn/8813e81b-7d8d-4eff-a607-7ee1f9a045b0-image.png",
"https://i.postimg.cc/5yvkL3ZC/Screenshot-20240906-213925-Threads.jpg",
"https://i.postimg.cc/66GPkWyp/Screenshot-20241001-131235-Threads.jpg",
"https://i.postimg.cc/SxmtYcVn/Screenshot-20240905-034541-Threads.jpg",
"https://i.postimg.cc/15rvSfPs/c62b6dea-540d-4143-a636-fffe31040a91-image.png",
"https://i.postimg.cc/hGfsVsmt/eba09edd-c1d4-4e1a-86e5-52a910703d03-image.png",
"https://i.postimg.cc/prtBbt6m/7bf49cfa-b6ef-4038-a238-b919aab5edb7-image.png",
"https://i.postimg.cc/kg5vdsfv/17e65cde-2459-4b74-a6ef-f636d103bdd8-image.png",
"https://i.postimg.cc/LsctLpRx/bfaae242-1bea-4eb4-99ce-20980445deed-image.png",
"https://i.postimg.cc/LXPr32P5/fed6a9d2-5333-4406-8297-f972a2c1805f_image.png",
"https://i.postimg.cc/L8NRJ9kM/fd3e4dbd-0e31-4a10-bce7-b3aac0bad885_image.png",
"https://i.postimg.cc/65qfkzHL/f14b6f64-06dc-4717-818a-17a3eedc83d2_image.png",
"https://i.postimg.cc/W4vpkWCM/eb265036-27bd-4d57-8b19-9e7f04d4676c_image.png",
"https://i.postimg.cc/cJSYLccz/ea6caa9b-ed75-4030-9632-b84553873e41_image.png",
"https://i.postimg.cc/rsKqkvRL/e91ec9d6-bb0c-43ba-ba3f-aad2442a976f_image.png",
"https://i.postimg.cc/wTrQgJZK/e5fe4ab3-c428-4772-976a-b9c26c62ee58_image.png",
"https://i.postimg.cc/rmg5btxP/e5ce4602-5557-48b9-ad31-4e7a70729ea6_image.png",
"https://i.postimg.cc/Xvd82JsR/e0d93014-19e6-4175-9511-e7f7d840e80d_image.png",
"https://i.postimg.cc/j5ThBb9L/ded52d4e-fdfb-4b8b-bea9-76accb712914_image.png",
"https://i.postimg.cc/DfX2xKhq/ddee6225-3e9a-46b1-8496-403fd8526983_image.png",
"https://i.postimg.cc/SxK3tW9w/da152d64-3d24-4a18-95da-c19c18571c5f_image.png",
"https://i.postimg.cc/pXs18pSk/d926cac1-6e05-4784-b282-0c5dd630c092_image.png",
"https://i.postimg.cc/XYwGmC0k/d380ca88-11e6-4ff4-8eeb-8915beab70e2_image.png",
"https://i.postimg.cc/XYwGmC0k/d380ca88-11e6-4ff4-8eeb-8915beab70e2_image.png",
"https://i.postimg.cc/Z51HF3xP/d20a6254-ea13-4fb3-95ce-197a89dba8e9_image.png",
"https://i.postimg.cc/B6JxMCLF/d1053e12-46f8-4bda-a036-227b97a61d90_image.png",
"https://i.postimg.cc/7h6SyYNY/d0bcde7f-80a8-4b1f-ad2d-4e1521a990e0_image.png",
"https://i.postimg.cc/t40nBz8g/d0aa2129-6421-4e86-8513-355acbbb549b_image.png",
"https://i.postimg.cc/SKPhGgtT/ce09e161-0ad2-4af6-9a21-1a2baf6a67c4_image.png",
"https://i.postimg.cc/SKPhGgtT/ce09e161-0ad2-4af6-9a21-1a2baf6a67c4_image.png",
"https://i.postimg.cc/V63zzKqr/c512105c-d41d-46a5-bedc-7e0d50404787_image.png",
"https://i.postimg.cc/J4xSqTsN/c298d597-a51a-42df-9e23-6b34e08956bb_image.png",
"https://i.postimg.cc/T1FfYCn5/c0d690ba-bb6b-4f82-bfbc-749ff9f56529_image.png",
"https://i.postimg.cc/JhzrxD7n/bfe3564a-53b8-4ffd-b241-9a23fa6d2887_image.png",
"https://i.postimg.cc/sxqGdPXw/be030da4-70a2-465e-b9e8-3ebf16d3075d_image.png",
"https://i.postimg.cc/hPcHVFt4/bc7e3183-3392-440a-a7ab-6b8815046546_image.png",
"https://i.postimg.cc/htgPJZHV/bb4c5f24-83bc-4379-99ab-a0412b0a25a0_image.png",
"https://i.postimg.cc/59RCCJ3L/ba261a6a-f88d-4c11-baa6-521364a582ea_image.png",
"https://i.postimg.cc/NfCpFZyz/b4babdd9-0490-490f-9662-6fe21114f992_image.png",
"https://i.postimg.cc/XJNCw7mc/af7550b9-f493-4dc2-b9e9-a081ec0c20e9_image.png",
"https://i.postimg.cc/kGtLw9tD/a83de5d0-6d29-4f26-b154-cb6357565598_image.png",
"https://i.postimg.cc/yYh7zXkx/a6fea91b-cc24-4e0e-a0ca-99d64c6c6bd9_image.png",
"https://i.postimg.cc/tgkbVXhj/a6ce71dd-6a67-45fe-888d-47636ad32af9_image.png",
"https://i.postimg.cc/nLSHPFM1/a13c7be0-b90d-4a35-8932-89d0e50fed2c_image.png",
"https://i.postimg.cc/4xNRkDD2/9e43925f-75aa-4b04-ab09-cbe03743794e_image.png",
"https://i.postimg.cc/NM8d0MT6/9e282350-f73c-44f2-89ea-b7935bb40349_image.png",
"https://i.postimg.cc/rmhq78mJ/9802567a-2779-49a7-a7fc-753a34777d12_image.png",
"https://i.postimg.cc/9FmnrGLr/9605b7ef-869d-467f-81f4-141bd6ee99a1_image.png",
"https://i.postimg.cc/6pjJ9HwW/92b97406-aeb8-4743-bd62-402f8b348298_image.png",
"https://i.postimg.cc/RZbyrNQq/8a8c49be-6951-462c-85d2-cc8168d4f2d6_image.png",
"https://i.postimg.cc/RVwZZxbM/87c7abaa-703b-41d7-8720-b2410bafcc8e_image.png",
"https://i.postimg.cc/BvS93dRw/86658ba2-1f0b-41e2-a261-9678b5268c15_image.png",
"https://i.postimg.cc/Xv4GbYjS/86656fe8-d082-4ef8-abe2-d27cdd560657_image.png",
"https://i.postimg.cc/y8WpT74K/7e20ca80-fc08-4c57-9b35-1ee7258ee60b_image.png",
"https://i.postimg.cc/Gh6GZRTd/7a7de9e6-292d-4a46-aa54-455806ed8013_image.png",
"https://i.postimg.cc/tTRXr1XJ/79b82f9f-6839-4086-b07e-959d1c33c13d_image.png",
"https://i.postimg.cc/FKYt1jsj/767f6485-1dad-4956-bf35-f423af87bbf4_image.png",
"https://i.postimg.cc/htr4VbB6/7529667d-c306-45a0-ab4f-b891179ba324_image.png",
"https://i.postimg.cc/fR3595mT/6d77ccfc-7a42-49a4-8091-8a1ccb0815e2_image.png",
"https://i.postimg.cc/HsMC90Q3/6a3e37bb-3f6d-4c4a-ae77-3d369eb5793c_image.png",
"https://i.postimg.cc/bwQpp0rd/68b3b09c-9133-49cf-a0f6-220ad95a1bc0-image.png",
"https://i.postimg.cc/XJvbfT8y/68ae74e3-d7dd-474e-aa95-11bb65e1e0d3-image.png",
"https://i.postimg.cc/sXZRH5kV/650b4e09-3ff9-4bd3-ab97-9f2666eebbb6-image.png",
"https://i.postimg.cc/mkGKdJ3w/63ed3e83-b991-421b-b2fd-de4ad54da29a-image.png",
"https://i.postimg.cc/j52pwyxH/63cfc56f-44c1-46a1-bc0e-c2c9a270a2fa-image.png",
"https://i.postimg.cc/kgtF4GP2/63b26158-e97b-4340-8d8e-1bfdd0ecfefb-image.png",
"https://i.postimg.cc/NMPwppJC/63ac7722-09db-450e-9e71-5707add448a6-image.png",
"https://i.postimg.cc/Znp4n6Hf/60b70996-f621-4cdc-8e35-4e9e0b7baea6-image.png",
"https://i.postimg.cc/zDtnFKJL/5f6c7e5b-3bd0-4ecd-8822-28bbe8bbfe88-image.png",
"https://i.postimg.cc/257WbBcS/5ed0e403-c0ab-4367-b3a2-9c02eaab4bf5-image.png",
"https://i.postimg.cc/90WJwhtv/586d212d-4eba-4653-87b5-917a167d37b3-image.png",
"https://i.postimg.cc/4dpShwCh/57138345-4a41-4036-9bca-28b4449c57a1-image.png",
"https://i.postimg.cc/vT3XWN0D/5660bb77-c08d-4650-b44a-34e0c211e7d8-image.png",
"https://i.postimg.cc/wTRs5rfP/53da4348-f26e-401c-b94b-f5782a71f977-image.png",
"https://i.postimg.cc/Y23XKvtk/4f6c5bd4-b1c6-45ff-a4b4-ecbc8ebe740e-image.png",
"https://i.postimg.cc/3wvLP9xb/4a3dbb6a-16ca-4738-8575-9ad08394b791-image.png",
"https://i.postimg.cc/QxFc4Ctf/48e1c0c3-a0eb-4a72-8dec-1f3963c6c788-image.png",
"https://i.postimg.cc/yxYyYT7K/48b9f95d-d1e3-45a1-9e76-171681bd8b34-image.png",
"https://i.postimg.cc/tJZGfW8q/4445d1db-89e3-4a5b-bcbe-00535577ecc5-image.png",
"https://i.postimg.cc/Kc6Yb8fq/41856986-0847-4c72-bc55-75a54c3cd7b6-image.png",
"https://i.postimg.cc/Bb9frX32/40ac1175-9194-43d6-abe9-08db4db42b7a-image.png",
"https://i.postimg.cc/3NSCyDwv/3eae55b3-4cf7-4dfd-9f80-f068e7b27c1b-image.png",
"https://i.postimg.cc/jj06JTRZ/3e5eabdc-0b64-4c9a-84d8-fea8fb99862b-image.png",
"https://i.postimg.cc/yNLq8LH6/396dcdf5-4cec-4134-82a5-1d1f7a13ac70-image.png",
"https://i.postimg.cc/wxhCtxHb/3199904b-144c-4a0b-985d-f4e29f5bfa82-image.png",
"https://i.postimg.cc/2SFRPz9Z/2f955612-c2c5-4b6a-986e-471a091a0f04-image.png",
"https://i.postimg.cc/qM6pZHds/2b03e0b7-a8d1-4a62-9106-bc0aea280504-image.png",
"https://i.postimg.cc/L8H24Y1T/2a2f30e5-c5a7-46e4-b782-a51d7fc55345-image.png",
"https://i.postimg.cc/52vLJr8v/243107f4-d4a9-4619-89db-23ccc1aa4197-image.png",
"https://i.postimg.cc/PxMMj7sK/225b0238-abb7-4024-a6ab-732d2a78f3eb-image.png",
"https://i.postimg.cc/0y3WWhPw/1f32b24a-99f1-4ecd-98f8-de8cf1071ce8-image.png",
"https://i.postimg.cc/k50H4zHm/1bef5703-7515-4a8f-8d45-80a8bf6e8b52-image.png",
"https://i.postimg.cc/ncxtTj0J/1627e08b-5e9f-4376-bbed-76cff23bda44-image.png",
"https://i.postimg.cc/tgJbPKDn/149f552d-d6e4-40e8-9aae-d680902cf89b-image.png",
"https://i.postimg.cc/VsVYRL2s/13b61638-5146-41ee-9e18-c49cee4d65aa-image.png",
"https://i.postimg.cc/fWmNxj7C/12184fd4-8edf-4833-929d-e919952dec43-image.png",
"https://i.postimg.cc/2jFtkHFs/0ae385d9-2040-41fe-8f95-60187034f006-image.png",
"https://i.postimg.cc/gcX01ZVL/0760c982-788e-478c-b778-d65f37e99575-image.png",
"https://i.postimg.cc/bNRf5yB2/06976094-cf55-43e0-9f4b-3df6efec44e9-image.png",
"https://i.postimg.cc/6qrxtt6g/05bdf0a0-fe81-4940-96d1-3bfd8b468237-image.png",
"https://i.postimg.cc/rwWFzXnV/04e3ac0b-cf98-41c0-82b0-0e08d9fa567a-image.png",
"https://i.postimg.cc/HWRgMv7V/044945bd-11f1-43cf-ab02-dd7669dd1036-image.png",
"https://i.postimg.cc/Pxn6hZLf/02428035-2cf5-42cf-9cce-9144ee54545f-image.png",
"https://i.postimg.cc/mDdFVWGx/02213c74-c1bc-4579-9b43-0a5c45f95d5c-image.png",
"https://i.postimg.cc/Zq2GNCCX/00c4de2f-57f4-40aa-adf6-84017d5dbe38-image.png",
"https://i.postimg.cc/JzVNg8SZ/689b5846-cdfd-4f97-8f3e-7e89f23ade37-image.png",
"https://i.postimg.cc/cCCgK92s/8a609859-14e2-43a9-8726-cf6a200f6a89-image.png"
                    ];
                    avatar.style.backgroundImage = `url(${aiChatbotAvatars[Math.floor(Math.random() * aiChatbotAvatars.length)]})`;
                } else if (botName === 'ResponseBot') {
                    const responseBotAvatars = [
                        "https://i.postimg.cc/RVFDhDgk/0e25aaca-17e4-480d-b3b2-65ac292ef87c_image.png",
                        "https://i.postimg.cc/KYn9CSYM/faa10a01-ed73-4283-9f9f-4ad1482994a0_image.png",
                        "https://i.postimg.cc/3R8Z6k6s/6ae0ec87-2bc3-4385-858d-ef9b31f3e164_image.png"
                    ];
                    avatar.style.backgroundImage = `url(${responseBotAvatars[Math.floor(Math.random() * responseBotAvatars.length)]})`;
                } else {
                    const botlarMatiniAvatars = [
                        "https://i.postimg.cc/269nK2nW/1e54101e-2485-4ca9-813a-80c00d007f1e_image.png",
                        "https://i.postimg.cc/vZP9B0SN/6f96372a-f875-42ee-bcd4-89bf115149ba_image.png",
                        "https://i.postimg.cc/j53k465g/2837d0fb-cf0a-41cf-a0e6-7e4c40478e17_image.png",
                        "https://i.postimg.cc/fTSC8qt1/4904af16-943d-4ea4-a9f7-4069639a49fb-image.png",
"https://i.postimg.cc/LsD3Jrwg/5ee8e958-0af0-456f-9cb7-7baf3619d3a8-image.png",
"https://i.postimg.cc/bwHQ57zV/d0efae69-bdba-4790-8123-826771800042-image.png",
"https://i.postimg.cc/NFHXkVJ4/c27ae0e5-480c-4016-8489-43cd650ce0c1-image.png",
"https://i.postimg.cc/Y2Rwn2VL/42d38c0d-ca75-4295-ba7d-80494a524ee5-image.png",
"https://i.postimg.cc/RhKdY0C6/851ca287-7a07-4143-bcf3-662c4a011225-image.png",
"https://i.postimg.cc/Ls5TpD6M/d8d0e86e-07e1-427e-8ba6-3c5ac65f3fbe-image.png",
"https://i.postimg.cc/pTNn6JmC/fb977b8c-f178-4799-80ca-57909b193793-image.png",
"https://i.postimg.cc/hjgtmyJk/0e6436b1-35e0-4ed4-8469-00d4457c2b57-image.png",
"https://i.postimg.cc/CxghXr7z/b75b4c83-a219-4ecf-9a37-31910293d058-image.png",
"https://i.postimg.cc/CKRQNS8D/728f8bb9-1444-4efc-8a4b-ed575d824e1a-image.png",
"https://i.postimg.cc/cCCgK92s/8a609859-14e2-43a9-8726-cf6a200f6a89-image.png",
"https://i.postimg.cc/yYP6qXbj/2ef3ea4b-0389-401c-9704-c87d2e53ffae-image.png",
"https://i.postimg.cc/Bbmzp6mT/824521ca-0c8f-46df-a735-a33cc1b58e14-image.png",
"https://i.postimg.cc/sD08ZMQy/c333892d-c532-43ec-8fe6-b04cc15ffca3-image.png",
"https://i.postimg.cc/V61HcMT9/5abc0aef-8bed-42c1-ac80-e8b647f306bc-image.png",
"https://i.postimg.cc/13qWnJ1c/7ac0b14a-6b45-419c-991a-523b7d25dd33-image.png",
"https://i.postimg.cc/s2PwKxXM/08b8bdb1-fab9-4aa0-951b-b37e2ce09a91-image.png",
"https://i.postimg.cc/HsJzRBnD/9b2a6b42-052d-481a-b691-2a513a938484-image.png",
"https://i.postimg.cc/JzVNg8SZ/689b5846-cdfd-4f97-8f3e-7e89f23ade37-image.png",
"https://i.postimg.cc/W33gr1JL/022e1b0e-8d9d-4270-a0f2-2c09e37f762d-image.png",
"https://i.postimg.cc/vZsPn5YJ/6ba27739-40f8-4108-b555-e082175a6c68-image.png",
"https://i.postimg.cc/5y8B9kC6/43b79420-ae12-4fd2-9c52-79c22b79b9e5-image.png",
"https://i.postimg.cc/R0qwJ0tr/20b09d31-31d4-47cb-bf01-14539e0291d8-image.png",
"https://i.postimg.cc/Wbjr68Zw/af88b22c-62f4-4e53-9182-3f2ad8f73117-image.png",
"https://i.postimg.cc/vZZVCm31/db7929bf-b34f-4db5-962f-f28127261829-image.png",
"https://i.postimg.cc/L5SqD4J8/8a424c6f-b30e-4db2-9af0-837f483508ed-image.png",
"https://i.postimg.cc/wT6ysvKW/b985ffc2-b613-467f-b802-b2d80be782bc-image.png",
"https://i.postimg.cc/RZYN8LW8/Screenshot-20241214-141609-Instagram.jpg",
"https://i.postimg.cc/QxxCdy5w/Screenshot-20240906-104759-Threads.jpg",
"https://i.postimg.cc/PJfXNCLY/906aa0a3-57f7-4883-8dd2-7db89643c387-image.png",
"https://i.postimg.cc/bNJYh2fj/e67ac9ed-ad74-4e0d-a6ef-897bff3c7642-image.png",
"https://i.postimg.cc/cCJW0Pjc/i-2024-12-16-T185201-766.jpg",
"https://i.postimg.cc/dtpFcH98/Screenshot-20241126-090823-Threads.jpg",
"https://i.postimg.cc/ydLqQvd3/Screenshot-20240904-181732-Threads.jpg",
"https://i.postimg.cc/Hxdc4scs/Screenshot-20240905-231116-Threads.jpg",
"https://i.postimg.cc/MKvcYLTR/Screenshot-20240907-151626-Threads.jpg",
"https://i.postimg.cc/xC6CvGVt/Screenshot-20240821-110804-Threads.jpg",
"https://i.postimg.cc/TYLwbW7J/Screenshot-20240904-111955-Threads.jpg",
"https://i.postimg.cc/cJm4W7C0/Screenshot-20240905-225901-Threads.jpg",
"https://i.postimg.cc/HxvYcpbN/Screenshot-20240904-112525-Threads.jpg",
"https://i.postimg.cc/bYMYqwyD/Screenshot-20240907-052226-Threads.jpg",
"https://i.postimg.cc/hGpg6SZG/Screenshot-20240822-070619-Threads.jpg",
"https://i.postimg.cc/8sQVMscZ/Screenshot-20240824-172120-Chrome.jpg",
"https://i.postimg.cc/wBT374S7/Screenshot-20240901-091754-Threads.jpg",
"https://i.postimg.cc/G3st8ySJ/Screenshot-20240907-193946-Threads.jpg",
"https://i.postimg.cc/d0xQDs2x/Screenshot-20240818-130340-Threads.jpg",
"https://i.postimg.cc/kGx7jWk0/Screenshot-20240819-145653-Threads.jpg",
"https://i.postimg.cc/HnCg7VVB/Screenshot-20240907-163145-Threads.jpg",
"https://i.postimg.cc/wjbYQW1t/Screenshot-20240819-082700-Threads.jpg",
"https://i.postimg.cc/yYvM7fXf/d92f542a-1368-4232-8ab8-a00e66986d70-image.png",
"https://i.postimg.cc/xdbhy9r7/Screenshot-20240913-130140-Threads.jpg",
"https://i.postimg.cc/tJDMCTP1/Screenshot-20240829-145810-Chrome.jpg",
"https://i.postimg.cc/mrMp1VCW/Screenshot-20240827-125211-Threads.jpg",
"https://i.postimg.cc/KzD9Jz09/Screenshot-20240816-021518-Threads.jpg",
"https://i.postimg.cc/xT46sBPS/e0bba6a5-5c53-4673-9b97-e0d9eaa356b6-image.png",
"https://i.postimg.cc/gJmsXpG3/Screenshot-20240819-114334-Threads.jpg",
"https://i.postimg.cc/90NYnqZB/Screenshot-20240817-133528-Threads.jpg",
"https://i.postimg.cc/9fjtK2Rs/Screenshot-20240816-132041-Threads.jpg",
"https://i.postimg.cc/pTsfmnGt/Screenshot-20240817-053138-Threads.jpg",
"https://i.postimg.cc/Nf312t4L/6b1b077d-4ad6-44eb-b3fb-a87ace55ff34-image.png",
"https://i.postimg.cc/j53fxY2x/Screenshot-20240904-201944-Instagram.jpg",
"https://i.postimg.cc/g2y6wZjB/Screenshot-20240924-230955-Threads.jpg",
"https://i.postimg.cc/BvqP2n1Z/Screenshot-20240826-194728-Chrome.jpg",
"https://i.postimg.cc/KzWKX7p4/fe0852b6-e763-4daa-9350-84555c8b370c-image.png",
"https://i.postimg.cc/fTmvKkkY/Screenshot-20240814-110338-Threads.jpg",
"https://i.postimg.cc/HLZ0xyP1/Screenshot-20240813-103309-Threads.jpg",
"https://i.postimg.cc/jd0HLKv2/Screenshot-20240905-160655-Chrome.jpg",
"https://i.postimg.cc/kGrb6FQz/0405daa9-780a-4d0f-ab1a-fe37f41c01df-image.png",
"https://i.postimg.cc/tgw1wtMJ/OOHp9-Jothi-Q.jpg",
"https://i.postimg.cc/4dqW4xJP/ZpAY_eglKFA.jpg",
"https://i.postimg.cc/c4NcFj6v/YS7oSJjBa2A.jpg",
"https://i.postimg.cc/2S79dYwj/Yfn7uYIixk4.jpg",
"https://i.postimg.cc/m2bHzGty/x_1d395d09.jpg",
"https://i.postimg.cc/02BykgmQ/XAzkeEABR7Y.jpg",
"https://i.postimg.cc/k5DNVPYp/x-P8A0ForG0.jpg",
"https://i.postimg.cc/9fz0Pmhy/vU_LuXgwdMI.jpg",
"https://i.postimg.cc/rFJwv0yS/TH3EVH4dVgI.jpg",
"https://i.postimg.cc/cCLbCbY1/SmJhJ8p2xE4.jpg",
"https://i.postimg.cc/xCCvzDsZ/rTXLoMANsd0.jpg",
"https://i.postimg.cc/9XskCJ02/QtlfVAhkEt4.jpg",
"https://i.postimg.cc/Xqx6D5Kq/QP_n4s6-3y0.jpg",
"https://i.postimg.cc/vBrsfkcW/QovNcz4hM1M.jpg",
"https://i.postimg.cc/Hnb9p0vW/oydt228thf.jpg",
"https://i.postimg.cc/j50TWtdx/OrDHQP2BoE0.jpg",
"https://i.postimg.cc/BZ26B7d7/nk9c9BVjeis.jpg",
"https://i.postimg.cc/5tv0KPXt/NBgxjOAcHtI.jpg",
"https://i.postimg.cc/wv7Wdmd3/M2TXQ6dluRI.jpg",
"https://i.postimg.cc/rwRFzhC9/k84AmPyEB5Q.jpg",
"https://i.postimg.cc/XvT5pGCr/IMG_0932.jpg",
"https://i.postimg.cc/7ZZZDHbj/IKhDu0gvO04.jpg",
"https://i.postimg.cc/7ZRGWGXK/IcEPYCtitno.jpg",
"https://i.postimg.cc/zG2XGsgv/i_-_2024-12-18T020644.719.jpg",
"https://i.postimg.cc/VN3fjX4c/i_-_2024-12-18T020640.227.jpg",
"https://i.postimg.cc/bJkzLdFS/i_-_2024-12-18T020633.566.jpg",
"https://i.postimg.cc/XYGt9mPp/i_-_2024-12-18T015900.896.jpg",
"https://i.postimg.cc/zfTMcW8N/i_-_2024-12-18T015758.856.jpg",
"https://i.postimg.cc/6pkgczsz/i_-_2024-12-18T015754.624.jpg",
"https://i.postimg.cc/SsrPyhnt/i_-_2024-12-18T015749.885.jpg",
"https://i.postimg.cc/WzYfkw6G/i_-_2024-12-18T015737.403.jpg",
"https://i.postimg.cc/W4mWnvwb/i_-_2024-12-18T015602.512.jpg",
"https://i.postimg.cc/ZRTfsMwP/i_-_2024-12-18T015521.506.jpg",
"https://i.postimg.cc/j5ZMp41p/i_-_2024-12-18T015516.641.jpg",
"https://i.postimg.cc/sxxTsZdv/i_-_2024-12-18T015508.512.jpg",
"https://i.postimg.cc/VsZ744nM/i_-_2024-12-18T015451.913.jpg",
"https://i.postimg.cc/rFdfHWNH/i_-_2024-12-18T015446.324.jpg",
"https://i.postimg.cc/Qd1083Pk/i_-_2024-12-18T015423.034.jpg",
"https://i.postimg.cc/zfNp3QYm/i_-_2024-12-18T015413.385.jpg",
"https://i.postimg.cc/tTC5NVg2/i_-_2024-12-18T015407.024.jpg",
"https://i.postimg.cc/zvyF9ZKh/i_-_2024-12-18T015355.878.jpg",
"https://i.postimg.cc/Y0Tz7nzs/i_-_2024-12-18T015351.099.jpg",
"https://i.postimg.cc/ryHJ5s2N/i_-_2024-12-18T015347.166.jpg",
"https://i.postimg.cc/MKjY5wW2/i_-_2024-12-18T015340.718.jpg",
"https://i.postimg.cc/8zQmnY5F/i_-_2024-12-18T015331.973.jpg",
"https://i.postimg.cc/9QdY3BRL/i_-_2024-12-18T015322.526.jpg",
"https://i.postimg.cc/jjRQRJyt/i_-_2024-12-18T015310.420.jpg",
"https://i.postimg.cc/tgDdJCzP/i_-_2024-12-18T015306.099.jpg",
"https://i.postimg.cc/9XDk6vW1/i_-_2024-12-18T015219.582.jpg",
"https://i.postimg.cc/8zSnrcLn/i_-_2024-12-18T015202.715.jpg",
"https://i.postimg.cc/tgRS2cS3/i_-_2024-12-18T015145.740.jpg",
"https://i.postimg.cc/VvtDJPv8/i_-_2024-12-18T015106.547.jpg",
"https://i.postimg.cc/m2xm0kp2/i_-_2024-12-18T015035.476.jpg",
"https://i.postimg.cc/SxdV2rSJ/i_-_2024-12-18T015018.329.jpg",
"https://i.postimg.cc/tgf3WvLC/i_-_2024-12-18T014736.795.jpg",
"https://i.postimg.cc/xTRLt1WZ/i_-_2024-12-18T014709.658.jpg",
"https://i.postimg.cc/GtPv0L9H/i_-_2024-12-18T014659.196.jpg",
"https://i.postimg.cc/25qvkFVp/i_(7).jpg",
"https://i.postimg.cc/0yyD3qvy/i_(4).jpg",
"https://i.postimg.cc/7hBYJdWK/i_(31).jpg",
"https://i.postimg.cc/QtJMhHkG/i_(27).jpg",
"https://i.postimg.cc/C50fs3JY/i_(2).jpg",
"https://i.postimg.cc/fy5kjJJj/i_(16).jpg",
"https://i.postimg.cc/76027H3m/i_(1).jpg",
"https://i.postimg.cc/fyvS28gd/i.jpg",
"https://i.postimg.cc/D078Xqyw/H_CZRNBRktc.jpg",
"https://i.postimg.cc/y63fQcPb/GxoHhOhF0hc.jpg",
"https://i.postimg.cc/fySY87Qj/goa380-L8xA.jpg",
"https://i.postimg.cc/J4mh6c8r/FcTrAgFzbec.jpg",
"https://i.postimg.cc/Z5Q4S6Gy/dtjwJZLer4k.jpg",
"https://i.postimg.cc/ZKTTFbP0/DO87jHZAiJM.jpg",
"https://i.postimg.cc/FzXKQ0Jx/cmS8YWmeF5k.jpg",
"https://i.postimg.cc/vHDKdCb3/Cl-zZuiXHSs.jpg",
"https://i.postimg.cc/FR4KMjSV/channels4_profile.jpg",
"https://i.postimg.cc/GpngG2Y5/BUe-pCW2D08.jpg",
"https://i.postimg.cc/gcyh20k0/aw-Qnwo-HCPm-M.jpg",
"https://i.postimg.cc/VsFw6yyw/ads-62167909afb6d.jpg",
"https://i.postimg.cc/k583PzNk/a3edae79483ed181b5042454b933d4eb387-1.jpg",
"https://i.postimg.cc/Y2NrWGWJ/7lnnp-GCGk6o.jpg",
"https://i.postimg.cc/rw7sJ6Fb/7ff9b1c75d1a76a75b6d996f527c.jpg",
"https://i.postimg.cc/nhXMBVZB/777330482cb16f08a7d2073929df.jpg",
"https://i.postimg.cc/8kbFVntJ/74aabd39ffa71e868af1de0c590c.jpg",
"https://i.postimg.cc/Mp6mSQ7x/743e868281e999728bb34ec2a4bb6fdd.jpg",
"https://i.postimg.cc/bNH9WT23/7.png",
"https://i.postimg.cc/1Rvd2yh8/6bhowifm6-Vo.jpg",
"https://i.postimg.cc/gc3VLD4m/42d8fd77314da0d87001f9f0619ec25b.jpg",
"https://i.postimg.cc/5tH9YsB3/3-Wwe-X45-LBvg.jpg",
"https://i.postimg.cc/9Q0CKLnh/3d6ad5fe796d54bfb59eaad2b1ac.jpg",
"https://i.postimg.cc/02WbzKg9/37c834dd90220ede5bc3b7b895da.jpg",
"https://i.postimg.cc/3r9wq0x2/3001745870.jpg",
"https://i.postimg.cc/c6qw2Ksq/2-Rkf-E7wtz-X4.jpg",
"https://i.postimg.cc/0QBpGWFy/2927175698.jpg",
"https://i.postimg.cc/Pr2dSgKy/2771113493.jpg",
"https://i.postimg.cc/Pxwm4zjb/2168065081-square-large.jpg",
"https://i.postimg.cc/SsFXmBB8/2144094003-huge.jpg",
"https://i.postimg.cc/GhY52GTy/2117487342-square-large.jpg",
"https://i.postimg.cc/sX9kvWNm/2116353094-huge.jpg",
"https://i.postimg.cc/CLK3xzHC/2116219069-square-large.jpg",
"https://i.postimg.cc/0jC9RFv8/2105213396-huge.jpg",
"https://i.postimg.cc/D0fwZnBW/2097411304-huge.jpg",
"https://i.postimg.cc/VLGcqjLH/2096169811-huge.jpg",
"https://i.postimg.cc/wMqSJvKp/2083076650-huge.jpg",
"https://i.postimg.cc/vBsRYh3D/2076003312-huge.jpg",
"https://i.postimg.cc/x1XVtcXj/2072500117-square.jpg",
"https://i.postimg.cc/SKKdWMRV/2062153155-square-large.jpg",
"https://i.postimg.cc/4NFr7sBD/2062086715-square-large.jpg",
"https://i.postimg.cc/9FFhwxV7/2043780325-huge.jpg",
"https://i.postimg.cc/Hn6FtgH7/2025559368-square-large.jpg",
"https://i.postimg.cc/FFGtvjcs/2021471389-square-large.jpg",
"https://i.postimg.cc/J4PBjdXV/2.jpg",
"https://i.postimg.cc/P5VYnFfz/1963182884-huge.jpg",
"https://i.postimg.cc/htcptwqk/1897138427-square-large.jpg",
"https://i.postimg.cc/brPq58KC/1873909416-huge.jpg",
"https://i.postimg.cc/L6zxRSGk/1843350013-square-large.jpg",
"https://i.postimg.cc/sXQJLCph/1812577004-huge.jpg",
"https://i.postimg.cc/43F5wxhG/1812576986-huge.jpg",
"https://i.postimg.cc/vBJvF2zS/1812576980-huge.jpg",
"https://i.postimg.cc/RZHbWf3t/1808111153-huge.jpg",
"https://i.postimg.cc/VLTVs4N1/112540913-800x600.jpg",
"https://i.postimg.cc/YSmkqh7D/l7hbbk-jho.jpg"
                    ];
                    avatar.style.backgroundImage = `url(${botlarMatiniAvatars[Math.floor(Math.random() * botlarMatiniAvatars.length)]})`;
                }
                messageDiv.appendChild(avatar);
            }

            const content = document.createElement('div');
            content.className = 'message-content';
            
            if (imageUrl) {
                const img = document.createElement('img');
                img.src = imageUrl;
                img.alt = "Sent image";
                img.style.maxWidth = '140px';
                img.style.borderRadius = '10px';
                img.style.marginBottom = '5px';
                content.appendChild(img);
            }
            
            const textNode = document.createElement('p');
            textNode.textContent = text;
            content.appendChild(textNode);
            
            messageDiv.appendChild(content);
            container.appendChild(messageDiv);
            
            if (!isScrollPaused) {
                container.scrollTop = container.scrollHeight;
            }

            if (!isUser) {
                showNotification("Yangi xabar keldi");
            }
        }

        let notificationCount = 0;
        const notificationElement = document.getElementById('notification');
        const notificationCounterElement = document.getElementById('notificationCounter');

        function showNotification(message) {
            notificationElement.textContent = message;
            notificationElement.classList.add('show');
            notificationCount++;
            updateNotificationCounter();

            setTimeout(() => {
                notificationElement.classList.remove('show');
                setTimeout(() => {
                    notificationCount--;
                    updateNotificationCounter();
                }, 2500);
            }, 3000);
        }

        function updateNotificationCounter() {
            notificationCounterElement.textContent = notificationCount;
            if (notificationCount > 0) {
                notificationCounterElement.classList.add('show');
            } else {
                notificationCounterElement.classList.remove('show');
            }
        }

        class Bot {
            constructor(messages, container, interval) {
                this.messages = messages;
                this.container = container;
                this.interval = interval;
            }

            start() {
                setInterval(() => {
                    const randomMessage = this.messages[Math.floor(Math.random() * this.messages.length)];
                    addMessage(this.container, randomMessage, false, this.constructor.name);
                }, this.interval);
            }
        }

        class ResponseBot {
            constructor(container) {
                this.container = container;
                this.responses = {
                    'salom': 'Salom xush kelib siz',
                    'assalomu aliykum': 'Va aliykum salom',
                    'qizlar bormi': 'Qizlar yoq',
                    'kim bor': 'Kim kirak sizga',
                    'qalaysiz': 'Yaxshi, o\'zingiz qalaysiz?',
                    'nima gap': 'Tinchlik, o\'zingizda nima gaplar?',
                    'rahmat': 'Arzimaydi, xizmatingizga tayyormiz',
                    'xayr': 'Xayr, yaxshi qoling',
                };
            }

            respond(message) {
                const lowercaseMessage = message.toLowerCase();
                for (const [key, value] of Object.entries(this.responses)) {
                    if (lowercaseMessage.includes(key)) {
                        setTimeout(() => {
                            addMessage(this.container, value, false, this.constructor.name);
                        }, 2500);
                        return;
                    }
                }
                setTimeout(() => {
                    addMessage(this.container, "Hop", false, this.constructor.name);
                }, 10000);
            }
        }

        class NazoratchiBot {
            constructor(container) {
                this.container = container;
                this.warnings = [
                    "Kichrasiz telefon raqam yozmang spam bo'lasiz",
                    "Men chatni nazorat qilaman shaxsiy ma'lumotlar uzatish taqiqlanadi",
                    "Iltimos foydalanuvchi chatga shaxsiy ma'lumotlarni tarqatmang"
                ];
            }

            checkMessage(message) {
                const phoneRegex = /\b\d{9,12}\b/;
                if (phoneRegex.test(message)) {
                    const warning = this.warnings[Math.floor(Math.random() * this.warnings.length)];
                    setTimeout(() => {
                        addMessage(this.container, warning, false, this.constructor.name);
                    }, 6000);
                }
            }
        }

        class RasmBot {
            constructor(container) {
                this.container = container;
                this.responses = [
                    "Voy buncha chiroyli siz",
                    "Bu sizning rasmingizmi",
                    "Rostan bu sizmi",
                    "Bu sizmi yaxshi yigit"
                ];
            }

            respond() {
                const randomResponse = this.responses[Math.floor(Math.random() * this.responses.length)];
                setTimeout(() => {
                    addMessage(this.container, randomResponse, false, this.constructor.name);
                }, 3500);
            }
        }

        class RasmlinkBot {
            constructor(container) {
                this.container = container;
                this.images = [
                    "https://i.postimg.cc/4dqW4xJP/ZpAY_eglKFA.jpg",
"https://i.postimg.cc/c4NcFj6v/YS7oSJjBa2A.jpg",
"https://i.postimg.cc/2S79dYwj/Yfn7uYIixk4.jpg",
"https://i.postimg.cc/m2bHzGty/x_1d395d09.jpg",
"https://i.postimg.cc/02BykgmQ/XAzkeEABR7Y.jpg",
"https://i.postimg.cc/k5DNVPYp/x-P8A0ForG0.jpg",
"https://i.postimg.cc/9fz0Pmhy/vU_LuXgwdMI.jpg",
"https://i.postimg.cc/rFJwv0yS/TH3EVH4dVgI.jpg",
"https://i.postimg.cc/cCLbCbY1/SmJhJ8p2xE4.jpg",
"https://i.postimg.cc/xCCvzDsZ/rTXLoMANsd0.jpg",
"https://i.postimg.cc/9XskCJ02/QtlfVAhkEt4.jpg",
"https://i.postimg.cc/Xqx6D5Kq/QP_n4s6-3y0.jpg",
"https://i.postimg.cc/vBrsfkcW/QovNcz4hM1M.jpg",
"https://i.postimg.cc/Hnb9p0vW/oydt228thf.jpg",
"https://i.postimg.cc/j50TWtdx/OrDHQP2BoE0.jpg",
"https://i.postimg.cc/BZ26B7d7/nk9c9BVjeis.jpg",
"https://i.postimg.cc/5tv0KPXt/NBgxjOAcHtI.jpg",
"https://i.postimg.cc/wv7Wdmd3/M2TXQ6dluRI.jpg",
"https://i.postimg.cc/rwRFzhC9/k84AmPyEB5Q.jpg",
"https://i.postimg.cc/XvT5pGCr/IMG_0932.jpg",
"https://i.postimg.cc/7ZZZDHbj/IKhDu0gvO04.jpg",
"https://i.postimg.cc/7ZRGWGXK/IcEPYCtitno.jpg",
"https://i.postimg.cc/zG2XGsgv/i_-_2024-12-18T020644.719.jpg",
"https://i.postimg.cc/VN3fjX4c/i_-_2024-12-18T020640.227.jpg",
"https://i.postimg.cc/bJkzLdFS/i_-_2024-12-18T020633.566.jpg",
"https://i.postimg.cc/XYGt9mPp/i_-_2024-12-18T015900.896.jpg",
"https://i.postimg.cc/zfTMcW8N/i_-_2024-12-18T015758.856.jpg",
"https://i.postimg.cc/6pkgczsz/i_-_2024-12-18T015754.624.jpg",
"https://i.postimg.cc/SsrPyhnt/i_-_2024-12-18T015749.885.jpg",
"https://i.postimg.cc/WzYfkw6G/i_-_2024-12-18T015737.403.jpg",
"https://i.postimg.cc/W4mWnvwb/i_-_2024-12-18T015602.512.jpg",
"https://i.postimg.cc/ZRTfsMwP/i_-_2024-12-18T015521.506.jpg",
"https://i.postimg.cc/j5ZMp41p/i_-_2024-12-18T015516.641.jpg",
"https://i.postimg.cc/sxxTsZdv/i_-_2024-12-18T015508.512.jpg",
"https://i.postimg.cc/VsZ744nM/i_-_2024-12-18T015451.913.jpg",
"https://i.postimg.cc/rFdfHWNH/i_-_2024-12-18T015446.324.jpg",
"https://i.postimg.cc/Qd1083Pk/i_-_2024-12-18T015423.034.jpg",
"https://i.postimg.cc/zfNp3QYm/i_-_2024-12-18T015413.385.jpg",
"https://i.postimg.cc/tTC5NVg2/i_-_2024-12-18T015407.024.jpg",
"https://i.postimg.cc/zvyF9ZKh/i_-_2024-12-18T015355.878.jpg",
"https://i.postimg.cc/Y0Tz7nzs/i_-_2024-12-18T015351.099.jpg",
"https://i.postimg.cc/ryHJ5s2N/i_-_2024-12-18T015347.166.jpg",
"https://i.postimg.cc/MKjY5wW2/i_-_2024-12-18T015340.718.jpg",
"https://i.postimg.cc/8zQmnY5F/i_-_2024-12-18T015331.973.jpg",
"https://i.postimg.cc/9QdY3BRL/i_-_2024-12-18T015322.526.jpg",
"https://i.postimg.cc/jjRQRJyt/i_-_2024-12-18T015310.420.jpg",
"https://i.postimg.cc/tgDdJCzP/i_-_2024-12-18T015306.099.jpg",
"https://i.postimg.cc/9XDk6vW1/i_-_2024-12-18T015219.582.jpg",
"https://i.postimg.cc/8zSnrcLn/i_-_2024-12-18T015202.715.jpg",
"https://i.postimg.cc/tgRS2cS3/i_-_2024-12-18T015145.740.jpg",
"https://i.postimg.cc/VvtDJPv8/i_-_2024-12-18T015106.547.jpg",
"https://i.postimg.cc/m2xm0kp2/i_-_2024-12-18T015035.476.jpg",
"https://i.postimg.cc/SxdV2rSJ/i_-_2024-12-18T015018.329.jpg",
"https://i.postimg.cc/tgf3WvLC/i_-_2024-12-18T014736.795.jpg",
"https://i.postimg.cc/xTRLt1WZ/i_-_2024-12-18T014709.658.jpg",
"https://i.postimg.cc/GtPv0L9H/i_-_2024-12-18T014659.196.jpg",
"https://i.postimg.cc/25qvkFVp/i_(7).jpg",
"https://i.postimg.cc/0yyD3qvy/i_(4).jpg",
"https://i.postimg.cc/7hBYJdWK/i_(31).jpg",
"https://i.postimg.cc/QtJMhHkG/i_(27).jpg",
"https://i.postimg.cc/C50fs3JY/i_(2).jpg",
"https://i.postimg.cc/fy5kjJJj/i_(16).jpg",
"https://i.postimg.cc/76027H3m/i_(1).jpg",
"https://i.postimg.cc/fyvS28gd/i.jpg",
"https://i.postimg.cc/D078Xqyw/H_CZRNBRktc.jpg",
"https://i.postimg.cc/y63fQcPb/GxoHhOhF0hc.jpg",
"https://i.postimg.cc/fySY87Qj/goa380-L8xA.jpg",
"https://i.postimg.cc/J4mh6c8r/FcTrAgFzbec.jpg",
"https://i.postimg.cc/Z5Q4S6Gy/dtjwJZLer4k.jpg",
"https://i.postimg.cc/ZKTTFbP0/DO87jHZAiJM.jpg",
"https://i.postimg.cc/FzXKQ0Jx/cmS8YWmeF5k.jpg",
"https://i.postimg.cc/vHDKdCb3/Cl-zZuiXHSs.jpg",
"https://i.postimg.cc/FR4KMjSV/channels4_profile.jpg",
"https://i.postimg.cc/GpngG2Y5/BUe-pCW2D08.jpg",
"https://i.postimg.cc/gcyh20k0/aw-Qnwo-HCPm-M.jpg",
"https://i.postimg.cc/VsFw6yyw/ads-62167909afb6d.jpg",
"https://i.postimg.cc/k583PzNk/a3edae79483ed181b5042454b933d4eb387-1.jpg",
"https://i.postimg.cc/Y2NrWGWJ/7lnnp-GCGk6o.jpg",
"https://i.postimg.cc/rw7sJ6Fb/7ff9b1c75d1a76a75b6d996f527c.jpg",
"https://i.postimg.cc/nhXMBVZB/777330482cb16f08a7d2073929df.jpg",
"https://i.postimg.cc/8kbFVntJ/74aabd39ffa71e868af1de0c590c.jpg",
"https://i.postimg.cc/Mp6mSQ7x/743e868281e999728bb34ec2a4bb6fdd.jpg",
"https://i.postimg.cc/bNH9WT23/7.png",
"https://i.postimg.cc/1Rvd2yh8/6bhowifm6-Vo.jpg",
"https://i.postimg.cc/gc3VLD4m/42d8fd77314da0d87001f9f0619ec25b.jpg",
"https://i.postimg.cc/5tH9YsB3/3-Wwe-X45-LBvg.jpg",
"https://i.postimg.cc/9Q0CKLnh/3d6ad5fe796d54bfb59eaad2b1ac.jpg",
"https://i.postimg.cc/02WbzKg9/37c834dd90220ede5bc3b7b895da.jpg",
"https://i.postimg.cc/3r9wq0x2/3001745870.jpg",
"https://i.postimg.cc/c6qw2Ksq/2-Rkf-E7wtz-X4.jpg",
"https://i.postimg.cc/0QBpGWFy/2927175698.jpg",
"https://i.postimg.cc/Pr2dSgKy/2771113493.jpg",
"https://i.postimg.cc/Pxwm4zjb/2168065081-square-large.jpg",
"https://i.postimg.cc/SsFXmBB8/2144094003-huge.jpg",
"https://i.postimg.cc/GhY52GTy/2117487342-square-large.jpg",
"https://i.postimg.cc/sX9kvWNm/2116353094-huge.jpg",
"https://i.postimg.cc/CLK3xzHC/2116219069-square-large.jpg",
"https://i.postimg.cc/0jC9RFv8/2105213396-huge.jpg",
"https://i.postimg.cc/D0fwZnBW/2097411304-huge.jpg",
"https://i.postimg.cc/VLGcqjLH/2096169811-huge.jpg",
"https://i.postimg.cc/wMqSJvKp/2083076650-huge.jpg",
"https://i.postimg.cc/vBsRYh3D/2076003312-huge.jpg",
"https://i.postimg.cc/x1XVtcXj/2072500117-square.jpg",
"https://i.postimg.cc/SKKdWMRV/2062153155-square-large.jpg",
"https://i.postimg.cc/4NFr7sBD/2062086715-square-large.jpg",
"https://i.postimg.cc/9FFhwxV7/2043780325-huge.jpg",
"https://i.postimg.cc/Hn6FtgH7/2025559368-square-large.jpg",
"https://i.postimg.cc/FFGtvjcs/2021471389-square-large.jpg",
"https://i.postimg.cc/J4PBjdXV/2.jpg",
"https://i.postimg.cc/P5VYnFfz/1963182884-huge.jpg",
"https://i.postimg.cc/htcptwqk/1897138427-square-large.jpg",
"https://i.postimg.cc/brPq58KC/1873909416-huge.jpg",
"https://i.postimg.cc/L6zxRSGk/1843350013-square-large.jpg",
"https://i.postimg.cc/sXQJLCph/1812577004-huge.jpg",
"https://i.postimg.cc/43F5wxhG/1812576986-huge.jpg",
"https://i.postimg.cc/vBJvF2zS/1812576980-huge.jpg",
"https://i.postimg.cc/RZHbWf3t/1808111153-huge.jpg",
"https://i.postimg.cc/VLTVs4N1/112540913-800x600.jpg",
"https://i.postimg.cc/YSmkqh7D/l7hbbk-jho.jpg",
"https://i.postimg.cc/Xq86WB79/0e2dc996-e798-426d-b3be-621a346d41ec-image.png",
"https://i.postimg.cc/RVFDhDgk/0e25aaca-17e4-480d-b3b2-65ac292ef87c_image.png",
"https://i.postimg.cc/CxnrHfTJ/da50d429-d989-4479-8f27-47640284bf72_image.png",
"https://i.postimg.cc/KYn9CSYM/faa10a01-ed73-4283-9f9f-4ad1482994a0_image.png",
"https://i.postimg.cc/152Jt5nF/68dedd04-aa99-49c8-8ef6-b8320c073fc6_image.png",
"https://i.postimg.cc/3R8Z6k6s/6ae0ec87-2bc3-4385-858d-ef9b31f3e164_image.png",
"https://i.postimg.cc/d1ZGgG6S/c4f1d469-fbc8-442c-868d-4cb739a9ef83_image.png",
"https://i.postimg.cc/gkm6HCC7/1ed3f7000d16c581037464d0c666bdde.jpg",
"https://i.postimg.cc/bYHZr6Z9/9d066084-383b-4daa-9062-b158f7054b34_image.png",
"https://i.postimg.cc/HL4qX7XR/062c0617-cc65-4f2e-97fb-88e994de940e_image.png",
"https://i.postimg.cc/pX0mK2NX/Screenshot_20241215_084412_Telegraph.jpg",
"https://i.postimg.cc/LsD3Jrwg/5ee8e958-0af0-456f-9cb7-7baf3619d3a8_image.png",
"https://i.postimg.cc/Y2Rwn2VL/42d38c0d-ca75-4295-ba7d-80494a524ee5_image.png",
"https://i.postimg.cc/Ls5TpD6M/d8d0e86e-07e1-427e-8ba6-3c5ac65f3fbe_image.png",
"https://i.postimg.cc/hjgtmyJk/0e6436b1-35e0-4ed4-8469-00d4457c2b57_image.png",
"https://i.postimg.cc/CxghXr7z/b75b4c83-a219-4ecf-9a37-31910293d058_image.png",
"https://i.postimg.cc/sD08ZMQy/c333892d-c532-43ec-8fe6-b04cc15ffca3_image.png",
"https://i.postimg.cc/13qWnJ1c/7ac0b14a-6b45-419c-991a-523b7d25dd33_image.png",
"https://i.postimg.cc/JzVNg8SZ/689b5846-cdfd-4f97-8f3e-7e89f23ade37_image.png",
"https://i.postimg.cc/63vRz1zY/ef4b4604-7518-42dd-8adb-60d97a74d6ad_image.png",
"https://i.postimg.cc/Wbjr68Zw/af88b22c-62f4-4e53-9182-3f2ad8f73117_image.png",
"https://i.postimg.cc/L5SqD4J8/8a424c6f-b30e-4db2-9af0-837f483508ed_image.png",
"https://i.postimg.cc/wT6ysvKW/b985ffc2-b613-467f-b802-b2d80be782bc_image.png",
"https://i.postimg.cc/PJfXNCLY/906aa0a3-57f7-4883-8dd2-7db89643c387_image.png",
"https://i.postimg.cc/xC6CvGVt/Screenshot_20240821_110804_Threads.jpg",
"https://i.postimg.cc/TYLwbW7J/Screenshot_20240904_111955_Threads.jpg",
"https://i.postimg.cc/wBT374S7/Screenshot_20240901_091754_Threads.jpg",
"https://i.postimg.cc/d0xQDs2x/Screenshot_20240818_130340_Threads.jpg",
"https://i.postimg.cc/kGx7jWk0/Screenshot_20240819_145653_Threads.jpg",
"https://i.postimg.cc/yYvM7fXf/d92f542a-1368-4232-8ab8-a00e66986d70_image.png",
"https://i.postimg.cc/9fjtK2Rs/Screenshot_20240816_132041_Threads.jpg",
"https://i.postimg.cc/pTsfmnGt/Screenshot_20240817_053138_Threads.jpg",
"https://i.postimg.cc/fTmvKkkY/Screenshot_20240814_110338_Threads.jpg",
"https://i.postimg.cc/kGrb6FQz/0405daa9-780a-4d0f-ab1a-fe37f41c01df_image.png",
"https://i.postimg.cc/GprgYGQB/6f96372a-f875-42ee-bcd4-89bf115149ba-image.png",
"https://i.postimg.cc/FKZWxzWT/Screenshot-20240821-185911-Threads.jpg",
"https://i.postimg.cc/wvjW4zng/Screenshot-20240827-125954-Threads.jpg",
"https://i.postimg.cc/GtZqpytm/Screenshot-20240822-070602-Threads.jpg",
"https://i.postimg.cc/rp8gzcVx/Screenshot-20240819-114043-Threads.jpg",
"https://i.postimg.cc/t7QNbGv1/cb378dab-86f7-4b40-adaf-e84bfbd62f00-image.png",
"https://i.postimg.cc/44rDyKrc/93917ca8-e3c3-49e6-afae-c25a74f3e676-image.png",
"https://i.postimg.cc/LsC7phtn/8813e81b-7d8d-4eff-a607-7ee1f9a045b0-image.png",
"https://i.postimg.cc/5yvkL3ZC/Screenshot-20240906-213925-Threads.jpg",
"https://i.postimg.cc/66GPkWyp/Screenshot-20241001-131235-Threads.jpg",
"https://i.postimg.cc/SxmtYcVn/Screenshot-20240905-034541-Threads.jpg",
"https://i.postimg.cc/15rvSfPs/c62b6dea-540d-4143-a636-fffe31040a91-image.png",
"https://i.postimg.cc/hGfsVsmt/eba09edd-c1d4-4e1a-86e5-52a910703d03-image.png",
"https://i.postimg.cc/prtBbt6m/7bf49cfa-b6ef-4038-a238-b919aab5edb7-image.png",
"https://i.postimg.cc/kg5vdsfv/17e65cde-2459-4b74-a6ef-f636d103bdd8-image.png",
"https://i.postimg.cc/LsctLpRx/bfaae242-1bea-4eb4-99ce-20980445deed-image.png",
"https://i.postimg.cc/LXPr32P5/fed6a9d2-5333-4406-8297-f972a2c1805f_image.png",
"https://i.postimg.cc/L8NRJ9kM/fd3e4dbd-0e31-4a10-bce7-b3aac0bad885_image.png",
"https://i.postimg.cc/65qfkzHL/f14b6f64-06dc-4717-818a-17a3eedc83d2_image.png",
"https://i.postimg.cc/W4vpkWCM/eb265036-27bd-4d57-8b19-9e7f04d4676c_image.png",
"https://i.postimg.cc/cJSYLccz/ea6caa9b-ed75-4030-9632-b84553873e41_image.png",
"https://i.postimg.cc/rsKqkvRL/e91ec9d6-bb0c-43ba-ba3f-aad2442a976f_image.png",
"https://i.postimg.cc/wTrQgJZK/e5fe4ab3-c428-4772-976a-b9c26c62ee58_image.png",
"https://i.postimg.cc/rmg5btxP/e5ce4602-5557-48b9-ad31-4e7a70729ea6_image.png",
"https://i.postimg.cc/Xvd82JsR/e0d93014-19e6-4175-9511-e7f7d840e80d_image.png",
"https://i.postimg.cc/j5ThBb9L/ded52d4e-fdfb-4b8b-bea9-76accb712914_image.png",
"https://i.postimg.cc/DfX2xKhq/ddee6225-3e9a-46b1-8496-403fd8526983_image.png",
"https://i.postimg.cc/SxK3tW9w/da152d64-3d24-4a18-95da-c19c18571c5f_image.png",
"https://i.postimg.cc/pXs18pSk/d926cac1-6e05-4784-b282-0c5dd630c092_image.png",
"https://i.postimg.cc/XYwGmC0k/d380ca88-11e6-4ff4-8eeb-8915beab70e2_image.png",
"https://i.postimg.cc/XYwGmC0k/d380ca88-11e6-4ff4-8eeb-8915beab70e2_image.png",
"https://i.postimg.cc/Z51HF3xP/d20a6254-ea13-4fb3-95ce-197a89dba8e9_image.png",
"https://i.postimg.cc/B6JxMCLF/d1053e12-46f8-4bda-a036-227b97a61d90_image.png",
"https://i.postimg.cc/7h6SyYNY/d0bcde7f-80a8-4b1f-ad2d-4e1521a990e0_image.png",
"https://i.postimg.cc/t40nBz8g/d0aa2129-6421-4e86-8513-355acbbb549b_image.png",
"https://i.postimg.cc/SKPhGgtT/ce09e161-0ad2-4af6-9a21-1a2baf6a67c4_image.png",
"https://i.postimg.cc/SKPhGgtT/ce09e161-0ad2-4af6-9a21-1a2baf6a67c4_image.png",
"https://i.postimg.cc/V63zzKqr/c512105c-d41d-46a5-bedc-7e0d50404787_image.png",
"https://i.postimg.cc/J4xSqTsN/c298d597-a51a-42df-9e23-6b34e08956bb_image.png",
"https://i.postimg.cc/T1FfYCn5/c0d690ba-bb6b-4f82-bfbc-749ff9f56529_image.png",
"https://i.postimg.cc/JhzrxD7n/bfe3564a-53b8-4ffd-b241-9a23fa6d2887_image.png",
"https://i.postimg.cc/sxqGdPXw/be030da4-70a2-465e-b9e8-3ebf16d3075d_image.png",
"https://i.postimg.cc/hPcHVFt4/bc7e3183-3392-440a-a7ab-6b8815046546_image.png",
"https://i.postimg.cc/htgPJZHV/bb4c5f24-83bc-4379-99ab-a0412b0a25a0_image.png",
"https://i.postimg.cc/59RCCJ3L/ba261a6a-f88d-4c11-baa6-521364a582ea_image.png",
"https://i.postimg.cc/NfCpFZyz/b4babdd9-0490-490f-9662-6fe21114f992_image.png",
"https://i.postimg.cc/XJNCw7mc/af7550b9-f493-4dc2-b9e9-a081ec0c20e9_image.png",
"https://i.postimg.cc/kGtLw9tD/a83de5d0-6d29-4f26-b154-cb6357565598_image.png",
"https://i.postimg.cc/yYh7zXkx/a6fea91b-cc24-4e0e-a0ca-99d64c6c6bd9_image.png",
"https://i.postimg.cc/tgkbVXhj/a6ce71dd-6a67-45fe-888d-47636ad32af9_image.png",
"https://i.postimg.cc/nLSHPFM1/a13c7be0-b90d-4a35-8932-89d0e50fed2c_image.png",
"https://i.postimg.cc/4xNRkDD2/9e43925f-75aa-4b04-ab09-cbe03743794e_image.png",
"https://i.postimg.cc/NM8d0MT6/9e282350-f73c-44f2-89ea-b7935bb40349_image.png",
"https://i.postimg.cc/rmhq78mJ/9802567a-2779-49a7-a7fc-753a34777d12_image.png",
"https://i.postimg.cc/9FmnrGLr/9605b7ef-869d-467f-81f4-141bd6ee99a1_image.png",
"https://i.postimg.cc/6pjJ9HwW/92b97406-aeb8-4743-bd62-402f8b348298_image.png",
"https://i.postimg.cc/RZbyrNQq/8a8c49be-6951-462c-85d2-cc8168d4f2d6_image.png",
"https://i.postimg.cc/RVwZZxbM/87c7abaa-703b-41d7-8720-b2410bafcc8e_image.png",
"https://i.postimg.cc/BvS93dRw/86658ba2-1f0b-41e2-a261-9678b5268c15_image.png",
"https://i.postimg.cc/Xv4GbYjS/86656fe8-d082-4ef8-abe2-d27cdd560657_image.png",
"https://i.postimg.cc/y8WpT74K/7e20ca80-fc08-4c57-9b35-1ee7258ee60b_image.png",
"https://i.postimg.cc/Gh6GZRTd/7a7de9e6-292d-4a46-aa54-455806ed8013_image.png",
"https://i.postimg.cc/tTRXr1XJ/79b82f9f-6839-4086-b07e-959d1c33c13d_image.png",
"https://i.postimg.cc/FKYt1jsj/767f6485-1dad-4956-bf35-f423af87bbf4_image.png",
"https://i.postimg.cc/htr4VbB6/7529667d-c306-45a0-ab4f-b891179ba324_image.png",
"https://i.postimg.cc/fR3595mT/6d77ccfc-7a42-49a4-8091-8a1ccb0815e2_image.png",
"https://i.postimg.cc/HsMC90Q3/6a3e37bb-3f6d-4c4a-ae77-3d369eb5793c_image.png",
"https://i.postimg.cc/bwQpp0rd/68b3b09c-9133-49cf-a0f6-220ad95a1bc0-image.png",
"https://i.postimg.cc/XJvbfT8y/68ae74e3-d7dd-474e-aa95-11bb65e1e0d3-image.png",
"https://i.postimg.cc/sXZRH5kV/650b4e09-3ff9-4bd3-ab97-9f2666eebbb6-image.png",
"https://i.postimg.cc/mkGKdJ3w/63ed3e83-b991-421b-b2fd-de4ad54da29a-image.png",
"https://i.postimg.cc/j52pwyxH/63cfc56f-44c1-46a1-bc0e-c2c9a270a2fa-image.png",
"https://i.postimg.cc/kgtF4GP2/63b26158-e97b-4340-8d8e-1bfdd0ecfefb-image.png",
"https://i.postimg.cc/NMPwppJC/63ac7722-09db-450e-9e71-5707add448a6-image.png",
"https://i.postimg.cc/Znp4n6Hf/60b70996-f621-4cdc-8e35-4e9e0b7baea6-image.png",
"https://i.postimg.cc/zDtnFKJL/5f6c7e5b-3bd0-4ecd-8822-28bbe8bbfe88-image.png",
"https://i.postimg.cc/257WbBcS/5ed0e403-c0ab-4367-b3a2-9c02eaab4bf5-image.png",
"https://i.postimg.cc/90WJwhtv/586d212d-4eba-4653-87b5-917a167d37b3-image.png",
"https://i.postimg.cc/4dpShwCh/57138345-4a41-4036-9bca-28b4449c57a1-image.png",
"https://i.postimg.cc/vT3XWN0D/5660bb77-c08d-4650-b44a-34e0c211e7d8-image.png",
"https://i.postimg.cc/wTRs5rfP/53da4348-f26e-401c-b94b-f5782a71f977-image.png",
"https://i.postimg.cc/Y23XKvtk/4f6c5bd4-b1c6-45ff-a4b4-ecbc8ebe740e-image.png",
"https://i.postimg.cc/3wvLP9xb/4a3dbb6a-16ca-4738-8575-9ad08394b791-image.png",
"https://i.postimg.cc/QxFc4Ctf/48e1c0c3-a0eb-4a72-8dec-1f3963c6c788-image.png",
"https://i.postimg.cc/yxYyYT7K/48b9f95d-d1e3-45a1-9e76-171681bd8b34-image.png",
"https://i.postimg.cc/tJZGfW8q/4445d1db-89e3-4a5b-bcbe-00535577ecc5-image.png",
"https://i.postimg.cc/Kc6Yb8fq/41856986-0847-4c72-bc55-75a54c3cd7b6-image.png",
"https://i.postimg.cc/Bb9frX32/40ac1175-9194-43d6-abe9-08db4db42b7a-image.png",
"https://i.postimg.cc/3NSCyDwv/3eae55b3-4cf7-4dfd-9f80-f068e7b27c1b-image.png",
"https://i.postimg.cc/jj06JTRZ/3e5eabdc-0b64-4c9a-84d8-fea8fb99862b-image.png",
"https://i.postimg.cc/yNLq8LH6/396dcdf5-4cec-4134-82a5-1d1f7a13ac70-image.png",
"https://i.postimg.cc/wxhCtxHb/3199904b-144c-4a0b-985d-f4e29f5bfa82-image.png",
"https://i.postimg.cc/2SFRPz9Z/2f955612-c2c5-4b6a-986e-471a091a0f04-image.png",
"https://i.postimg.cc/qM6pZHds/2b03e0b7-a8d1-4a62-9106-bc0aea280504-image.png",
"https://i.postimg.cc/L8H24Y1T/2a2f30e5-c5a7-46e4-b782-a51d7fc55345-image.png",
"https://i.postimg.cc/52vLJr8v/243107f4-d4a9-4619-89db-23ccc1aa4197-image.png",
"https://i.postimg.cc/PxMMj7sK/225b0238-abb7-4024-a6ab-732d2a78f3eb-image.png",
"https://i.postimg.cc/0y3WWhPw/1f32b24a-99f1-4ecd-98f8-de8cf1071ce8-image.png",
"https://i.postimg.cc/k50H4zHm/1bef5703-7515-4a8f-8d45-80a8bf6e8b52-image.png",
"https://i.postimg.cc/ncxtTj0J/1627e08b-5e9f-4376-bbed-76cff23bda44-image.png",
"https://i.postimg.cc/tgJbPKDn/149f552d-d6e4-40e8-9aae-d680902cf89b-image.png",
"https://i.postimg.cc/VsVYRL2s/13b61638-5146-41ee-9e18-c49cee4d65aa-image.png",
"https://i.postimg.cc/fWmNxj7C/12184fd4-8edf-4833-929d-e919952dec43-image.png",
"https://i.postimg.cc/2jFtkHFs/0ae385d9-2040-41fe-8f95-60187034f006-image.png",
"https://i.postimg.cc/gcX01ZVL/0760c982-788e-478c-b778-d65f37e99575-image.png",
"https://i.postimg.cc/bNRf5yB2/06976094-cf55-43e0-9f4b-3df6efec44e9-image.png",
"https://i.postimg.cc/6qrxtt6g/05bdf0a0-fe81-4940-96d1-3bfd8b468237-image.png",
"https://i.postimg.cc/rwWFzXnV/04e3ac0b-cf98-41c0-82b0-0e08d9fa567a-image.png",
"https://i.postimg.cc/HWRgMv7V/044945bd-11f1-43cf-ab02-dd7669dd1036-image.png",
"https://i.postimg.cc/Pxn6hZLf/02428035-2cf5-42cf-9cce-9144ee54545f-image.png",
"https://i.postimg.cc/mDdFVWGx/02213c74-c1bc-4579-9b43-0a5c45f95d5c-image.png",
"https://i.postimg.cc/Zq2GNCCX/00c4de2f-57f4-40aa-adf6-84017d5dbe38-image.png",
"https://i.postimg.cc/JzVNg8SZ/689b5846-cdfd-4f97-8f3e-7e89f23ade37-image.png",
"https://i.postimg.cc/cCCgK92s/8a609859-14e2-43a9-8726-cf6a200f6a89-image.png",
"https://i.postimg.cc/fTSC8qt1/4904af16-943d-4ea4-a9f7-4069639a49fb-image.png",
"https://i.postimg.cc/LsD3Jrwg/5ee8e958-0af0-456f-9cb7-7baf3619d3a8-image.png",
"https://i.postimg.cc/bwHQ57zV/d0efae69-bdba-4790-8123-826771800042-image.png",
"https://i.postimg.cc/NFHXkVJ4/c27ae0e5-480c-4016-8489-43cd650ce0c1-image.png",
"https://i.postimg.cc/Y2Rwn2VL/42d38c0d-ca75-4295-ba7d-80494a524ee5-image.png",
"https://i.postimg.cc/RhKdY0C6/851ca287-7a07-4143-bcf3-662c4a011225-image.png",
"https://i.postimg.cc/Ls5TpD6M/d8d0e86e-07e1-427e-8ba6-3c5ac65f3fbe-image.png",
"https://i.postimg.cc/pTNn6JmC/fb977b8c-f178-4799-80ca-57909b193793-image.png",
"https://i.postimg.cc/hjgtmyJk/0e6436b1-35e0-4ed4-8469-00d4457c2b57-image.png",
"https://i.postimg.cc/CxghXr7z/b75b4c83-a219-4ecf-9a37-31910293d058-image.png",
"https://i.postimg.cc/CKRQNS8D/728f8bb9-1444-4efc-8a4b-ed575d824e1a-image.png",
"https://i.postimg.cc/cCCgK92s/8a609859-14e2-43a9-8726-cf6a200f6a89-image.png",
"https://i.postimg.cc/yYP6qXbj/2ef3ea4b-0389-401c-9704-c87d2e53ffae-image.png",
"https://i.postimg.cc/Bbmzp6mT/824521ca-0c8f-46df-a735-a33cc1b58e14-image.png",
"https://i.postimg.cc/sD08ZMQy/c333892d-c532-43ec-8fe6-b04cc15ffca3-image.png",
"https://i.postimg.cc/V61HcMT9/5abc0aef-8bed-42c1-ac80-e8b647f306bc-image.png",
"https://i.postimg.cc/13qWnJ1c/7ac0b14a-6b45-419c-991a-523b7d25dd33-image.png",
"https://i.postimg.cc/s2PwKxXM/08b8bdb1-fab9-4aa0-951b-b37e2ce09a91-image.png",
"https://i.postimg.cc/HsJzRBnD/9b2a6b42-052d-481a-b691-2a513a938484-image.png",
"https://i.postimg.cc/JzVNg8SZ/689b5846-cdfd-4f97-8f3e-7e89f23ade37-image.png",
"https://i.postimg.cc/W33gr1JL/022e1b0e-8d9d-4270-a0f2-2c09e37f762d-image.png",
"https://i.postimg.cc/vZsPn5YJ/6ba27739-40f8-4108-b555-e082175a6c68-image.png",
"https://i.postimg.cc/5y8B9kC6/43b79420-ae12-4fd2-9c52-79c22b79b9e5-image.png",
"https://i.postimg.cc/R0qwJ0tr/20b09d31-31d4-47cb-bf01-14539e0291d8-image.png",
"https://i.postimg.cc/Wbjr68Zw/af88b22c-62f4-4e53-9182-3f2ad8f73117-image.png",
"https://i.postimg.cc/vZZVCm31/db7929bf-b34f-4db5-962f-f28127261829-image.png",
"https://i.postimg.cc/L5SqD4J8/8a424c6f-b30e-4db2-9af0-837f483508ed-image.png",
"https://i.postimg.cc/wT6ysvKW/b985ffc2-b613-467f-b802-b2d80be782bc-image.png",
"https://i.postimg.cc/RZYN8LW8/Screenshot-20241214-141609-Instagram.jpg",
"https://i.postimg.cc/QxxCdy5w/Screenshot-20240906-104759-Threads.jpg",
"https://i.postimg.cc/PJfXNCLY/906aa0a3-57f7-4883-8dd2-7db89643c387-image.png",
"https://i.postimg.cc/bNJYh2fj/e67ac9ed-ad74-4e0d-a6ef-897bff3c7642-image.png",
"https://i.postimg.cc/cCJW0Pjc/i-2024-12-16-T185201-766.jpg",
"https://i.postimg.cc/dtpFcH98/Screenshot-20241126-090823-Threads.jpg",
"https://i.postimg.cc/ydLqQvd3/Screenshot-20240904-181732-Threads.jpg",
"https://i.postimg.cc/Hxdc4scs/Screenshot-20240905-231116-Threads.jpg",
"https://i.postimg.cc/MKvcYLTR/Screenshot-20240907-151626-Threads.jpg",
"https://i.postimg.cc/xC6CvGVt/Screenshot-20240821-110804-Threads.jpg",
"https://i.postimg.cc/TYLwbW7J/Screenshot-20240904-111955-Threads.jpg",
"https://i.postimg.cc/cJm4W7C0/Screenshot-20240905-225901-Threads.jpg",
"https://i.postimg.cc/HxvYcpbN/Screenshot-20240904-112525-Threads.jpg",
"https://i.postimg.cc/bYMYqwyD/Screenshot-20240907-052226-Threads.jpg",
"https://i.postimg.cc/hGpg6SZG/Screenshot-20240822-070619-Threads.jpg",
"https://i.postimg.cc/8sQVMscZ/Screenshot-20240824-172120-Chrome.jpg",
"https://i.postimg.cc/wBT374S7/Screenshot-20240901-091754-Threads.jpg",
"https://i.postimg.cc/G3st8ySJ/Screenshot-20240907-193946-Threads.jpg",
"https://i.postimg.cc/d0xQDs2x/Screenshot-20240818-130340-Threads.jpg",
"https://i.postimg.cc/kGx7jWk0/Screenshot-20240819-145653-Threads.jpg",
"https://i.postimg.cc/HnCg7VVB/Screenshot-20240907-163145-Threads.jpg",
"https://i.postimg.cc/wjbYQW1t/Screenshot-20240819-082700-Threads.jpg",
"https://i.postimg.cc/yYvM7fXf/d92f542a-1368-4232-8ab8-a00e66986d70-image.png",
"https://i.postimg.cc/xdbhy9r7/Screenshot-20240913-130140-Threads.jpg",
"https://i.postimg.cc/tJDMCTP1/Screenshot-20240829-145810-Chrome.jpg",
"https://i.postimg.cc/mrMp1VCW/Screenshot-20240827-125211-Threads.jpg",
"https://i.postimg.cc/KzD9Jz09/Screenshot-20240816-021518-Threads.jpg",
"https://i.postimg.cc/xT46sBPS/e0bba6a5-5c53-4673-9b97-e0d9eaa356b6-image.png",
"https://i.postimg.cc/gJmsXpG3/Screenshot-20240819-114334-Threads.jpg",
"https://i.postimg.cc/90NYnqZB/Screenshot-20240817-133528-Threads.jpg",
"https://i.postimg.cc/9fjtK2Rs/Screenshot-20240816-132041-Threads.jpg",
"https://i.postimg.cc/pTsfmnGt/Screenshot-20240817-053138-Threads.jpg",
"https://i.postimg.cc/Nf312t4L/6b1b077d-4ad6-44eb-b3fb-a87ace55ff34-image.png",
"https://i.postimg.cc/j53fxY2x/Screenshot-20240904-201944-Instagram.jpg",
"https://i.postimg.cc/g2y6wZjB/Screenshot-20240924-230955-Threads.jpg",
"https://i.postimg.cc/BvqP2n1Z/Screenshot-20240826-194728-Chrome.jpg",
"https://i.postimg.cc/KzWKX7p4/fe0852b6-e763-4daa-9350-84555c8b370c-image.png",
"https://i.postimg.cc/fTmvKkkY/Screenshot-20240814-110338-Threads.jpg",
"https://i.postimg.cc/HLZ0xyP1/Screenshot-20240813-103309-Threads.jpg",
"https://i.postimg.cc/jd0HLKv2/Screenshot-20240905-160655-Chrome.jpg",
"https://i.postimg.cc/kGrb6FQz/0405daa9-780a-4d0f-ab1a-fe37f41c01df-image.png",
"https://i.postimg.cc/tgw1wtMJ/OOHp9-Jothi-Q.jpg"
                ];
                this.captions = [
                    "Nomzod Baxtini Kanalimizdan Qidirmoqda",
                    "Xali Baxti topilmadi",
                    "Baxtini Qidirmoqda"
                ];
            }

            start() {
                setInterval(() => {
                    this.sendRandomMessage();
                }, Math.floor(Math.random() * 20000) + 5000);
            }

            sendRandomMessage() {
                const isImage = Math.random() < 0.7;
                if (isImage) {
                    this.sendRandomImage();
                } else {
                    this.sendRandomText();
                }
            }

            sendRandomImage() {
                const randomImageIndex = Math.floor(Math.random() * this.images.length);
                const randomCaptionIndex = Math.floor(Math.random() * this.captions.length);
                const imageUrl = this.images[randomImageIndex];
                const caption = this.captions[randomCaptionIndex];
                
                addMessage(this.container, caption, false, 'RasmlinkBot', imageUrl);
            }

            sendRandomText() {
                const randomCaptionIndex = Math.floor(Math.random() * this.captions.length);
                const text = this.captions[randomCaptionIndex];
                
                addMessage(this.container, text, false, 'RasmlinkBot');
            }
        }

        class AIChatbot {
            constructor(container) {
                this.container = container;
                this.wordDatabase = {};
                this.unknownWords = [];
                this.loadData();
                this.observeChat();
            }

            loadData() {
                const storedWordDatabase = localStorage.getItem('aiWordDatabase');
                const storedUnknownWords = localStorage.getItem('aiUnknownWords');
                
                if (storedWordDatabase) this.wordDatabase = JSON.parse(storedWordDatabase);
                if (storedUnknownWords) this.unknownWords = JSON.parse(storedUnknownWords);
            }

            saveData() {
                localStorage.setItem('aiWordDatabase', JSON.stringify(this.wordDatabase));
                localStorage.setItem('aiUnknownWords', JSON.stringify(this.unknownWords));
            }

            analyzeAndSaveWords(message) {
                const words = message.toLowerCase().split(/\s+/);
                words.forEach((word, index) => {
                    if (!(word in this.wordDatabase)) {
                        if (Math.random() < 0.15) {
                            this.unknownWords.push(word);
                        }
                        this.wordDatabase[word] = { count: 0, connections: {} };
                    }
                    
                    this.wordDatabase[word].count++;
                    
                    if (index > 0) {
                        const prevWord = words[index - 1];
                        this.wordDatabase[word].connections[prevWord] = (this.wordDatabase[word].connections[prevWord] || 0) + 1;
                    }
                });
                this.saveData();
            }

            generateResponse() {
                const allWords = Object.keys(this.wordDatabase);
                if (allWords.length === 0) {
                    return "Men hali so'zlarni o'rganmadim...";
                }
                
                let response = '';
                let currentWord = allWords[Math.floor(Math.random() * allWords.length)];
                
                for (let i = 0; i < 3; i++) {
                    response += currentWord + ' ';
                    
                    const wordData = this.wordDatabase[currentWord];
                    if (wordData && wordData.connections) {
                        const nextWords = Object.keys(wordData.connections);
                        if (nextWords.length > 0) {
                            currentWord = nextWords[Math.floor(Math.random() * nextWords.length)];
                        } else {
                            currentWord = allWords[Math.floor(Math.random() * allWords.length)];
                        }
                    } else {
                        currentWord = allWords[Math.floor(Math.random() * allWords.length)];
                    }
                    
                    if (Math.random() < 0.03  && this.unknownWords.length > 0) {
                        const randomUnknown = this.unknownWords[Math.floor(Math.random() * this.unknownWords.length)];
                        response += randomUnknown + ' ';
                    }
                }
                
                return response.trim();
            }

            respond(message) {
                this.analyzeAndSaveWords(message);
                const response = this.generateResponse();
                setTimeout(() => {
                    addMessage(this.container, response, false, 'AIChatbot');
                }, 4500);
            }

            observeChat() {
                const observer = new MutationObserver((mutations) => {
                    mutations.forEach((mutation) => {
                        if (mutation.type === 'childList') {
                            mutation.addedNodes.forEach((node) => {
                                if (node.nodeType === Node.ELEMENT_NODE && node.classList.contains('message')) {
                                    const messageContent = node.querySelector('.message-content');
                                    if (messageContent && !node.classList.contains('user') && !node.classList.contains('AIChatbot')) {
                                        const botMessage = messageContent.textContent.trim();
                                        this.respond(botMessage);
                                    }
                                }
                            });
                        }
                    });
                });

                observer.observe(this.container, { childList: true, subtree: true });
            }
        }

        const chatContainer = document.getElementById('chatMessages');
        const chatPausedOverlay = chatContainer.querySelector('.chat-paused-overlay');

        function toggleChatPause() {
            isScrollPaused = !isScrollPaused;
            chatPausedOverlay.classList.toggle('visible', isScrollPaused);
            showNotification(isScrollPaused ? "Chat to'xtatildi" : "Chat davom etmoqda");
            
            if (isScrollPaused) {
                const pauseDuration = Math.floor(Math.random() * (20000 - 15000 + 1)) + 15000;
                scrollTimeout = setTimeout(() => {
                    isScrollPaused = false;
                    chatPausedOverlay.classList.remove('visible');
                    chatContainer.scrollTop = chatContainer.scrollHeight;
                    showNotification("Chat davom etmoqda");
                }, pauseDuration);
            } else {
                clearTimeout(scrollTimeout);
            }
        }

        let pressTimer;

        chatContainer.addEventListener('mousedown', () => {
            pressTimer = setTimeout(toggleChatPause, 500);
        });

        chatContainer.addEventListener('mouseup', () => {
            clearTimeout(pressTimer);
        });

        chatContainer.addEventListener('mouseleave', () => {
            clearTimeout(pressTimer);
        });

        chatContainer.addEventListener('touchstart', (e) => {
            pressTimer = setTimeout(toggleChatPause, 500);
        });

        chatContainer.addEventListener('touchend', () => {
            clearTimeout(pressTimer);
        });

        document.getElementById('sendMessage').addEventListener('click', () => {
            const input = document.getElementById('messageInput');
            const text = input.value.trim();
            if (text) {
                addMessage(document.getElementById('chatMessages'), text, true);
                responseBot.respond(text);
                nazoratchiBot.checkMessage(text);
                aiChatbot.respond(text);
                input.value = '';
            }
        });

        document.getElementById('announcementButton').addEventListener('click', () => {
            document.getElementById('announcementForm').style.display = 'block';
        });

        document.getElementById('submitAnnouncement').addEventListener('click', () => {
            const name = document.getElementById('announcementName').value;
            const info = document.getElementById('announcementInfo').value;
            const phone = document.getElementById('announcementPhone').value;
            const imageFile = document.getElementById('announcementImage').files[0];

            if (name && info && phone) {
                if (imageFile) {
                    const reader = new FileReader();
                    reader.onload = (e) => {
                        addAnnouncement(name, info, phone, e.target.result);
                    };
                    reader.readAsDataURL(imageFile);
                } else {
                    addAnnouncement(name, info, phone);
                }

                document.getElementById('announcementForm').style.display = 'none';
                document.getElementById('announcementName').value = '';
                document.getElementById('announcementInfo').value = '';
                document.getElementById('announcementPhone').value = '';
                document.getElementById('announcementImage').value = '';
            } else {
                showNotification("Iltimos, barcha maydonlarni to'ldiring");
            }
        });

        function addAnnouncement(name, info, phone, imageUrl = '') {
            const announcementText = `E'lon: ${name}\n${info}\nTel: ${phone}`;
            addMessage(chatContainer, announcementText, false, 'AnnouncementBot', imageUrl);
        }

        document.getElementById('backButton').addEventListener('click', () => {
            if (linkPage.classList.contains('hidden')) {
                showNotification("Siz asosiy sahifadasiz");
            } else {
                linkPage.classList.add('hidden');
                sovchilarPage.classList.remove('hidden');
            }
        });

        let clickCount = 0;
        const kelingaXabarButton = document.getElementById('kelingaXabar');
        const countdownWindow = document.getElementById('countdownWindow');
        const warningMessage = document.getElementById('warningMessage');

        kelingaXabarButton.addEventListener('click', () => {
            clickCount++;
            if (clickCount >= 2) {
                warningMessage.textContent = "Kechrasiz, tugmani siz ko'p marta bosdingiz. Sahifadan chiqing va kelin nomzodni tanlang va faqat 1 marta tugmani bosing. 2, 3 marta tugmani bosmang.";
                warningMessage.style.color = "red";
                return;
            }

            const data = JSON.parse(localStorage.getItem('botData'));
            const randomUrl = data.httpsManzillar[Math.floor(Math.random() * data.httpsManzillar.length)];
            
            countdownWindow.classList.remove('hidden');
            let countdown = Math.floor(Math.random() * 3) + 1;
            
            const countdownInterval = setInterval(() => {
                countdownWindow.textContent = countdown;
                countdown--;
                
                if (countdown < 0) {
                    clearInterval(countdownInterval);
                    countdownWindow.classList.add('hidden');
                    window.open(randomUrl, '_blank');
                }
            }, 1000);
        });

        const tanishuvBot = new Bot(
            JSON.parse(localStorage.getItem('botData')).botlarMatini,
            document.getElementById('chatMessages'),
            3500
        );
        tanishuvBot.start();

        const rasmlinkBot = new RasmlinkBot(document.getElementById('chatMessages'));
        rasmlinkBot.start();

        document.getElementById('closeAnnouncementForm').addEventListener('click', () => {
            document.getElementById('announcementForm').style.display = 'none';
        });

        const responseBot = new ResponseBot(document.getElementById('chatMessages'));
        const nazoratchiBot = new NazoratchiBot(document.getElementById('chatMessages'));
        const rasmBot = new RasmBot(document.getElementById('chatMessages'));
        const aiChatbot = new AIChatbot(document.getElementById('chatMessages'));

        function startBots() {
            const data = JSON.parse(localStorage.getItem('botData'));
            
            const userBot = new Bot(
                data.botlarMatini,
                document.getElementById('chatMessages'),
                2500
            );
            userBot.start();

            const adminBot = new Bot(
                data.yordamMatinlar,
                document.getElementById('yordamMessages'),
                300000
            );
            adminBot.start();

            const animatedTexts = [
                "Agar siz kelinga yoza olmagan bo'lsangiz unda siz saxifadan chiqib qayta kiring",
                "Kelinga Xabar Yozganda Extiyotkorlik bilan yondashing sizni sapam qilishi mumkun",
                "Siz Kelin nomzodga xabar yozmoqda siz xush momlada bo'ling uni ranjitmang"
            ];
            
            let currentTextIndex = 0;
            const animatedTextElement = document.getElementById('animatedText');
            
            setInterval(() => {
                animatedTextElement.textContent = animatedTexts[currentTextIndex];
                currentTextIndex = (currentTextIndex + 1) % animatedTexts.length;
            }, 5000);
        }

        function updateOnlineUsers() {
            const femaleCount = document.getElementById('femaleCount');
            const maleCount = document.getElementById('maleCount');

            const newFemaleCount = Math.floor(Math.random() * (3000 - 2500 + 1)) + 1500;
            const newMaleCount = Math.floor(Math.random() * (1800 - 1500 + 1)) + 1300;

            femaleCount.textContent = newFemaleCount;
            maleCount.textContent = newMaleCount;

            femaleCount.classList.add('flip');
            maleCount.classList.add('flip');

            setTimeout(() => {
                femaleCount.classList.remove('flip');
                maleCount.classList.remove('flip');
            }, 500);
        }

        setInterval(updateOnlineUsers, 30000);

        updateOnlineUsers();

        function clearOldMessages() {
            const chatMessages = document.getElementById('chatMessages');
            const messages = chatMessages.getElementsByClassName('message');
            const maxMessages = 100; // Maksimum saqlash kerak bo'lgan xabarlar soni

            if (messages.length > maxMessages) {
                const messagesToRemove = messages.length - maxMessages;
                for (let i = 0; i < messagesToRemove; i++) {
                    chatMessages.removeChild(messages[0]);
                }
            }
        }

        setInterval(clearOldMessages, Math.floor(Math.random() * (40000 - 30000 + 1)) + 30000);

        document.getElementById('sendYordamMessage').addEventListener('click', () => {
            const input = document.getElementById('yordamInput');
            const text = input.value.trim();
            if (text) {
                addMessage(document.getElementById('yordamMessages'), text, true);
                const yordamBot = new Bot(
                    ["Salom xush kelib siz", "Balki siz tugmani 2 marta boshgan siz", "Tugmani takror bosmang"],
                    document.getElementById('yordamMessages'),
                    30000
                );
                yordamBot.start();
                input.value = '';
            }
        });
    </script>
</body>
