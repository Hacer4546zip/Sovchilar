<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Online Chat va Kod Terish Sahifasi</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f7f7f7;
            margin: 0;
            padding: 20px;
        }

        h1 {
            text-align: center;
            font-size: 24px;
            color: #333;
        }

        .container {
            max-width: 500px;
            margin: 0 auto;
            background: white;
            padding: 10px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
        }

        .online-users {
            margin-bottom: 20px;
        }

        .chat-box {
            border: 1px solid #ccc;
            height: 300px;
            overflow-y: auto;
            margin-bottom: 10px;
            padding: 10px;
            background-color: #fafafa;
        }

        .input-area {
            display: flex;
            align-items: center;
        }

        .input-area input[type="text"] {
            flex-grow: 1;
            padding: 10px;
            margin-right: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        .input-area button {
            padding: 10px 30px;
            border: none;
            border-radius: 5px;
            background-color: #5cb85c;
            color: white;
            cursor: pointer;
        }

        .input-area button:hover {
            background-color: #4cae4c;
        }

        textarea {
            width: 100%;
            height: 50px;
            padding: 10px;
            font-family: monospace;
            font-size: 14px;
            border: 1px solid #ccc;
            border-radius: 5px;
            box-sizing: border-box;
            margin-bottom: 15px;
        }

        #runBtn {
            display: block;
            width: 100%;
            padding: 15px;
            font-size: 15px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            margin-bottom: 4px;
        }

        #runBtn:hover {
            background-color: #0056b3;
        }

        #output {
            padding: 15px;
            border: 1px solid #ccc;
            border-radius: 5px;
            background-color: white;
            min-height: 50px;
            box-sizing: border-box;
        }

        .message {
            margin: 5px 0;
            padding: 5px;
            border-radius: 5px;
            opacity: 0; /* Animatsiya uchun dastlabki daraja */
            transform: translateY(-10px); /* Yozuvni yuqoridan boshlanishi uchun */
            animation: fadeIn 0.3s forwards; /* Animatsiyani qo'shamiz */
        }

        .message.user {
            background-color: #d1e7dd;
            text-align: right;
        }

        .message.bot {
            background-color: #e2e3e5;
            text-align: left;
        }

        .message span {
            font-weight: bold;
        }

        @keyframes fadeIn {
            to {
                opacity: 1; /* Xabar ko'rinadigan darajaga o'tadi */
                transform: translateY(0); /* Xabar o'z pozitsiyasiga qaytadi */
            }
        }

        .button-container {
            margin-top: 5px;
        }

        .button-container a {
            display: inline-block;
            margin-right: 10px;
            padding: 10px 15px;
            background-color: #007bff;
            color: white;
            border-radius: 50px;
            text-decoration: none;
            text-align: center;
        }

        .button-container a:hover {
            background-color: #0056b3;
        }

        .info-text {
            margin-top: 20px;
            font-size: 18px;
            color: #003;
            text-align: center;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Online Chat Yor Yor Online 7/27</h1>

    <div class="online-users">
        <p><strong>🟢Online Erkaklar:</strong> <span id="online-men"></span></p>
        <p><strong>🟢Online Qizlar:</strong> <span id="online-women"></span></p>
    </div>

    <div class="chat-box" id="chat-box">
        <!-- Chat xabarlar joylashadi -->
    </div>
    <div class="input-area">
        <input type="text" id="message-input" placeholder="Chatga Xabar yozing..." />
        <button id="send-button">Yuborish</button>
    </div>
    
    <h2>Kodingizni Tering (****) Pastga Qarang 👇 </h2>
    <textarea id="codeArea" placeholder="Kodni yozing ......"></textarea>
    <button id="runBtn">🔐  Kodni Tasdiqlash  ✋️</button>

    <h2>🟢 Келинни Хаволаси Чикади 👇</h2>
    <div id="output"></div>
    <div class="button-container">
        <a href="https://t.me/Vovo_Admen" target="_blank">🔐 Kod sotib olish</a>
        <a href="https://t.me/+_rFTajPX3_1kMTg6" target="_blank">📢Telegram Kanal</a>
    </div>
    <div class="info-text">
        Kod Sotib Olish Uchun Admenga Murojat qilishingiz kerak, sizga 5 oylik maxsus Kod Beriladi 🔐 Kelin Nomzodlar Bilan Yaqindan Tanishish uchun ✋ 
        🟢 Kod Sotib Olingandan Sung Barcha Qizlarga Yoza Olasiz Chiksiz istalgan vaxt kodni yozish orqali qizlarni lenki Olasiz va ularga Xush Momilalik bilan o'zingiz haqingizda qisqacha malumot bilan yozishingiz mumkun bo'ladi 🥰 Xizmat Narxi 5 Oylik 50 Ming So'm 🇺🇿
    </div>
</div>

<script>
    let codeUsed = false; // Kodni bir martalik ishlatish uchun bayroq

    // Tasodifiy raqamni yaratish uchun funksiya
    function getRandomInt(min, max) {
        return Math.floor(Math.random() * (max - min + 1)) + min;
    }

    // Online foydalanuvchilar sonini yangilash funktsiyasi
    function updateOnlineUsers() {
        document.getElementById('online-men').textContent = getRandomInt(10000, 28072);
        document.getElementById('online-women').textContent = getRandomInt(10000, 28720);
    }

    // Dastlabki online foydalanuvchilar sonini yangilash
    updateOnlineUsers();

    // Jamlangan online foydalanuvchilar sonini har 6 soniyada yangilash
    setInterval(updateOnlineUsers, 20000);

    // Xabar yuborish
    document.getElementById('send-button').addEventListener('click', function() {
        const messageInput = document.getElementById('message-input');
        const message = messageInput.value;

        if (message) {
            // Xabari ko'rsatish
            const chatBox = document.getElementById('chat-box');
            const userId = getRandomInt(1000, 9999);  // 4 raqamli ID
            const newMessage = document.createElement('div');
            newMessage.classList.add('message', 'user'); // Foydalanuvchi xabari
            newMessage.innerHTML = `<span>ID: ${userId}</span>: ${message}`;
            chatBox.appendChild(newMessage);

            messageInput.value = ''; // Inputni tozalash
            chatBox.scrollTop = chatBox.scrollHeight; // Skrollni pastga tushirish
        }
    });

    // Kodni tekshirish
    function checkCode() {
        const codeInput = document.getElementById('codeArea');
        const code = codeInput.value.trim();
        const output = document.getElementById('output');
        const links = [
            "https://t.me/MISSISS_789",
            "https://t.me/Muiza_010",
            "https://t.me/Life982r",
            "https://t.me/DILYA_27_11",
            "https://t.me/Azizabonu_1995",
            "https://t.me/Insoff02",
            "https://t.me/Biglifemaybeee",
            "https://t.me/UmmuMuhammad1920",
            "https://t.me/Diorggggg",
            "https://t.me/Alxamdulillax9933",
            "https://t.me/BahronovaShahribonu",
            "https://t.me/sevgi_faqat_Allohga_s8",
            "https://t.me/Gulifarim",
            "https://t.me/Kabatullohn",
            "https://t.me/izer99",
            "https://t.me/Iziyiziy",
            "https://t.me/medina_06e",
            "https://t.me/guslu_madam",
            "https://t.me/Zarifa_asila",
            "https://t.me/D9091I",
            "https://t.me/mis_ss_0110",
            "https://t.me/eifhg",
            "https://t.me/Bibi_Hojar94",
            "https://t.me/Xastakongill",
            "https://t.me/ChiroyliQiz_99",
            "https://t.me/LJ0984",
            "https://t.me/fayz1114",
            "https://t.me/Sumayya012397",
            "https://t.me/Dilya00111",
            "https://t.me/Tavohas",
            "https://t.me/YURAK1984",
            "https://t.me/Ddgghhjjkkkl",
            "https://t.me/Baxtim_0308",
            "https://t.me/BAXTIMSAN0202",
            "https://t.me/hgfgft45tru",
            "https://t.me/ao1va",
            "https://t.me/YT1612",
            "https://t.me/Ummatliyligim",
            "https://t.me/Gulim1287",
            "https://t.me/FARGONA1987",
            "https://t.me/Habibim_humayroyim",
            "https://t.me/Jkjhgjj",
            "https://t.me/mehr098iu",
            "https://t.me/gulixadicha",
            "https://t.me/Florrrsss",
            "https://t.me/Guli90966",
            "https://t.me/samiya0797",
            "https://t.me/Azobli099",
            "https://t.me/hggff67uyt56t",
            "https://t.me/hghggg65tr5",
            "https://t.me/Nigora2190",
            "https://t.me/Sabrligim212718",
            "https://t.me/Inshaolloh852911",
            "https://t.me/Missbegim_32",
            "https://t.me/Fff1200Ll",
            "https://t.me/hamanarsagasabr",
            "https://t.me/MBB_444",
            "https://t.me/w7007wa",
            "https://t.me/TALKASHBONU"
        ];

        if (codeUsed) {
            output.innerHTML = "Kechrasiz Siz Xato Tergan Ko'rinasiz Yoki siz Xozir Saxifadan Chiqib Qaytib Kirib Kodni Yozing...!✋️ eslatma Tog'ri kod terilgan ammo qizni havolasi chiqmagan bo'lsa Demak u qiz Zaynet 🤐 Bunday Holatda Siz 1 2 Soatdan Sung Qayta Saxifaga Kirib Kodni Qayta Tering Va Qizni Havolasi Yana O'zini Joyiga Qaytib Qo'yiladi 🟢 Va Qizga Xabar Yozishingiz Mumkun 🔐";
            return; // Agar kod ishlatilgan bo'lsa, funktsiyani to'xtatamiz
        }

        // Xabarlarni tayyorlash
        let linkToShow = '';

        if (code === '760' || code === '6287') {
            const randomLink = links[getRandomInt(0, links.length - 1)];
            linkToShow = `<br>💚 Kelin nomzodni Xavolasi ✋️ Ustiga Bosing va Siz Kelin Nomzodni Lechkasiga O'tib Kitasiz 👇 
             <a href="${randomLink}" target="_blank">${randomLink}</a>`;
            codeUsed = true; // Kod ishlatilganligini belgilaymiz
        } else {
            linkToShow = `<br>🚫 Kod Xato Terild.... Yoki Umuman Terilmagan... To'g'ri Kodni Tering 🔐 `;
        }

        output.innerHTML = linkToShow; // Natijani ko'rsatish
    }

    // Yozilgan kodni natijalar bo'limida ko'rsatish
    document.getElementById('runBtn').addEventListener('click', function() {
        checkCode(); // Kodni tekshirish
    });

    // Botlar
    const bots = [
        { name: 'Ayol Bot 1', id: '🟢 Nomalum...' },
        { name: 'Ayol Bot 2', id: '🟣 Nomalum...' },
        { name: 'Ayol Bot 3', id: '⚫️ Nomalum...' },
        { name: 'Erkak Bot 1', id: '🔴 Nomalum...' },
        { name: 'Erkak Bot 2', id: '🔵 Nomalum...' },
        { name: 'Erkak Bot 3', id: '🟠 Nomalum...' },
        { name: 'Ayol Bot 5', id: '🟡 Nomalum...' }
    ];

    // Tasodifiy xabarlarni yaratish
    function getRandomBotMessage() {
        const messages = [
            "Kicha Mazza Qildim, telfonda gaplashdim 🥰",
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
        "Бу код 5 ой ишлайдими"
        ];
        return messages[getRandomInt(0, messages.length - 1)];
    }

    // Botlar xabar yuboradi
    function startBotMessaging(bot) {
        const interval = getRandomInt(3500, 10000); // Har 3-10 soniyada tasodifiy interval berish
        setInterval(() => {
            const chatBox = document.getElementById('chat-box');
            const botMessage = document.createElement('div');
            botMessage.classList.add('message', 'bot'); // Bot xabari
            botMessage.innerHTML = `<span>${bot.id}</span>: ${getRandomBotMessage()}`;
            chatBox.appendChild(botMessage);
            chatBox.scrollTop = chatBox.scrollHeight; // Skrollni pastga tushirish
        }, interval);
    }

    // Har bir bot uchun xabar yuborish jarayoni
    bots.forEach(bot => {
        startBotMessaging(bot);
    });

</script>

</body>
</html>
