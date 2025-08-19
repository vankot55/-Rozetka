<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Інтерактивна Бізнес-Модель: Академія Продавця Rozetka</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Calm Harmony -->
    <!-- Application Structure Plan: The SPA is designed as an interactive dashboard centered around the Business Model Canvas. This structure was chosen because the source report is fundamentally based on the canvas framework, making it the most intuitive entry point for users. The main view presents the 9 blocks of the canvas. Clicking any block smoothly scrolls the user to a detailed section for that component. This non-linear, exploratory approach is more engaging and efficient for understanding the business model than a linear document. Additional sections for Launch Strategy and KPIs are accessible via a top navigation bar, providing structured pathways to key strategic information. The user flow is designed to go from a high-level overview (the canvas) to granular details on demand. -->
    <!-- Visualization & Content Choices: 
        - Business Model Canvas (Organize): A CSS Grid of interactive cards. Goal: Provide a holistic, at-a-glance view of the entire model. Interaction: Click to navigate. Justification: This is the most direct and logical representation of the report's core structure. Method: HTML/Tailwind CSS Grid + JS for navigation.
        - Customer Segments vs. Value Propositions (Compare): An interactive filter system. Goal: Clearly show which value propositions target which customer segments. Interaction: Clicking segment buttons filters the visible propositions. Justification: This dynamic comparison is more insightful than static lists. Method: HTML/Tailwind + JS DOM manipulation.
        - Financials (Inform): Two side-by-side Doughnut charts. Goal: Visualize the composition of revenue streams and cost structure. Interaction: Hover tooltips. Justification: Doughnut charts are ideal for showing part-to-whole relationships. Library: Chart.js (Canvas).
        - Launch Plan (Change): An interactive horizontal timeline. Goal: Show the phased rollout of the project over time. Interaction: Click to expand phase details. Justification: A timeline is the most intuitive way to represent a chronological plan. Method: HTML/Tailwind Flexbox + JS for interactivity.
        - KPIs & Risks (Inform): Styled card grids. Goal: Present key metrics and potential issues in a digestible format. Interaction: None. Justification: Simple, clear presentation for important but static information. Method: HTML/Tailwind Grid.
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #FDFBF7;
            color: #2c3e50;
        }
        .canvas-card {
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .canvas-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 400px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }
        .active-filter {
            background-color: #27ae60 !important;
            color: white !important;
        }
        .timeline-item::before {
            content: '';
            position: absolute;
            top: 11px;
            left: -16px;
            width: 10px;
            height: 10px;
            background-color: #27ae60;
            border-radius: 50%;
            border: 2px solid #FDFBF7;
        }
        .timeline-line {
            position: absolute;
            left: -12px;
            top: 15px;
            bottom: 0;
            width: 2px;
            background-color: #e0e0e0;
        }
        .timeline-item:last-child .timeline-line {
            display: none;
        }
    </style>
</head>
<body class="antialiased">

    <header class="sticky top-0 bg-white/80 backdrop-blur-md shadow-sm z-50">
        <nav class="container mx-auto px-6 py-3 flex justify-between items-center">
            <h1 class="text-xl font-bold text-gray-800">Академія Продавця Rozetka</h1>
            <div class="hidden md:flex space-x-6">
                <a href="#business-model" class="text-gray-600 hover:text-green-600 transition">Бізнес-модель</a>
                <a href="#strategy" class="text-gray-600 hover:text-green-600 transition">Стратегія запуску</a>
                <a href="#kpi" class="text-gray-600 hover:text-green-600 transition">Ключові показники</a>
                <a href="#financials" class="text-gray-600 hover:text-green-600 transition">Фінанси</a>
            </div>
            <button id="mobile-menu-button" class="md:hidden text-gray-700 focus:outline-none">
                <span class="text-2xl">☰</span>
            </button>
        </nav>
        <div id="mobile-menu" class="hidden md:hidden px-6 pt-2 pb-4">
            <a href="#business-model" class="block py-2 text-gray-600 hover:text-green-600">Бізнес-модель</a>
            <a href="#strategy" class="block py-2 text-gray-600 hover:text-green-600">Стратегія запуску</a>
            <a href="#kpi" class="block py-2 text-gray-600 hover:text-green-600">Ключові показники</a>
            <a href="#financials" class="block py-2 text-gray-600 hover:text-green-600">Фінанси</a>
        </div>
    </header>

    <main class="container mx-auto px-6 py-12">
        <section id="hero" class="text-center mb-16">
            <h2 class="text-4xl md:text-5xl font-bold mb-4 text-gray-800">Інтерактивна Бізнес-Модель</h2>
            <p class="text-lg text-gray-600 max-w-3xl mx-auto">Дослідіть стратегічний план "Академії Продавця Rozetka" через візуальну та інтерактивну Business Model Canvas. Натисніть на будь-який блок, щоб зануритися в деталі.</p>
        </section>

        <section id="business-model" class="mb-20 scroll-mt-20">
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-5 gap-4">
                
                <div class="lg:col-span-1 md:col-span-1 space-y-4">
                    <div data-target="partners" class="canvas-card cursor-pointer bg-white p-4 rounded-lg shadow-md h-48 flex flex-col justify-center text-center border-l-4 border-orange-400">
                        <h3 class="font-bold text-lg">Ключові партнери</h3>
                        <p class="text-sm text-gray-500 mt-1">Стратегічні та екосистемні альянси</p>
                    </div>
                     <div data-target="activities" class="canvas-card cursor-pointer bg-white p-4 rounded-lg shadow-md h-48 flex flex-col justify-center text-center border-l-4 border-purple-400">
                        <h3 class="font-bold text-lg">Основні види діяльності</h3>
                        <p class="text-sm text-gray-500 mt-1">Ключові процеси для створення цінності</p>
                    </div>
                </div>

                <div class="lg:col-span-1 md:col-span-1 space-y-4">
                   <div data-target="resources" class="canvas-card cursor-pointer bg-white p-4 rounded-lg shadow-md h-48 flex flex-col justify-center text-center border-l-4 border-purple-400">
                        <h3 class="font-bold text-lg">Ключові ресурси</h3>
                        <p class="text-sm text-gray-500 mt-1">Найважливіші активи бізнесу</p>
                    </div>
                </div>

                <div class="lg:col-span-1 md:col-span-2">
                    <div data-target="propositions" class="canvas-card cursor-pointer bg-green-50 p-6 rounded-lg shadow-xl h-full flex flex-col justify-center text-center border-l-4 border-green-500">
                        <h3 class="font-bold text-2xl text-green-800">Ключові пропозиції</h3>
                        <p class="text-md text-gray-600 mt-2">Цінність, яку ми створюємо для клієнтів</p>
                    </div>
                </div>

                <div class="lg:col-span-1 md:col-span-1 space-y-4">
                    <div data-target="relationships" class="canvas-card cursor-pointer bg-white p-4 rounded-lg shadow-md h-48 flex flex-col justify-center text-center border-l-4 border-blue-400">
                        <h3 class="font-bold text-lg">Відносини з клієнтами</h3>
                        <p class="text-sm text-gray-500 mt-1">Як ми взаємодіємо з сегментами</p>
                    </div>
                     <div data-target="channels" class="canvas-card cursor-pointer bg-white p-4 rounded-lg shadow-md h-48 flex flex-col justify-center text-center border-l-4 border-blue-400">
                        <h3 class="font-bold text-lg">Канали</h3>
                        <p class="text-sm text-gray-500 mt-1">Точки контакту з клієнтами</p>
                    </div>
                </div>
                
                <div class="lg:col-span-1 md:col-span-1">
                     <div data-target="segments" class="canvas-card cursor-pointer bg-white p-4 rounded-lg shadow-md h-full flex flex-col justify-center text-center border-l-4 border-red-400">
                        <h3 class="font-bold text-lg">Сегменти клієнтів</h3>
                        <p class="text-sm text-gray-500 mt-1">Для кого ми створюємо цінність</p>
                    </div>
                </div>

                <div class="lg:col-span-2 md:col-span-1 mt-4">
                     <div data-target="costs" class="canvas-card cursor-pointer bg-white p-4 rounded-lg shadow-md h-32 flex flex-col justify-center text-center border-t-4 border-red-500">
                        <h3 class="font-bold text-lg">Структура витрат</h3>
                    </div>
                </div>
                 <div class="lg:col-span-3 md:col-span-1 mt-4">
                     <div data-target="revenue" class="canvas-card cursor-pointer bg-white p-4 rounded-lg shadow-md h-32 flex flex-col justify-center text-center border-t-4 border-green-500">
                        <h3 class="font-bold text-lg">Джерела доходу</h3>
                    </div>
                </div>
            </div>
        </section>
        
        <div id="details-container" class="space-y-16">
            <section id="segments" class="scroll-mt-20 p-8 bg-white rounded-lg shadow-lg">
                <h2 class="text-3xl font-bold mb-6 text-red-700">👥 Сегменти клієнтів</h2>
                <p class="text-lg text-gray-600 mb-6">Успіх Академії залежить від чіткого розуміння, що «продавець на Rozetka» — це не монолітна аудиторія. Ми виділяємо чотири ключові групи зі своїми унікальними потребами та викликами.</p>
                <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
                    <div class="border-l-4 border-red-300 pl-4">
                        <h3 class="font-bold text-xl">Підприємці-початківці</h3>
                        <p class="text-gray-600 mt-2">Індивідуальні продавці або мікрокоманди, що роблять перші кроки. Їхні головні бар'єри — страх невдачі, брак капіталу та знань.</p>
                    </div>
                    <div class="border-l-4 border-red-400 pl-4">
                        <h3 class="font-bold text-xl">МСБ у стагнації</h3>
                        <p class="text-gray-600 mt-2">Продавці, що досягли плато у зростанні. Вони стикаються з операційними проблемами та неефективною логістикою.</p>
                    </div>
                    <div class="border-l-4 border-red-500 pl-4">
                        <h3 class="font-bold text-xl">Великі підприємства/Бренди</h3>
                        <p class="text-gray-600 mt-2">Офіційні дистриб'ютори та виробники. Їхні виклики — інтеграція IT-систем, глибока аналітика та корпоративне навчання.</p>
                    </div>
                    <div class="border-l-4 border-red-600 pl-4">
                        <h3 class="font-bold text-xl">Нішеві спеціалісти</h3>
                        <p class="text-gray-600 mt-2">Продавці у вузьких категоріях (handmade, крафт). Потребують специфічних знань з просування унікальних товарів.</p>
                    </div>
                </div>
            </section>

            <section id="propositions" class="scroll-mt-20 p-8 bg-white rounded-lg shadow-lg">
                <h2 class="text-3xl font-bold mb-2 text-green-700">🎁 Ключові пропозиції</h2>
                <p class="text-lg text-gray-600 mb-6">Ми створюємо цільові продукти, що вирішують конкретні проблеми кожного сегмента. Оберіть сегмент, щоб побачити релевантні пропозиції.</p>
                <div id="segment-filters" class="flex flex-wrap gap-3 mb-8">
                    <button data-filter="all" class="px-4 py-2 bg-gray-200 text-gray-700 rounded-full hover:bg-gray-300 transition active-filter">Для всіх</button>
                    <button data-filter="beginner" class="px-4 py-2 bg-gray-200 text-gray-700 rounded-full hover:bg-gray-300 transition">Для початківців</button>
                    <button data-filter="smb" class="px-4 py-2 bg-gray-200 text-gray-700 rounded-full hover:bg-gray-300 transition">Для МСБ</button>
                    <button data-filter="brand" class="px-4 py-2 bg-gray-200 text-gray-700 rounded-full hover:bg-gray-300 transition">Для брендів</button>
                </div>
                <div id="propositions-list" class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <div class="proposition-card p-4 bg-green-50 rounded-lg border border-green-200" data-segment='["all", "beginner"]'>
                        <h3 class="font-bold text-xl">«Швидкий старт»</h3>
                        <p class="text-gray-600 mt-2">Покрокова програма від реєстрації до перших 10 замовлень.</p>
                    </div>
                    <div class="proposition-card p-4 bg-green-50 rounded-lg border border-green-200" data-segment='["all", "beginner"]'>
                        <h3 class="font-bold text-xl">«Безпека та впевненість»</h3>
                        <p class="text-gray-600 mt-2">Модулі про правила платформи, податки та уникнення блокувань.</p>
                    </div>
                    <div class="proposition-card p-4 bg-green-50 rounded-lg border border-green-200" data-segment='["all", "smb"]'>
                        <h3 class="font-bold text-xl">«Масштабування бізнесу»</h3>
                        <p class="text-gray-600 mt-2">Курси з автоматизації, оптимізації логістики та управління командою.</p>
                    </div>
                    <div class="proposition-card p-4 bg-green-50 rounded-lg border border-green-200" data-segment='["all", "smb"]'>
                        <h3 class="font-bold text-xl">«Збільшення маржинальності»</h3>
                        <p class="text-gray-600 mt-2">Стратегії ціноутворення та методи нецінової конкуренції.</p>
                    </div>
                    <div class="proposition-card p-4 bg-green-50 rounded-lg border border-green-200" data-segment='["all", "brand"]'>
                        <h3 class="font-bold text-xl">«Корпоративне навчання»</h3>
                        <p class="text-gray-600 mt-2">Індивідуальні навчальні програми для команд та сертифікація.</p>
                    </div>
                    <div class="proposition-card p-4 bg-green-50 rounded-lg border border-green-200" data-segment='["all", "brand"]'>
                        <h3 class="font-bold text-xl">«Аналітика та дані»</h3>
                        <p class="text-gray-600 mt-2">Доступ до розширених звітів та навчання роботі з даними.</p>
                    </div>
                    <div class="proposition-card p-4 bg-green-50 rounded-lg border border-green-200" data-segment='["all"]'>
                        <h3 class="font-bold text-xl">«Спільнота»</h3>
                        <p class="text-gray-600 mt-2">Закритий клуб продавців для обміну досвідом та нетворкінгу.</p>
                    </div>
                     <div class="proposition-card p-4 bg-green-50 rounded-lg border border-green-200" data-segment='["all"]'>
                        <h3 class="font-bold text-xl">«Актуальність»</h3>
                        <p class="text-gray-600 mt-2">Гарантія регулярного оновлення контенту відповідно до змін на Rozetka.</p>
                    </div>
                </div>
            </section>

            <section id="channels" class="scroll-mt-20 p-8 bg-white rounded-lg shadow-lg">
                <h2 class="text-3xl font-bold mb-6 text-blue-700">📡 Канали</h2>
                <p class="text-lg text-gray-600 mb-6">Ми використовуємо багатошарову стратегію, щоб досягати клієнтів та доставляти їм цінність через найбільш ефективні точки контакту.</p>
                <div class="grid md:grid-cols-3 gap-8">
                    <div>
                        <h3 class="font-semibold text-xl mb-3">Основний канал доступу</h3>
                        <p>Пряма інтеграція в екосистему Rozetka: банери, віджети та сповіщення в особистому кабінеті продавця.</p>
                    </div>
                    <div>
                        <h3 class="font-semibold text-xl mb-3">Маркетингові канали</h3>
                        <p>Email-маркетинг, контент-маркетинг (блог, YouTube), безкоштовні вебінари для залучення аудиторії.</p>
                    </div>
                    <div>
                        <h3 class="font-semibold text-xl mb-3">Канали доставки цінності</h3>
                        <p>LMS-платформа для курсів, живі онлайн-воркшопи, закриті спільноти в Telegram для неформального спілкування.</p>
                    </div>
                </div>
            </section>
            
            <section id="relationships" class="scroll-mt-20 p-8 bg-white rounded-lg shadow-lg">
                <h2 class="text-3xl font-bold mb-6 text-blue-700">🤝 Відносини з клієнтами</h2>
                <p class="text-lg text-gray-600 mb-6">Тип відносин відповідає очікуванням кожного сегмента та економічній доцільності, від повної автоматизації до персональної підтримки.</p>
                <ul class="space-y-4">
                    <li class="flex items-start">
                        <span class="text-green-500 text-2xl mr-4">✓</span>
                        <div><strong class="font-semibold">Автоматизоване самообслуговування:</strong> Для масового сегмента — база знань, чат-боти, онбординг-листи.</div>
                    </li>
                    <li class="flex items-start">
                        <span class="text-green-500 text-2xl mr-4">✓</span>
                        <div><strong class="font-semibold">Підтримка на базі спільноти:</strong> Для підписників — активні форуми, Q&A-сесії з експертами.</div>
                    </li>
                    <li class="flex items-start">
                        <span class="text-green-500 text-2xl mr-4">✓</span>
                        <div><strong class="font-semibold">Виділена персональна підтримка:</strong> Для корпоративних клієнтів — персональний менеджер.</div>
                    </li>
                </ul>
            </section>

            <section id="partners" class="scroll-mt-20 p-8 bg-white rounded-lg shadow-lg">
                <h2 class="text-3xl font-bold mb-6 text-orange-700">🔗 Ключові партнери</h2>
                <p class="text-lg text-gray-600 mb-6">Успіх Академії залежить від побудови сильної партнерської екосистеми, наріжним каменем якої є Rozetka.</p>
                <div class="grid md:grid-cols-2 gap-6">
                    <div class="bg-orange-50 p-4 rounded-lg">
                        <h3 class="font-bold text-xl">Стратегічний партнер: Rozetka</h3>
                        <p class="mt-2">Надає бренд, доступ до клієнтської бази, дані та можливість глибокої інтеграції.</p>
                    </div>
                    <div class="bg-orange-50 p-4 rounded-lg">
                        <h3 class="font-bold text-xl">Екосистемні партнери</h3>
                        <p class="mt-2">Логістичні оператори (Нова Пошта), фулфілмент-центри, маркетингові агенції.</p>
                    </div>
                    <div class="bg-orange-50 p-4 rounded-lg">
                        <h3 class="font-bold text-xl">Технологічні партнери</h3>
                        <p class="mt-2">Провайдери LMS-платформ, студії відеопродакшену, розробники аналітичного ПЗ.</p>
                    </div>
                    <div class="bg-orange-50 p-4 rounded-lg">
                        <h3 class="font-bold text-xl">Фінансові партнери</h3>
                        <p class="mt-2">Банки та фінтех-компанії для створення спільних програм кредитування продавців.</p>
                    </div>
                </div>
            </section>
            
            <section id="activities" class="scroll-mt-20 p-8 bg-white rounded-lg shadow-lg">
                <h2 class="text-3xl font-bold mb-6 text-purple-700">⚙️ Основні види діяльності</h2>
                <p class="text-lg text-gray-600 mb-6">Це ключові дії, які компанія повинна виконувати бездоганно для досягнення успіху.</p>
                <ul class="list-disc list-inside space-y-2 text-gray-700">
                    <li><b>Створення та курація контенту:</b> Розробка та постійне оновлення навчальних програм, відеолекцій, статей.</li>
                    <li><b>Управління технологічною платформою:</b> Забезпечення стабільної та зручної роботи LMS.</li>
                    <li><b>Маркетинг та продажі:</b> Залучення нових користувачів та конвертація їх у платних клієнтів.</li>
                    <li><b>Управління спільнотою:</b> Організація онлайн-подій, стимулювання дискусій, залучення експертів.</li>
                    <li><b>Управління партнерствами:</b> Підтримка та розвиток відносин з ключовими партнерами.</li>
                </ul>
            </section>

            <section id="resources" class="scroll-mt-20 p-8 bg-white rounded-lg shadow-lg">
                <h2 class="text-3xl font-bold mb-6 text-purple-700">💡 Ключові ресурси</h2>
                <p class="text-lg text-gray-600 mb-6">Найважливіші активи, необхідні для функціонування бізнес-моделі. Поєднання доступу до даних та створення контенту створює потужний конкурентний бар'єр.</p>
                <div class="grid md:grid-cols-2 gap-6">
                    <p><strong>Бренд та схвалення від Rozetka:</strong> Найцінніший і незамінний ресурс, що надає миттєву довіру.</p>
                    <p><strong>Власний контент та експерти-практики:</strong> Бібліотека унікальних, практично орієнтованих навчальних матеріалів.</p>
                    <p><strong>Технологічна платформа (LMS):</strong> Надійна та функціональна програмна інфраструктура.</p>
                    <p><strong>Доступ до даних Rozetka:</strong> Унікальна можливість створювати контент, що базується не на теорії, а на реальних даних.</p>
                </div>
            </section>

            <section id="financials" class="scroll-mt-20 mb-20">
                <div class="text-center mb-12">
                     <h2 class="text-4xl font-bold text-gray-800">Фінансова основа</h2>
                     <p class="text-lg text-gray-600 mt-2">Як проєкт заробляє гроші та на що їх витрачає.</p>
                </div>
                <div class="grid md:grid-cols-2 gap-12">
                    <div id="revenue" class="scroll-mt-20 p-8 bg-white rounded-lg shadow-lg">
                        <h3 class="text-2xl font-bold mb-6 text-green-700 text-center">💰 Джерела доходу</h3>
                        <div class="chart-container">
                            <canvas id="revenueChart"></canvas>
                        </div>
                        <ul class="mt-6 space-y-2 text-sm text-gray-600">
                            <li><b>Рівнева підписка (SaaS):</b> Основне джерело регулярного доходу.</li>
                            <li><b>Разові платежі:</b> Продаж окремих преміум-курсів та сертифікацій.</li>
                            <li><b>Корпоративні ліцензії:</b> Пакети для навчання команд великих клієнтів.</li>
                            <li><b>Freemium-модель:</b> Безкоштовний базовий контент для залучення.</li>
                            <li><b>Партнерський дохід:</b> Комісії від рекомендованих сервісів.</li>
                        </ul>
                    </div>
                    <div id="costs" class="scroll-mt-20 p-8 bg-white rounded-lg shadow-lg">
                        <h3 class="text-2xl font-bold mb-6 text-red-700 text-center">💸 Структура витрат</h3>
                        <div class="chart-container">
                            <canvas id="costsChart"></canvas>
                        </div>
                        <ul class="mt-6 space-y-2 text-sm text-gray-600">
                            <li><b>Заробітна плата команди:</b> Найбільша стаття постійних витрат (контент, маркетинг, розробка).</li>
                            <li><b>Виробництво контенту:</b> Гонорари експертам, послуги фрілансерів.</li>
                            <li><b>Маркетинг та реклама:</b> Бюджет на залучення клієнтів.</li>
                            <li><b>Підписки на ПЗ:</b> Платежі за LMS, CRM, сервіси email-маркетингу.</li>
                        </ul>
                    </div>
                </div>
            </section>

            <section id="strategy" class="scroll-mt-20 mb-20">
                <div class="text-center mb-12">
                     <h2 class="text-4xl font-bold text-gray-800">Стратегія запуску (MVP)</h2>
                     <p class="text-lg text-gray-600 mt-2">Ми пропонуємо поетапний підхід для мінімізації ризиків та прийняття рішень на основі даних. Натисніть на фазу, щоб дізнатися деталі.</p>
                </div>
                <div class="relative pl-4">
                    <div class="timeline-item relative pb-8">
                        <div class="timeline-line"></div>
                        <div class="timeline-content">
                            <button class="timeline-phase-button text-left w-full">
                                <h3 class="text-2xl font-bold text-green-700">Фаза 1: MVP (3-6 місяців)</h3>
                                <p class="text-gray-500">Валідація основної ціннісної пропозиції</p>
                            </button>
                            <div class="timeline-details hidden mt-4 pl-4 border-l-2 border-gray-200">
                                <p><strong>Ціль:</strong> Перевірити гіпотезу з мінімальними інвестиціями.</p>
                                <ul class="list-disc list-inside mt-2">
                                    <li>Сфокусуватися на сегменті «Підприємці-початківці».</li>
                                    <li>Створити один флагманський курс «Швидкий старт на Rozetka».</li>
                                    <li>Використовувати прості інструменти: вебінари в Zoom, спільнота в Telegram.</li>
                                    <li>Основний фокус — на зборі фідбеку та доведенні готовності клієнтів платити.</li>
                                </ul>
                            </div>
                        </div>
                    </div>
                    <div class="timeline-item relative pb-8">
                        <div class="timeline-line"></div>
                        <div class="timeline-content">
                            <button class="timeline-phase-button text-left w-full">
                                <h3 class="text-2xl font-bold text-green-700">Фаза 2: Масштабування (6-12 місяців)</h3>
                                <p class="text-gray-500">Побудова технологічної основи</p>
                            </button>
                            <div class="timeline-details hidden mt-4 pl-4 border-l-2 border-gray-200">
                                <p><strong>Ціль:</strong> Розширити продуктову лінійку та автоматизувати процеси.</p>
                                <ul class="list-disc list-inside mt-2">
                                    <li>Розробити та запустити власну LMS-платформу.</li>
                                    <li>Впровадити модель підписки.</li>
                                    <li>Додати курси для сегмента «МСБ у стагнації».</li>
                                    <li>Побудувати автоматизовану маркетингову воронку.</li>
                                </ul>
                            </div>
                        </div>
                    </div>
                    <div class="timeline-item relative">
                        <div class="timeline-line"></div>
                        <div class="timeline-content">
                            <button class="timeline-phase-button text-left w-full">
                                <h3 class="text-2xl font-bold text-green-700">Фаза 3: Зрілість (12+ місяців)</h3>
                                <p class="text-gray-500">Лідерство на ринку та розширення</p>
                            </button>
                            <div class="timeline-details hidden mt-4 pl-4 border-l-2 border-gray-200">
                                <p><strong>Ціль:</strong> Стати №1 та диверсифікувати доходи.</p>
                                <ul class="list-disc list-inside mt-2">
                                    <li>Запустити пропозиції для корпоративних клієнтів.</li>
                                    <li>Побудувати та монетизувати партнерську програму.</li>
                                    <li>Використовувати дані для створення персоналізованих навчальних траєкторій.</li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <section id="kpi" class="scroll-mt-20 p-8 bg-white rounded-lg shadow-lg">
                <h2 class="text-3xl font-bold mb-6 text-gray-800">📊 Ключові показники ефективності (KPI)</h2>
                <p class="text-lg text-gray-600 mb-8">Для об'єктивної оцінки ефективності моделі ми відстежуємо набір ключових показників у чотирьох основних напрямках.</p>
                <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
                    <div class="bg-gray-50 p-4 rounded-lg">
                        <h4 class="font-bold text-lg">Залучення</h4>
                        <ul class="text-sm mt-2 space-y-1 text-gray-600">
                            <li>Кількість нових реєстрацій</li>
                            <li>Вартість залучення клієнта (CAC)</li>
                        </ul>
                    </div>
                    <div class="bg-gray-50 p-4 rounded-lg">
                        <h4 class="font-bold text-lg">Активація</h4>
                        <ul class="text-sm mt-2 space-y-1 text-gray-600">
                            <li>% завершення курсів</li>
                            <li>Індекс залученості спільноти</li>
                            <li>Щомісячні активні користувачі (MAU)</li>
                        </ul>
                    </div>
                    <div class="bg-gray-50 p-4 rounded-lg">
                        <h4 class="font-bold text-lg">Дохід</h4>
                        <ul class="text-sm mt-2 space-y-1 text-gray-600">
                            <li>Щомісячний регулярний дохід (MRR)</li>
                            <li>Довічна цінність клієнта (LTV)</li>
                        </ul>
                    </div>
                    <div class="bg-green-100 p-4 rounded-lg border border-green-300">
                        <h4 class="font-bold text-lg text-green-800">Вплив на екосистему</h4>
                        <p class="text-sm mt-2 text-green-700"><strong>Головний KPI:</strong> Кореляція між проходженням курсів та зростанням продажів/рейтингу продавця.</p>
                    </div>
                </div>
            </section>
        </div>
    </main>

    <footer class="bg-gray-800 text-white mt-20">
        <div class="container mx-auto px-6 py-8 text-center">
            <p>&copy; 2024 Концепт "Академія Продавця Rozetka".</p>
            <p class="text-sm text-gray-400 mt-2">Цей інтерактивний додаток створено для демонстрації бізнес-моделі.</p>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function () {
            
            const mobileMenuButton = document.getElementById('mobile-menu-button');
            const mobileMenu = document.getElementById('mobile-menu');
            mobileMenuButton.addEventListener('click', () => {
                mobileMenu.classList.toggle('hidden');
            });

            document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                anchor.addEventListener('click', function (e) {
                    e.preventDefault();
                    const targetId = this.getAttribute('href');
                    const targetElement = document.querySelector(targetId);
                    if (targetElement) {
                        targetElement.scrollIntoView({
                            behavior: 'smooth'
                        });
                        if (mobileMenu.classList.contains('hidden') === false) {
                            mobileMenu.classList.add('hidden');
                        }
                    }
                });
            });

            document.querySelectorAll('.canvas-card').forEach(card => {
                card.addEventListener('click', function() {
                    const targetId = this.dataset.target;
                    const targetElement = document.getElementById(targetId);
                    if (targetElement) {
                        targetElement.scrollIntoView({ behavior: 'smooth' });
                    }
                });
            });

            const filterButtons = document.querySelectorAll('#segment-filters button');
            const propositionCards = document.querySelectorAll('#propositions-list .proposition-card');

            filterButtons.forEach(button => {
                button.addEventListener('click', function() {
                    const filter = this.dataset.filter;
                    
                    filterButtons.forEach(btn => btn.classList.remove('active-filter'));
                    this.classList.add('active-filter');

                    propositionCards.forEach(card => {
                        const segments = JSON.parse(card.dataset.segment);
                        if (filter === 'all' || segments.includes(filter)) {
                            card.style.display = 'block';
                        } else {
                            card.style.display = 'none';
                        }
                    });
                });
            });

            const timelineButtons = document.querySelectorAll('.timeline-phase-button');
            timelineButtons.forEach(button => {
                button.addEventListener('click', () => {
                    const details = button.nextElementSibling;
                    details.classList.toggle('hidden');
                });
            });

            const chartOptions = {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        position: 'bottom',
                        labels: {
                            padding: 15,
                            font: {
                                size: 12
                            }
                        }
                    }
                },
                cutout: '60%'
            };

            const revenueCtx = document.getElementById('revenueChart').getContext('2d');
            new Chart(revenueCtx, {
                type: 'doughnut',
                data: {
                    labels: ['Підписка (SaaS)', 'Разові платежі', 'Корпоративні ліцензії', 'Партнерський дохід'],
                    datasets: [{
                        label: 'Джерела доходу',
                        data: [45, 25, 20, 10],
                        backgroundColor: [
                            '#27ae60',
                            '#2ecc71',
                            '#1abc9c',
                            '#16a085'
                        ],
                        borderColor: '#FDFBF7',
                        borderWidth: 4
                    }]
                },
                options: chartOptions
            });

            const costsCtx = document.getElementById('costsChart').getContext('2d');
            new Chart(costsCtx, {
                type: 'doughnut',
                data: {
                    labels: ['Заробітна плата', 'Виробництво контенту', 'Маркетинг', 'Підписки на ПЗ'],
                    datasets: [{
                        label: 'Структура витрат',
                        data: [50, 20, 15, 15],
                        backgroundColor: [
                            '#c0392b',
                            '#e74c3c',
                            '#d35400',
                            '#f39c12'
                        ],
                        borderColor: '#FDFBF7',
                        borderWidth: 4
                    }]
                },
                options: chartOptions
            });
        });
    </script>
</body>
</html>
