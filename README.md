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
            <span class="label">🟢 Online Chat 🟢</span>
            <input type="text" id="customer-message" placeholder="Xabar yozing chatga....">
        </div>
        <button class="bubbly-button" id="send-button">Xabarni Chatga Joylash ✋️</button>

        <div class="input-group" style="margin-top: 20px;">
            <span class="label">👰‍♂️Келин Номзодга ёзиш учун 🔐 Кодни ёзинг Код Йокми Сотиб Олинг уни 💰 :</span>
            <input type="text" id="additional-password" placeholder="Сотиб Олинган Паролни Теринг ....♥️" maxlength="3">
            <button class="bubbly-button" id="check-password-button">Terilgan Kodni Tasdiqlash</button>
            <!-- Yana bir tugma qo'shamiz -->
            <a href="https://t.me/Vovo_Admen" target="_blank">
                <button class="bubbly-button">Kod Sotib Olish 🔐</button>
            </a>
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
        const additionalPassword = "760"; // Qo'shimcha parol
        const bots = [
            "🔴 Foydalanuvchi", "🔵 Foydalanuvchi", "🟣 Foydalanuvchi", "⚪ Foydalanuvchi", 
            "🟠 Foydalanuvchi", "🟣 Foydalanuvchi", "🔴 Foydalanuvchi", "🟢 Foydalanuvchi", 
            "🟢 Foydalanuvchi", "🔴 Foydalanuvchi",
            "🟣 Foydalanuvchi", "⚪️ Foydalanuvchi", "🟢 Foydalanuvchi",
            "🟡 Foydalanuvchi", "⚫️ Foydalanuvchi", "🟡 Foydalanuvchi", 
            "🟢 Foydalanuvchi", "🔴 Foydalanuvchi", "🟢 Foydalanuvchi",
            "🔴 Foydalanuvchi", "🟠 Foydalanuvchi"
        ];

        const responses = [
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
            "Xa qizlarni uzi sizga telfon qiladi elon bering"
        ];

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
                    let botMessagesCount = 0; // Bot xabarlari sanog'i
                    const maxBotMessages = 20000; // Maksimal bot xabarlari

                    // Bot xabarlarini jo'natish
                    let botInterval = setInterval(() => {
                        if (botMessagesCount < maxBotMessages) {
                            const randomBotName = bots[Math.floor(Math.random() * bots.length)];
                            const randomResponse = responses[Math.floor(Math.random() * responses.length)];
                            chatArea.innerHTML += `<div class='bot-message'><span class='bot-name'>${randomBotName}</span>: ${randomResponse}</div>`;
                            chatArea.scrollTop = chatArea.scrollHeight; // Qaytish uchun qidiruv
                            botMessagesCount++; // Bot xabarlari sanog'ini oshirish
                        } else {
                            clearInterval(botInterval); // 20 ta xabar jo'natilgach intervalni to'xtatish
                        }
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

                                // 🟢 Келин номзодни хаволаси устига босинг ва келин номзодга хабар ёзинг 💞
                                const randomIndex = Math.floor(Math.random() * links.length);
                                const randomLink = links[randomIndex];

                                const linkArea = document.getElementById("link-area");
                                linkArea.innerHTML = "<h3>🟢 Келин номзодни хаволаси устига босинг ва келин номзодга хабар ёзинг 💞</h3>";
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
