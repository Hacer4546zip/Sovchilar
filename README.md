<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pinkod Terib Kirish & Chat</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-image: url('https://images.wallpaperscraft.ru/image/single/skaly_gory_vershiny_123926_1080x1920.jpg');
            background-size: cover; /* Rasmni to'liq ekranga yopishtirish */
            background-position: center; /* Rasmni markazda joylashtirish */
            color: #ffffff; /* Oq matn */
            display: flex;
            flex-direction: column;
            justify-content: center; /* Vertikal markazlash */
            align-items: center; /* Gorizontal markazlash */
            height: 100vh; /* Butun balandlikni egallash */
            margin: 0;
        }

        .container {
            display: flex;
            flex-direction: column;
            align-items: center; /* Elementlarni gorizontal markazlash */
            width: 80%; /* Mobil ekran uchun kenglik */
            max-width: 600px; /* Maksimal kenglik */
            background-color: rgba(49,49,49,0.259); /* Fon rangini shaffof qilish */
            padding: 20px; /* Ichki bo'shliq */
            border-radius: 20px; /* Burchaklarini yumshatish */
            box-shadow: 0 2px 10px rgba(0,0,0,0.484); /* Soyali ko'rinish */
        }

        .greetings {
            color: black; /* Qora rang */
            font-size: 4vw; /* Ekran o'lchamiga mos kenglikdan kelib chiqadigan hajm */
            font-weight: bold; /* Qalin harflar */
            margin-bottom: 3px; /* Pastga bo'shliq */
            text-align: center; /* Markazdan joylash */
            opacity: 0; /* Dastlab shaffof */
            animation: fadeIn 2s forwards; /* Animatsiya qo'shildi */
        }

        @media (max-width: 600px) {
            .greetings {
                font-size: 2vw; /* Kichik ekranlar uchun yana ham kichikroq hajm */
            }
        }

        @media (max-width: 200px) {
            .greetings {
                font-size: 7vw; /* Juda kichik ekranlar uchun yana ham kichikroq hajm */
            }
        }

        .pin-container, .chat-container {
            background-color: transparent; /* Pin va chat konteynerlarining fonini shaffof qilamiz */
            padding: 15px;
            border-radius: 20px;
            box-shadow: 0 2px 10px rgb(17,17,17);
            margin: 5px 0;
            width: 100%;
        }

        h2 {
            margin-bottom: 20px;
            color: #00ff00;
            text-align: center;
        }

        input[type="password"], input[type="text"], input[type="url"] {
            width: 75%;
            padding: 10px;
            margin: 10px 0;
            border: 2px solid rgba(251,0,0,0.917);
            border-radius: 13px;
            background-color: #000000;
            color: #ffffff;
        }

        button {
            padding: 10px 20px; /* Tugma ichidagi bo'shliqlar */
            background-color: #00ff00;
            color: black;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            width: auto; /* Tugmalarning kengligi avtomatik bo'ladi */
            margin-left: 10px; /* Tugma kirish maydonidan bir oz masofa */
        }

        button:hover {
            background-color: #00d500;
        }

        .error-message {
            color: #ef0909;
            margin-top: 10px;
            display: none;
        }

        .chat-box {
            max-height: 300px; /* Chat oyna balandligi */
            overflow-y: auto; /* Oqim kerak bo'lsa, skroll qiladi */
            background-color: #00000031;
            padding: 10px;
            border-radius: 10px;
            margin-bottom: 10px;
            flex: 1; /* Chat-box bo'sh joyni egallaydi */
        }

        .chat-message {
            margin: 5px 0;
            animation: fadeIn 0.5s forwards, slideIn 0.5s forwards; /* Animatsiya qo'shildi */
        }

        .bot-message {
            text-align: left; /* Bot xabarlari chap tomonda */
            color: white; /* Bot xabarlari oq rangda */
        }

        .user-message {
            text-align: right; /* Foydalanuvchi xabarlari o'ng tomonda */
            color: #00ff00; /* Foydalanuvchi xabarlari yashil rangda */
        }

        .bot-name {
            color: red; /* Bot nomini qizil rangda ko'rsatish */
        }

        .chat-input {
            display: flex; /* Flex qoidasi yordamida joylash */
            width: 100%;
            justify-content: center; /* Tugmalarni markazlashtirish */
            margin-top: 10px; /* Yuqori tomondan bo'shliq */
        }

        .chat-input input {
            flex: 1; /* Xabar kiritish maydoni kengligi */
            margin-right: 5px; /* O'ng tarafda bo'shliq */
            height: 14px; /* Xabar kiritish joyi balandligi */
            font-size: 14px; /* O'lcham o'zgarishi */
            padding: 10px; /* Ichkaridan bo'sh joy */
        }

        @keyframes fadeIn {
            0% {
                opacity: 0;
                transform: translateY(-20px); /* O'ngdan chiqish */
            }
            100% {
                opacity: 1;
                transform: translateY(0); /* O'z holatiga o'tish */
            }
        }

        @keyframes slideIn {
            from {
                transform: translateY(10px); /* Pastdan yuqoriga ko'chirish */
            }
            to {
                transform: translateY(0); /* Dastur bo'yondan o'z holatiga o'tish */
            }
        }

        .button-container {
            margin-top: 20px; /* Tugma ko'rsatiladigan joy */
            display: none; /* Dastlab ko'rsatmaymiz */
            text-align: center; /* Markazdan joylash */
        }

        .link-message {
            margin-top: 10px; /* "Havola chiqadi" matniga bo'shliq */
            text-align: center; /* Markazdan joylash */
            color: #e4d7d7; /* Matn rangini qizil qilish */
        }

        .flex-container {
            display: flex; /* Flex qoidasi yordamida joylash */
            justify-content: space-between; /* Maydonni bo'sh joylar bilan to'ldirish */
            align-items: center; /* Vertikal markazlash */
        }

        /* Animatsiya qo'shilishi kerak bo'lgan matnlar */
        .animated-text {
            opacity: 0; /* Dastlab, shaffof */
            animation: fading 3s forwards; /* Animatsiya */
        }

        @keyframes fading {
            0% {
                opacity: 0; /* Boshlanishda shaffof bo'lishi */
            }
            100% {
                opacity: 1; /* Olingandan so'ng to'liq ko'rinishi */
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="pin-container">
            <h2 class="animated-text">Диккат Кизни Телеграмига Хабар Ёзищ Учун Махсус Код Керак...👮‍♂️</h2>
            <form id="pinForm" onsubmit="return verifyPin(event);">
                <div class="flex-container">
                    <input type="password" id="pin" placeholder="Pinkodni kiriting...." required maxlength="8" pattern="\d{1,8}">
                    <button type="submit" form="pinForm">Pin Kodni Tasdiqlash</button> <!-- Tugma joylashtirildi -->
                </div>
                <div class="error-message" id="error-message">Noto'g'ri pin kod! Iltimos, qayta urinib ko'ring...?</div>
                <div class="link-message">
                    <h3 class="animated-text">👋 Кодни Тугри Теринг Адашманг ва Тасдиклаш Тугмасини Босинг Ва 1 Менут Кутинг Агар Кирмаса У Зайнет ❗ Бироздан Сунг Кириб Хабар Олинг Бундай Вазиятда Маслахатим щу 🫡 </h3>
                </div>
            </form>
            <div class="button-container" id="buttonContainer">
                <a href="#" id="girlLink" class="access-button" target="_blank">Qizning havolasi</a>
            </div>
        </div>
        
        <div class="chat-container">
            <h2>Online Chat 7/24</h2>
            <div class="chat-box" id="chatBox"></div>

            <!-- Chat yozish joyi -->
            <div class="chat-input">
                <input type="text" id="chatMessage" placeholder="Xabar yozing..." required>
                <button onclick="sendMessage()">Yuborish</button>
            </div>
        </div>
    </div>

    <script>
        const validPins = ['760', '769', '6622', '6287']; // Yangi pin kodlar ro'yhati
        const botMessages = [
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
        "Man xam elon joylamoqchiman akalar natija qanday",
        "♡ man elon berdimku qizlar manga telfon qildi raxmat opa",
        " opa sizga raxmat manga tel qilshdi",
        "Гап ю муниса",
        "ва мазза килдим гаплашиб кизлар билан",
        "Raxmat munis asalim natija zor ekan",
        "nima spam berdiz jonim spam bermang manga",
        "elon bergan man zirikishdan kirdim",
        "Farxod ismim kicha elon bergandim natijasi zo'r bo'ldi raxmat hammaga",
        "Hamma Onlinemi",
        "Munischa sizga raxmat",
        "шу кизча савобга колди ман бахтимни топдим",
        "Муниса сингилжоним рахмат якинда туй киламан",
        "Бугун кайфиятим ало чунки эрга тегябман",
        "ишончлими акалар ман янги ман",
        "ха эшончли элон бириб курган ман кизлар скворади телифон килиб",
        "ха манам элон бирдим ишдан колдирди жуда коп телефон килишар экан",
        "манам элон бериб килдим хозир",
        "50 minga arziydi raxmat",
        "Raxmat",
        "baraka toping singlim",
        "Admenka raxmat turmushga chiqyabman xorazimga",
        "asalim raxmat sizga baxtimni topdim",
        "telefon raqamizni etvoring manga",
        "Rustam aka manga telefon qiling megabaytim kam",
        "Salom xammaga manam keldim",
        "Guli erga tegdizmi",
        "Faxriddin aka uylandizmi aka man Anora",
        "Elon bergan qizga yozdim gaplashdim raxmat",
        "Man kod sotib olgan man ishladi raxmat",
        "Manda kod bkr sotaman 30 minga",
        "Diqqat man 50 minga kod sotib olgan man ushani sotaman 25 mingga kim oladi",
        "Manda Kod Bor Sotiladi 15 ming paynet qilasiz",
        "Kod Sotmaylar blok qiladi admen",
        "код олганлар кодингизни бировга сотсангиз блок буласизлар аник",
        "Манда хам код бор 1 йиллик сотаман 50 минг ким олади натижаси зор коп кизлар билан гаплашиб танишасиз",
        "эй ман код бор сотаман хамма кизларга ёщиш учун нархи 100 минг сум",
        "Код сотилади 150 мнг вип код каналдаги хамма кизларга тугридан тугри хабар ёзиш мумкун",
        "Элон ман 2004 йил ман эрга тегмокчиман фаргонадан ман",
        "Мен сизга уйланардим опа ёщиз катта",
        "код бор манда",
        "кизларга ёзиш учун код сотаман кимда олиш ният бор",
        "arzonga kod sotaman 20 minga 1 oylik kim oladi shu kanalda elonga chiqarilgan qizlarga 1 oy yozolasiz",
        "Qizlarga yozish uchun menda kod bor sotaman kim oladi bolla",
        "Kod Sotmaylar blokka tushub qolasiz javob",
        "Chatda uzini kodini sotganlar kodingiz ko'yib qoladi sotmang",
        "Velik sotaman sport kim oladi narxi 500 ming katta bolonlari",
        "Elektron skutir sotaman oladigonlar bormi",
        "Qachon bir piva ichib mazza qilib utiramiz grupa ahli",
        "pivaga husi borlar bormi",
        "Toshkentli qizla bomi",
        "Niyati jiddiy oqila vafodor mehribon ayol bolsa lichkaga yosin niyat jiddilar iltmos",
        "Samarqand viloyatidan niyati jiddiy ayol bormi",
        "Жиддий ниятли эркаклар борми личкага ёзинг танишамиз",
        "kelilar gaplashib ötramiz",
        "Спам босме йўқ тўғри кемеди дисен ўласанми покиза ўзи ерсираб турган бўсен",
        "Kod oling admendan qizlarga yozolasiz man olgan man",
        "Kod olish kerak ekan qizlarga yozish uchun",
        "Kodni narxini biladigon bormi",
        "Men tojikistondan Guli man 2005 yil",
        "Kod oldim natija yaxshi raxmat",
        " Kod olish kerak ekan qizlarga yozish uchun, bu juda foydali! ",  
" Yozish uchun kodni qanday qilib olish mumkinligini bilasizmi? ",  
" Men tojikistondan Guli man, 2005 yil, qizlar bilan gaplashish yaxshi! ",  
" Kod oldim, natija chindan ham yaxshi, raxmat! ",  
" Har kimga kerak, kod olish uchun kerakli ma'lumotlar! ",  
" Kodni narxini biladigon bormi? Bu juda qiziq! ",  
" Qizlar bilan muloqot qilish uchun kodning ahamiyati juda katta. ",  
" Murojaat qilish robotiga juda qiziq. ",  
" Raxmat, kod olgach, qizlar bilan so'zlashish juda oson! ",  
" Har bir inson uchun qizlarga yozish imkoniyatini yaratadi. ",  
" Men kod oldim va natijalarni kutmoqdaman! ",  
" Kodga ega bo'lgach, yangi aloqalarni o'rnatish mumkin. ",  
" Qizlar bilan tanishish osonlashdi, bu kodni olish kerak edi. ",  
" Bugun muloqot qildim, juda ko'p qiziqarli qizlar bor! ",  
" Kod narxini bilmoqchiman, chiroyli qizlar bilan gaplashish qiyin bo'lmasligi kerak. ",  
" Qizlar bilan yozish uchun o'ziga xos kodlar kerak ekan! ",  
" Dastlabki tajriba juda yaxshi o'tdi, raxmat sizga! ",  
" Qizlar bilan muloqot qilish tajribasi juda yoqdi. ",  
" Barcha qizlar juda samimiy va ochiq! ",  
" Yana boshqa qizlar bilan gaplashish uchun kod olish kerak. ",  
" Bu jarayon juda qiziqarli, shunchaki hozir boshlasam ham bo'ladi! ",  
" Tanlov keng, har xil qizlar bilan suhbatlashish imkoniyati bor! ",  
" Kod olish juda muhim ekan, xuddi orzudek! ",  
" Raxmat sizlarga, asosiy narsani berasizlar! ",  
" Men yana kod olishim kerak, bu juda qiziq! ",  
" Yozish jarayoni juda qiziqarli, siz bilan faxrlanaman! ",  
" Har bir suhbat yangi imkoniyatlarni ochadi! ",  
" Kodni olish jarayoni yaxshi o’tdi, imkoniyatlar shunchaki cheksiz! ",  
" Qizlar bilan bog'lanish juda muhim! ",  
" Kodingiz bormi? Agar yo'q bo'lsa, tezda oling! ",  
" Kenja va chiroyli qizlar bilan bog'lanish juda muhim! ",  
" Men yangi aloqa o'rnatdim va kodim sharafi bilan! ",  
" Muloqot qilish yozuvimizdagi kuchli tajriba! ",  
" Poytaxtda qizlar bilan tanishish uchun bu kod juda samarali! ",  
" Albatta, o'z shahrimdan qizlar bilan gaplashishni kutyapman. ",  
" Kod oldim, juda ko'p qizlar bilan oson suhbatlashyapman! ",  
" Boshqa imkoniyatlardan, narsani qulay dastur bilan ko'rishingiz mumkin! ",  
" Qizlar bilan suhbatda yanada ko'proq qiziqarli vatanlash! ",  
" Kod olganimdan berun, juda ko'p qizlar bilan oson suhbatlashdi! ",  
" Yozish jarayoni juda rahmatli va qiziqarli! ",  
" Juda yoqimli qizlar bilan o'zaro bog'lanish! ",  
" Suhbatlarni yangilash uchun kod olish haqida o'ylayman! ",  
" Bu kod orqali kirgan suhbatlar juda hayajonli! ",  
" Yozing va qizlar bilan bog'lanishni darhol boshlang! ",  
" Har bir yangi muloqot yangi tajribalar, yangi naif g'oyalar beradi! ",  
" Meni kutayotgan qizlar juda sevgi va mehr bilan! ",  
" Kodni o'zingizdan so'rashga va taklif qilishga harakat qiling! ",  
" Men muloqotlarim orqali ko'proq qiziqarli qizlar bilan tanishdim! ",  
" Kitob o'qichilar uchun bir joyda tanishuv juda yoqadi! ",  
" Maktabdan keyin maydalagan qizlar bilan ortga qaytish! ",  
" Qizlar uchun kod, bu juda zarur va hayotiy muhim! ",  
" O'zaro aloqalarni ko'paytirish uchun zarur bo'lsa, yozing! ",  
" Qizlar bilan tanishish qiyinmas edi, kodim bor! ",  
" Yana kod olishni va qizlar bilan suhbatda davom etmishni xohlayman! ",  
" Va'da beraman, kod olish jarayoni osonlik va qulaylik! ",  
" Kodingizni bilib, qizlar bilan bog'lanish juda ! ",  
" Bu tajriba har bir qiz bilan o'zaro aloqalar ochadi! ",  
" Suhbat davomida bir-birimizni yaxshiroq tushunishga harakat qilamiz! ",  
" Qizlar bilan uchrashish juda qiziq va yangi g'oyalar olib keladi! ",  
" Qizlar bilan tanishish va yangiliklarni o'rganish ajoyib! ",  
" Muloqot qilish uchun ovoz berish shunchaki zarurlik! ",  
" Kodlarni oling va qizlar bilan tezda suhbat boshlang! ",  
" Raxmat, bu kodga menga yangi imkoniyatlarni berdi! ",  
" Qizlar bilan qiziqarli suhbatlar har doim yoqimli! ",  
" Kodli hamkorlikda qizlar bilan yaxshi aloqa o'rganing! ",  
" Suhbatlarim go'zal bo'ladi, muloqotlarini kutib qolaman! ",  
" Qizlarni yozish jarayonida yoningda bo'lishni istayman! ",  
" Kodingizni olishni unutmang, qizlar bilan juda qiziqarli! ",  
" Tanlovda ochiq ko'ngilni kashf eting, muloqot muhim! ",  
" Raxmat, muloqot qilish jarayoni bilan ko'rish! ",  
" Har bir qiz bilan yangi imkoniyatlar kutyapman! ",  
" Yozish kunga bir oz ko'rsatuvchi bo'lishi kerak! ",  
" Kechki suhbatlar juda o'ziga xos va chiroyli! ",  
" Men qizlar bilan suhbatlashishni juda sevaman, kod oldim! ",  
" Yozish jarayonini kuchaytirish uchun zarur kodni olish! ",  
" Taqdimot yangi imkoniyatlar sahnasidan chiqadi! ",  
" Qizlar bilan yaxshi aloqalar o'rnatish har doim muhim! ",  
" O'zingizni yangilangan kodda his qilmoqdasiz! ",  
" O'zaro muloqot qilish jarayoni baxtli bo'ling! ",  
" Borayotgan qizlar barchani sevganlarimni yodda tuting! ",  
" Har qanday g'oyalar, ushbu kod orqali chiqishi mumkin! ",  
" Har doim ochiq suhbatlar, qizlar bilan birga eng muhim! ",  
" Kodlar orqali qizlar bilan xursandchilikni oshiring! ",  
" Yangi qizlar bilan muloqotda davom etaman! ",  
" Kod oldim va natijalarni kuta boshladim, sevgi bilan! ",
" Qizlarga yozish uchun kod olish juda muhim! ",  
" Kodni qanday qilib olishni bilasizmi, shu haqda o'ylaylik! ",  
" Men qizlar bilan muloqot qilishni yaxshi ko'raman, barchasi qiziqarli! ",  
" Kodni olishdan juda xursandman, natijalar ajoyib! ",  
" Har kimga ma'lum kod kerak bo'lishi mumkin! ",  
" Qizlar bilan suhbatlashish uchun kodning narxi qanday? ",  
" Yozish jarayonida qizlar bilan aloqalar juda muhimdir! ",  
" Murojaat robotlari qiziqarli, ko'p savolga javob beradi! ",  
" Kodimni olgach, qizlar bilan xushmuomala bo'lishim osonlashdi! ",  
" Muloqot qilish uchun qizlarga yozish imkoniyatiga ega bo'ladim! ",  
" Kod oldim, endi yangi tanishuvlar kutyapman! ",  
" Nima uchun kod olish muhim, bilasizmi? Yangi aloqalar ochiladi! ",  
" Qizlar bilan tanishishni boshlash uchun zarur kodni olish kerak! ",  
" Bugun juda ko'p qiziqarli qizlar bilan gaplashdim! ",  
" Kod narxi haqida bilmayman, kimdir aytishi mumkinmi? ",  
" Qizlar bilan yozish jarayoni uchun qiziqarli xususiyatlar kerak! ",  
" O'ylayman, yozuvimda yanada ko'proq qiziqarli bo'laman! ",  
" Suhbatlar juda ko'p, turli qizlar bilan tanishish imkonim bor! ",  
" Kod olish – bu orzudek, ushbu imkoniyatni hech qachon yoddan chiqarmayman! ",  
" Raxmat, sizlar yordam berdingiz! ",  
" Yana bir marta kod olishni xohlashim haqida o'ylayman, juda qiziqarli! ",  
" Yozish jarayoni davom etmoqda, va juda qiziq! ",  
" Bu jarayonda samimiy qizlar bilan tanishganim uchun xursandman! ",  
" Yana boshqa qizlar bilan aloqalar o'rnatish uchun kod kerak! ",  
" Suhbat jarayoni juda hayajonli, buni imkoniyat sifatida ko'raman! ",  
" Tanlov keling, har xil qizlar bilan muloqot qilish imkonini beradi! ",  
" Kodni olish juda muhim, chunki bu menga kerak edi! ",  
" Raxmat, sizlarga! Kod ma'lumotlaringiz uchun! ",  
" Yana kod olishni o'ylayapman, qizlar bilan muloqot juda qiziqarli! ",  
" Har bir suhbat yangi imkoniyatlarni ochadi! ",  
" Kod olish jarayoni juda oson va qulay! ",  
" Qizlar bilan bog'lanish menda juda muhim! ",  
" Kodingiz yo'qmi? Agar kerak bo'lsa, uni hoziroq oling! ",  
" Kenja va chiroyli qizlar bilan bog'lanish juda foydali! ",  
" Yangi aloqa o'rnatib, qizlar bilan yaxshi suhbatlar qilmoqchiman! ",  
" Muloqot jarayoni davomida qiziqarli narsalarni bilib oldim, rahmat! ",  
" Poytaxtda qizlar bilan tanishishni o'z umidim deb bilaman! ",  
" Kod oldim, endi ko'p qizlar bilan suhbatlashishim mumkin! ",  
" Boshqa imkoniyatlar qiziqarli va muloqot uchun qulay! ",  
" Qizlar bilan yozish tajribasi, albatta, hayajonli voqea! ",  
" Kodni olishdan oldin bir oz kutdim, natijalarni ko'rishni kutyapman! ",  
" Suhbat jarayoni juda hayajonli va foydali! ",  
" Yana yangi qizlar bilan tanishishga tayyorman! ",  
" Kod olish qizlar bilan qiziqarli uchrashuvlar imkonini yaratadi! ",  
" O'zingizni yangi imkoniyatlarda his qilishingiz kerak! ",  
" Suhbat davomida bir-birimizni yaxshiroq tushunish eng yaxshi narsa! ",  
" Qizlar bilan uchrashish juda qiziqarli va ko'plab g'oyalar olib keladi! ",  
" Muloqot qilish jarayoni men uchun muhim! ",  
" Kodlarni oling va yangi suhbatlarni boshlang! ",  
" Raxmat, bu kod menga yangi imkoniyatlar berdi! ",  
" Qizlar bilan qiziqarli suhbatlar har doim kutilgan! ",  
" Kodli hamkorlikda qizlar bilan muloqot qilish imkoniyatini o'rganing! ",  
" Suhbatlarim zamonaviy va qiziqarli bo'ladi! ",  
" Qizlar bilan yozish jarayoni davom etmoqda, bu juda qiziqarli! ",  
" Kodingizni olishni unutmang, bu qizlar bilan tanishishga yordam beradi! ",  
" Tanlovda ajoyib imkoniyatlarni kashf eting! ",  
" Raxmat, bu muloqotda hazil va unutilmas tajribalar berasiz! ",  
" Har bir yangi tanishuv uchun yangi imkoniyatlar mavjud! ",  
" Yozish jarayonini yanada yoqimli qilish uchun tayyorman! ",  
" Kechki suhbatlar doimo ajoyib va qiziqarli! ",  
" Men qizlar bilan suhbatlarni juda sevaman, kod oldim! ",  
" Yozish jarayonini kuchaytirish uchun zarur kod olishga tayyorman! ",  
" Taqdimot yangi imkoniyatlar haqida tushuncha beradi! ",  
" Qizlar bilan yaxshi aloqalar o'rnatish har doim muhim! ",  
" O'zingizni yanada yaxshi his qilish uchun qizlar bilan kashf etishingiz mumkin! ",  
" O'zaro muloqot jarayoni men uchun juda baxtli! ",  
" Borayotgan qizlar bilan samimiy aloqalar juda yaxshi! ",  
" Har qanday qiziqarli g'oyalar ushbu kod orqali kelishi mumkin! ",  
" Ochiq suhbatlar har doim qizlar bilan eng yaxshi xulosalarga olib keladi! ",  
" Kodlar orqali qizlar bilan muloqotda yanada ko'proq qiziqish ochin! ",  
" Yangi tajribalar davomida qizlar bilan yaxshi imkoniyatlar o'rnataman! ",  
" Kod oldim va natijalarni kutmoqdaman! ",
"Dilnoza",  
"Aziza",  
"Shahnoza",  
"Malika",  
"Nodira",  
"Saida",  
"Muqaddas",  
"Zilola",  
"Farida",  
"Laylo",  
"Shirin",  
"Feruza",  
"Nilufar",  
"Fatima",  
"Dilafruz",  
"Sitora",  
"Samira",  
"Diana",  
"Shahzoda",  
"Mahnoza",  
"Gulsara",  
"Gulbahor",  
"Umida",  
"Jamila",  
"Rayhona",  
"Yulduz",  
"Parvina",  
"Shodigul",  
"Nargiza",  
"Dilyara",  
"Shahida",  
"Zaynab",  
"Sanoora",  
"Asal",  
"Mahfuza",  
"Nasiba",  
"Bahora",  
"Rano",  
"Saodat",  
"Shokhida",  
"Gulay",  
"Rabia",  
"Nilofer",  
"Nozima",  
"Oydin",  
"Lobar",  
"Nubora",  
"Shohida",  
"Zarrina",  
"Xurshida"
        ];
        const bots = ['Foydalanuvchi', 'Foydalanuvchi', 'Foydalanuvchi', 'Foydalanuvchi', 'Foydalanuvchi', 'Foydalanuvchi',];
        const links = [
            "https://t.me/iyutcuccu ",
            "https://t.me/Makkah_go ",
            "https://t.me/Nargiz_Logoped ",
            "https://t.me/Durdona_989 ",
            "https://t.me/Medin_077 ", 
            "https://t.me/Mursalina002 ",
            "https://t.me/Tavakullllll ",
            "https://t.me/MMA1726 ",
            "https://t.me/akbarovna009 ",
            "https://t.me/sakinat20050615 ",
            "https://t.me/hiiletstalk",
            "https://t.me/oakuzb",
            "https://t.me/bpa261",
            "https://t.me/Di_lux88",
            "https://t.me/missmira0401",
            "https://t.me/sabr_iyman01",
            "https://t.me/babbii00",
            "https://t.me/babbii00",
            "https://t.me/IrodaWodi",
            "https://t.me/NozaNK1 ",
            "https://t.me/H19832610 ",
            "https://t.me/Lahavla",
            "https://t.me/ruxsora8810 ",
            "https://t.me/Dilyara_1985 ",
            "https://t.me/Bella6980 ",
            "https://t.me/zhndm01 ",
            "https://t.me/Yuragim211 ",
            "https://t.me/Fotima2356 ",
            "https://t.me/rakhimovna97 ",
            "https://t.me/HGB501004 ",
            "https://t.me/kunfayakun96 ",
            "https://t.me/Mumtoza2233 ",
            "https://t.me/biinafsha ",
            "https://t.me/Baxt_557 ",
            "https://t.me/DILYA_56_56 ",
            "https://t.me/sad1_chka ",
            "https://t.me/zul9897 ",
            "https://t.me/lilyrser ",
            "https://t.me/wellu90 ",
            "https://t.me/KGuli01 ",
            "https://t.me/IIJI_com ",
            "https://t.me/ww_8283 ",
            "https://t.me/Kz_kz99 ",
            "https://t.me/rosamarinne ",
            "https://t.me/Farangiz051 ",
            "https://t.me/imkon_999 ",
            "https://t.me/babbii005500 ",
            "https://t.me/Jonkam92 ",
            "https://t.me/ledy177 ",
            "https://t.me/dunyo_026 ",
            "https://t.me/summer_4488 ",
            "https://t.me/Nelll22 ",
            "https://t.me/Suyanchiqlarm ",
            "https://t.me/XCh_1905 ",
            "https://t.me/Ppppp_dddfff ",
            "https://t.me/missmira0401 ",
            "https://t.me/Sab1r ",
            "https://t.me/Moychechak202202 ",
            "https://t.me/Stamina_095 ",
            "https://t.me/Onam_jannatim0961 ",
            "https://t.me/dilimmen",
            "https://t.me/Qodirova_Zaynabbegim ",
            "https://t.me/Inshaalloh8888 ",
            "https://t.me/hggff65yt56yt ",
            "https://t.me/abde129920 ",
            "https://t.me/Lfwnsns ",
            "https://t.me/baxtim_izlab1 ",
            "https://t.me/sadiya_102 ",
            "https://t.me/Ndldkejfb ",
            "https://t.me/TAQDIR0202 ",
            "https://t.me/Samolarda6865 ",
            "https://t.me/parishta88 ",
            "https://t.me/Angelina_uz1 ",
            "https://t.me/Oydin_98 ",
            "https://t.me/BAHTIMSAN12 ",
            "https://t.me/hghhu76yt65t ",
            "https://t.me/nurnoma29 ",
            "https://t.me/hghgf6y5t45tr ",
            "https://t.me/Oyqiz_33 ",
            "https://t.me/maxliyo0606 ",
            "https://t.me/Jannatimsiz22 ",
            "https://t.me/Gullola1287 ",
            "https://t.me/niveasd ",
            "https://t.me/Tursunovaaaaaa ",
            "https://t.me/notanishka ",
            "https://t.me/Anoorxon ",
            "https://t.me/Melibayeva1 ",
            "https://t.me/Magnitcha_25 ",
            "https://t.me/hgh6gy65y09oi ",
            "https://t.me/jenifer_lops ",
            "https://t.me/Oxu70 ",
            "https://t.me/Flegmatik_2014 ",
            "https://t.me/Oyisha49 ",
            "https://t.me/Soxtaaa0022 ",
            "https://t.me/gulim9315 ",
            "https://t.me/dunyo1752 ",
            "https://t.me/nilufar95hgg ",
            "https://t.me/Baxtiimsizz ",
            "https://t.me/Bahtfasli ",
            "https://t.me/umkdaxon ",
        ];
        let botInterval;

        // Botlardan tasodifiy xabar yuborish
        function sendRandomBotMessages() {
            const botName = bots[Math.floor(Math.random() * bots.length)];
            const messageContent = botMessages[Math.floor(Math.random() * botMessages.length)];
            const messageElement = document.createElement('div');
            messageElement.className = 'chat-message bot-message'; // Bot xabari
            messageElement.innerHTML = `<span class="bot-name">${botName}</span>: ${messageContent}`; // Bot nomini qizil rangda
            document.getElementById('chatBox').appendChild(messageElement);

            scrollChatToBottom();
        }

        // Botlardan xabar yuborishni boshlash
        function startBotMessages() {
            botInterval = setInterval(sendRandomBotMessages, 2000);
        }

        // Pinni tekshirish
        function verifyPin(event) {
            event.preventDefault();
            const pin = document.getElementById('pin').value;
            const errorMessage = document.getElementById('error-message');
            const buttonContainer = document.getElementById('buttonContainer');

            if (validPins.includes(pin)) {
                alert('Kirish muvaffaqiyatli!');
                // Tasodifiy havola ko'rsatish
                const randomLink = links[Math.floor(Math.random() * links.length)];
                const girlLink = document.getElementById('girlLink');
                girlLink.href = randomLink; // Havolani yangilash
                buttonContainer.style.display = 'block'; // Tugmani ko'rsatish

                // 3 soniyadan so'ng havolaga o'tish
                setTimeout(() => {
                    window.location.href = randomLink; // Foydalanuvchini havolaga yo'naltirish
                }, 3000);
            } else {
                errorMessage.style.display = 'block';
            }
        }

        // Xabar yuborish
        function sendMessage() {
            const chatBox = document.getElementById('chatBox');
            const chatMessage = document.getElementById('chatMessage');
            const message = chatMessage.value;

            if (message) {
                const messageElement = document.createElement('div');
                messageElement.className = 'chat-message user-message'; // Foydalanuvchi xabari
                messageElement.textContent = `Siz: ${message}`;
                chatBox.appendChild(messageElement);
                chatMessage.value = ''; // Xabar kiritish maydonini tozalash

                // Chat oynasini pastki qismga aylanish
                scrollChatToBottom();
            }
        }

        // Chat oynasini pastki qismga aylantirish
        function scrollChatToBottom() {
            const chatBox = document.getElementById('chatBox');
            chatBox.scrollTop = chatBox.scrollHeight;
        }

        // Foydalanuvchi sahifaga yuklanganda bot xabarlarini boshlash
        window.onload = function() {
            startBotMessages();
        };
    </script>
</body>
</html>
