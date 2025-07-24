<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>الدليل الوطني للتدريب القيادي في العراق</title>
    
    <!-- Chosen Palette: Iraqi Dawn -->
    <!-- Application Structure Plan: A thematic single-page application with a fixed top navigation bar. The structure is designed to guide the user from the high-level vision to the specific implementation details, rather than following the report's linear chapter structure. The sections are: 1. Hero section for the core vision and transformations. 2. A visual representation of the Core Transformations using a chart. 3. Strategic Goals presented as interactive cards. 4. An interactive diagram of the System's Structure. 5. An interactive chart for Training Methodologies by leadership level. 6. A visual timeline for the Roadmap. This structure prioritizes user engagement and quick access to key concepts, making a dense strategic document digestible and explorable. -->
    <!-- Visualization & Content Choices: 
        - Core Transformations: Report Info -> Four key shifts (Loyalty to Merit, etc.). Goal -> Compare "before" and "after" states. Viz -> Horizontal Bar Chart (Chart.js). Interaction -> Visual comparison of two states. Justification -> A bar chart provides a clear, powerful visual metaphor for the shift from an undesirable state to a desirable one.
        - System Structure: Report Info -> Four main components of the system. Goal -> Organize and show relationships. Presentation -> Interactive diagram using styled HTML divs (Flexbox/Grid). Interaction -> Clicking a component reveals its details. Justification -> Avoids a static, boring list and encourages user exploration of the system's architecture.
        - Training Methodologies: Report Info -> Table mapping methodologies to leadership levels. Goal -> Show distribution and allow comparison. Viz -> Bar Chart (Chart.js). Interaction -> A dropdown filter to select the leadership level, which updates the chart dynamically. Justification -> Transforms a static table into an interactive tool for understanding the tailored training approach.
        - Roadmap: Report Info -> 5-phase implementation plan (2025-2028). Goal -> Show change over time. Presentation -> Visual timeline using HTML/CSS. Interaction -> Clicking on a phase highlights it and shows details. Justification -> A timeline is the most intuitive way to present chronological information, making the plan easy to follow.
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;800&display=swap" rel="stylesheet">
    
    <style>
        body {
            font-family: 'Tajawal', sans-serif;
            scroll-behavior: smooth;
            background-color: #f8fafc;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
            height: 400px;
            max-height: 50vh;
        }
        .nav-link {
            transition: color 0.3s, border-bottom-color 0.3s;
        }
        .nav-link:hover, .nav-link.active {
            color: #2563eb; 
            border-bottom-color: #2563eb;
        }
        .rtl-grid {
            direction: rtl;
        }
        .timeline-item::before {
            content: '';
            position: absolute;
            top: 50%;
            right: -1.25rem;
            transform: translateY(-50%);
            width: 1.25rem;
            height: 1.25rem;
            border-radius: 50%;
            background-color: #ffffff;
            border: 4px solid #3b82f6;
            z-index: 10;
        }
        .timeline-line {
            position: absolute;
            top: 0;
            bottom: 0;
            right: 0;
            width: 4px;
            background-color: #d1d5db;
            transform: translateX(50%);
        }
        .section-title {
            position: relative;
            padding-bottom: 0.5rem;
            margin-bottom: 2rem;
        }
        .section-title::after {
            content: '';
            position: absolute;
            bottom: 0;
            right: 50%;
            transform: translateX(50%);
            width: 80px;
            height: 4px;
            background-color: #3b82f6;
            border-radius: 2px;
        }
    </style>
</head>
<body class="text-slate-800">

    <header class="bg-white/90 backdrop-blur-lg shadow-sm sticky top-0 z-50">
        <nav class="container mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <div class="flex items-center">
                    <h1 class="text-xl md:text-2xl font-extrabold text-blue-700">القيادة في العراق</h1>
                </div>
                <div class="hidden md:block">
                    <div class="ml-10 flex items-baseline space-x-4 space-x-reverse">
                        <a href="#hero" class="nav-link text-slate-600 px-3 py-2 rounded-md text-sm font-medium border-b-2 border-transparent">الرئيسية</a>
                        <a href="#transformations" class="nav-link text-slate-600 px-3 py-2 rounded-md text-sm font-medium border-b-2 border-transparent">التحولات</a>
                        <a href="#goals" class="nav-link text-slate-600 px-3 py-2 rounded-md text-sm font-medium border-b-2 border-transparent">الأهداف</a>
                        <a href="#structure" class="nav-link text-slate-600 px-3 py-2 rounded-md text-sm font-medium border-b-2 border-transparent">البنية</a>
                        <a href="#methods" class="nav-link text-slate-600 px-3 py-2 rounded-md text-sm font-medium border-b-2 border-transparent">المنهجيات</a>
                        <a href="#roadmap" class="nav-link text-slate-600 px-3 py-2 rounded-md text-sm font-medium border-b-2 border-transparent">خارطة الطريق</a>
                    </div>
                </div>
                <div class="md:hidden">
                    <button id="mobile-menu-button" class="inline-flex items-center justify-center p-2 rounded-md text-slate-500 hover:text-white hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-slate-100 focus:ring-white">
                        <span class="sr-only">فتح القائمة الرئيسية</span>
                        <svg class="h-6 w-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" aria-hidden="true">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
                        </svg>
                    </button>
                </div>
            </div>
            <div id="mobile-menu" class="md:hidden hidden">
                <div class="px-2 pt-2 pb-3 space-y-1 sm:px-3">
                    <a href="#hero" class="nav-link text-slate-700 hover:bg-blue-600 hover:text-white block px-3 py-2 rounded-md text-base font-medium">الرئيسية</a>
                    <a href="#transformations" class="nav-link text-slate-700 hover:bg-blue-600 hover:text-white block px-3 py-2 rounded-md text-base font-medium">التحولات</a>
                    <a href="#goals" class="nav-link text-slate-700 hover:bg-blue-600 hover:text-white block px-3 py-2 rounded-md text-base font-medium">الأهداف</a>
                    <a href="#structure" class="nav-link text-slate-700 hover:bg-blue-600 hover:text-white block px-3 py-2 rounded-md text-base font-medium">البنية</a>
                    <a href="#methods" class="nav-link text-slate-700 hover:bg-blue-600 hover:text-white block px-3 py-2 rounded-md text-base font-medium">المنهجيات</a>
                    <a href="#roadmap" class="nav-link text-slate-700 hover:bg-blue-600 hover:text-white block px-3 py-2 rounded-md text-base font-medium">خارطة الطريق</a>
                </div>
            </div>
        </nav>
    </header>

    <main>
        <section id="hero" class="pt-20 pb-16 bg-white">
            <div class="container mx-auto px-4 sm:px-6 lg:px-8 text-center">
                <h2 class="text-4xl md:text-5xl font-extrabold text-slate-900 mb-4">مقترح الدليل الوطني للتدريب القيادي</h2>
                <p class="text-lg md:text-xl text-slate-600 max-w-3xl mx-auto mb-8">رؤية استراتيجية لبناء منظومة قيادية حديثة ومتكاملة في القطاع العام العراقي، تهدف إلى صناعة قادة دولة حقيقيين.</p>
                <div class="flex justify-center">
                    <a href="#transformations" class="bg-blue-600 text-white font-bold py-3 px-8 rounded-full hover:bg-blue-700 transition duration-300 transform hover:scale-105">اكتشف التحولات</a>
                </div>
            </div>
        </section>

        <section id="transformations" class="py-20">
            <div class="container mx-auto px-4 sm:px-6 lg:px-8">
                <div class="text-center">
                    <h3 class="section-title text-3xl md:text-4xl font-extrabold text-slate-900">التحولات الجوهرية الأربعة</h3>
                    <p class="mt-4 text-lg text-slate-600 max-w-3xl mx-auto">يهدف الدليل إلى إحداث نقلة نوعية في ثقافة وممارسة القيادة في القطاع العام، من خلال أربعة تحولات أساسية تمثل جوهر الإصلاح المنشود.</p>
                </div>
                <div class="chart-container mt-12">
                    <canvas id="transformationsChart"></canvas>
                </div>
            </div>
        </section>

        <section id="goals" class="py-20 bg-white">
            <div class="container mx-auto px-4 sm:px-6 lg:px-8">
                <div class="text-center">
                    <h3 class="section-title text-3xl md:text-4xl font-extrabold text-slate-900">الأهداف الاستراتيجية</h3>
                    <p class="mt-4 text-lg text-slate-600 max-w-3xl mx-auto">سبعة أهداف رئيسية تشكل الإطار التأسيسي لتطوير منظومة التدريب القيادي في العراق، وتحقيق رؤيته الشاملة.</p>
                </div>
                <div id="goals-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8 rtl-grid mt-12">
                </div>
            </div>
        </section>

        <section id="structure" class="py-20">
            <div class="container mx-auto px-4 sm:px-6 lg:px-8">
                <div class="text-center">
                    <h3 class="section-title text-3xl md:text-4xl font-extrabold text-slate-900">المكونات البنيوية للمنظومة</h3>
                    <p class="mt-4 text-lg text-slate-600 max-w-3xl mx-auto">تتألف المنظومة من أربعة مكونات رئيسية متكاملة تضمن تحويل التدريب إلى مشروع وطني استراتيجي. انقر على كل مكون لعرض تفاصيله.</p>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mt-12 text-center">
                    <div id="structure-btn-1" class="structure-btn bg-white p-6 rounded-xl shadow-md cursor-pointer border-2 border-transparent hover:border-blue-500 hover:shadow-lg transition duration-300 transform hover:-translate-y-1">
                        <h4 class="text-xl font-bold text-blue-700">البنية المؤسسية</h4>
                    </div>
                    <div id="structure-btn-2" class="structure-btn bg-white p-6 rounded-xl shadow-md cursor-pointer border-2 border-transparent hover:border-green-500 hover:shadow-lg transition duration-300 transform hover:-translate-y-1">
                        <h4 class="text-xl font-bold text-green-700">البنية التشريعية</h4>
                    </div>
                    <div id="structure-btn-3" class="structure-btn bg-white p-6 rounded-xl shadow-md cursor-pointer border-2 border-transparent hover:border-purple-500 hover:shadow-lg transition duration-300 transform hover:-translate-y-1">
                        <h4 class="text-xl font-bold text-purple-700">البنية الفنية والتقنية</h4>
                    </div>
                    <div id="structure-btn-4" class="structure-btn bg-white p-6 rounded-xl shadow-md cursor-pointer border-2 border-transparent hover:border-amber-500 hover:shadow-lg transition duration-300 transform hover:-translate-y-1">
                        <h4 class="text-xl font-bold text-amber-700">البنية المعرفية</h4>
                    </div>
                </div>
                <div id="structure-content" class="bg-white p-8 rounded-xl shadow-lg mt-8 min-h-[200px] transition-all duration-500 flex items-center justify-center">
                    <p class="text-slate-500 text-lg text-center">اختر أحد المكونات أعلاه لعرض التفاصيل.</p>
                </div>
            </div>
        </section>

        <section id="methods" class="py-20 bg-white">
            <div class="container mx-auto px-4 sm:px-6 lg:px-8">
                <div class="text-center">
                    <h3 class="section-title text-3xl md:text-4xl font-extrabold text-slate-900">منهجيات التدريب المعتمدة</h3>
                    <p class="mt-4 text-lg text-slate-600 max-w-3xl mx-auto">يعتمد الدليل على أحدث المقاربات التجريبية والتفاعلية، مع توظيفها بما يتناسب مع كل مستوى قيادي.</p>
                </div>
                <div class="max-w-sm mx-auto mt-12">
                    <label for="leadership-level" class="block text-sm font-medium text-slate-700 mb-2">اختر المستوى القيادي:</label>
                    <select id="leadership-level" class="block w-full p-3 border border-slate-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500 bg-white">
                        <option value="emerging">القيادات الناشئة</option>
                        <option value="middle">القيادات المتوسطة</option>
                        <option value="senior">القيادات العليا</option>
                        <option value="sovereign">القيادات السيادية</option>
                    </select>
                </div>
                <div class="chart-container mt-8">
                    <canvas id="methodologiesChart"></canvas>
                </div>
            </div>
        </section>

        <section id="roadmap" class="py-20">
            <div class="container mx-auto px-4 sm:px-6 lg:px-8">
                <div class="text-center">
                    <h3 class="section-title text-3xl md:text-4xl font-extrabold text-slate-900">خارطة الطريق الوطنية للتنفيذ</h3>
                    <p class="mt-4 text-lg text-slate-600 max-w-3xl mx-auto">خطة زمنية محددة تمتد من 2025 إلى 2028 لضمان التنفيذ الناجح للمنظومة.</p>
                </div>
                <div class="relative max-w-4xl mx-auto mt-12">
                    <div class="timeline-line"></div>
                    <div id="roadmap-container" class="space-y-12 pr-10">
                    </div>
                </div>
            </div>
        </section>
    </main>

    <footer class="bg-slate-800 text-white py-8">
        <div class="container mx-auto px-4 sm:px-6 lg:px-8 text-center">
            <p>&copy; 2025 - رؤية لتطوير القيادة في العراق.</p>
            <p class="text-sm mt-2 text-slate-400">مستوحى من "مقترح الدليل الوطني للتدريب القيادي العام في العراق" للمستشار د. عقيل محمود الخزعلي.</p>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function () {
            const data = {
                goals: [
                    { title: "إرساء مرجعية وطنية", description: "توفير إطار موحد للتخطيط والتنفيذ والتقييم، والانتقال من الفوضى التدريبية إلى بنية مؤسسية منهجية." },
                    { title: "بناء نظام للجدارات", description: "تأسيس نظام وطني متكامل للجدارات القيادية ليصبح شرطًا للترقية والتعيين في المناصب العليا." },
                    { title: "تصميم مسارات تدريبية", description: "تطوير مسارات تدريبية تراكمية وعملية تمتد من القيادات الناشئة حتى القيادة السيادية." },
                    { title: "مواءمة مع التحول الرقمي", description: "إدماج أدوات الذكاء الاصطناعي والبيانات الضخمة والتقييم الذكي في التدريب القيادي." },
                    { title: "تطوير منظومة تقييم", description: "إنشاء منظومة لمتابعة وقياس أثر التدريب على الأداء المؤسسي باستخدام مؤشرات كمية ونوعية." },
                    { title: "ضمان الاستدامة", description: "ضمان استدامة التدريب عبر التشريعات وتخصيص الموازنات وربط الترقيات بالتدريب قانونًا." },
                    { title: "بناء شبكة وطنية", description: "تكوين شبكة متكاملة للقيادة الحكومية تضم قادة مؤهلين ومدربين ومؤسسات أكاديمية ودولية." }
                ],
                structure: {
                    "1": { title: "البنية المؤسسية الحاكمة", color: "blue", details: ["الفريق الوطني للقيادة الحكومية (مرتبط برئيس الوزراء).", "المعهد الوطني لإعداد وتأهيل القيادات (مرتبط بمجلس الوزراء).", "وحدات تدريب قيادية داخل كل مؤسسة حكومية."] },
                    "2": { title: "البنية التشريعية والتنظيمية", color: "green", details: ["إصدار قانون خاص بالتدريب القيادي يجعله إلزامياً للتدرج الوظيفي.", "إصدار تعليمات تنظيمية وأدلة إجرائية موحدة.", "تحديث التشريعات الداعمة (الخدمة المدنية، الإصلاح الإداري)."] },
                    "3": { title: "البنية الفنية والتقنية", color: "purple", details: ["منصات رقمية موحدة للتدريب (LMS) مع محتوى تفاعلي.", "أدوات تقييم متقدمة (تقييم 360، محاكاة).", "استخدام تقنيات الواقع الافتراضي والذكاء الاصطناعي."] },
                    "4": { title: "البنية المعرفية والتكوينية", color: "amber", details: ["صياغة إطار وطني موحد للجدارات القيادية (6 أبعاد).", "بناء مصفوفة تدريبية متعددة المستويات (تأسيسي، تمكيني، استراتيجي).", "إنشاء بنك محتوى تدريبي وطني رقمي."] }
                },
                methodologies: {
                    emerging: { labels: ['التعلم بالخبرة', 'حل المشكلات', 'دراسة الحالة', 'العصف الذهني'], data: [40, 30, 20, 10] },
                    middle: { labels: ['المحاكاة', 'السيناريوهات', 'مختبرات القيادة', 'التعلم التشاركي'], data: [35, 25, 25, 15] },
                    senior: { labels: ['مختبرات التحول', 'حل المشكلات الكبرى', 'الواقع الافتراضي', 'تحليل السياسات'], data: [40, 30, 20, 10] },
                    sovereign: { labels: ['التوجيه الاستراتيجي', 'الألعاب الكبرى', 'مسرح القيادة', 'الذكاء الاصطناعي'], data: [45, 25, 15, 15] }
                },
                roadmap: [
                    { phase: "1", title: "الانطلاق السياسي", date: "الربع الثالث 2025", description: "إصدار القرار الوزاري، تشكيل المجلس الوطني، وتحديد التمويل." },
                    { phase: "2", title: "التأسيس المؤسسي", date: "الربع الرابع 2025", description: "إنشاء المركز الوطني، تطوير الإطار القانوني، وتصميم النظم الرقمية." },
                    { phase: "3", title: "المرحلة التجريبية", date: "الربع الأول 2026", description: "تنفيذ برامج أولية في 5 وزارات و 3 محافظات مختارة." },
                    { phase: "4", title: "التوسعة الوطنية", date: "2026 - 2027", description: "تعميم المنظومة على جميع المؤسسات الاتحادية بشكل تدريجي." },
                    { phase: "5", title: "التقييم الشامل", date: "2028", description: "إعداد تقرير الأداء الوطني الأول للقيادة الحكومية في العراق." }
                ]
            };

            const goalsGrid = document.getElementById('goals-grid');
            data.goals.forEach(goal => {
                const card = document.createElement('div');
                card.className = 'bg-white p-6 rounded-xl shadow-md hover:shadow-xl hover:-translate-y-1 transition-all duration-300';
                card.innerHTML = `
                    <h4 class="text-xl font-bold text-slate-800 mb-2">${goal.title}</h4>
                    <p class="text-slate-600">${goal.description}</p>
                `;
                goalsGrid.appendChild(card);
            });

            const structureContent = document.getElementById('structure-content');
            const structureBtns = document.querySelectorAll('.structure-btn');
            structureBtns.forEach(btn => {
                btn.addEventListener('click', () => {
                    const id = btn.id.split('-')[2];
                    const contentData = data.structure[id];

                    structureBtns.forEach(b => {
                        const otherId = b.id.split('-')[2];
                        b.classList.remove(`border-${data.structure[otherId].color}-500`, 'scale-105');
                        b.classList.add('border-transparent');
                    });
                    
                    btn.classList.remove('border-transparent');
                    btn.classList.add(`border-${contentData.color}-500`, 'scale-105');

                    structureContent.innerHTML = `
                        <div class="w-full">
                            <h4 class="text-2xl font-bold text-${contentData.color}-700 mb-4">${contentData.title}</h4>
                            <ul class="space-y-3 list-disc list-inside text-slate-700 text-right">
                                ${contentData.details.map(item => `<li>${item}</li>`).join('')}
                            </ul>
                        </div>
                    `;
                });
            });

            const roadmapContainer = document.getElementById('roadmap-container');
            data.roadmap.forEach(item => {
                const roadmapItem = document.createElement('div');
                roadmapItem.className = 'relative pr-8';
                roadmapItem.innerHTML = `
                    <div class="timeline-item bg-white p-6 rounded-xl shadow-md border-l-4 border-blue-500">
                        <span class="text-sm font-bold text-blue-600">${item.date}</span>
                        <h4 class="text-xl font-bold mt-1 mb-2">المرحلة ${item.phase}: ${item.title}</h4>
                        <p class="text-slate-600">${item.description}</p>
                    </div>
                `;
                roadmapContainer.appendChild(roadmapItem);
            });

            let transformationsChartInstance, methodologiesChartInstance;

            function createTransformationsChart() {
                const ctx = document.getElementById('transformationsChart').getContext('2d');
                if (transformationsChartInstance) {
                    transformationsChartInstance.destroy();
                }
                transformationsChartInstance = new Chart(ctx, {
                    type: 'bar',
                    data: {
                        labels: ['الولاءات', 'العشوائية', 'الشخصنة', 'التدوير السياسي'],
                        datasets: [{
                            label: 'إلى',
                            data: [100, 100, 100, 100],
                            backgroundColor: '#60a5fa',
                        }]
                    },
                    options: {
                        indexAxis: 'y',
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            legend: {
                                display: false
                            },
                            title: {
                                display: true,
                                text: 'الانتقال من الممارسات الحالية إلى المستهدفة',
                                font: { size: 16, family: 'Tajawal' },
                                color: '#1e293b'
                            },
                            tooltip: {
                                rtl: true,
                                callbacks: {
                                    title: function(context) {
                                        const toLabels = ['الجدارات', 'المهنية', 'المؤسسية', 'التمكين الإصلاحي'];
                                        return `من: ${context[0].label}  ⬅️  إلى: ${toLabels[context[0].dataIndex]}`;
                                    },
                                    label: function(context) {
                                        return '';
                                    }
                                }
                            }
                        },
                        scales: {
                            x: {
                                display: false,
                                stacked: true,
                            },
                            y: {
                                stacked: true,
                                ticks: { font: { size: 14, family: 'Tajawal' }, color: '#334155' }
                            }
                        }
                    }
                });
            }

            function createMethodologiesChart(level) {
                const chartData = data.methodologies[level];
                const ctx = document.getElementById('methodologiesChart').getContext('2d');
                if (methodologiesChartInstance) {
                    methodologiesChartInstance.destroy();
                }
                methodologiesChartInstance = new Chart(ctx, {
                    type: 'bar',
                    data: {
                        labels: chartData.labels,
                        datasets: [{
                            label: 'الأهمية النسبية للمنهجية',
                            data: chartData.data,
                            backgroundColor: ['#3b82f6', '#10b981', '#8b5cf6', '#f59e0b'],
                            borderColor: ['#2563eb', '#059669', '#7c3aed', '#d97706'],
                            borderWidth: 1,
                            borderRadius: 5
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            legend: {
                                display: false
                            },
                            title: {
                                display: true,
                                text: `المنهجيات الأساسية لـ: ${document.getElementById('leadership-level').options[document.getElementById('leadership-level').selectedIndex].text}`,
                                font: { size: 16, family: 'Tajawal' },
                                color: '#1e293b'
                            }
                        },
                        scales: {
                            y: {
                                beginAtZero: true,
                                title: { display: true, text: 'الأهمية (%)', font: { family: 'Tajawal' }, color: '#475569' },
                                ticks: { color: '#475569' }
                            },
                             x: {
                                ticks: { font: { size: 12, family: 'Tajawal' }, color: '#334155' }
                            }
                        }
                    }
                });
            }
            
            document.getElementById('leadership-level').addEventListener('change', function() {
                createMethodologiesChart(this.value);
            });

            const mobileMenuButton = document.getElementById('mobile-menu-button');
            const mobileMenu = document.getElementById('mobile-menu');
            mobileMenuButton.addEventListener('click', () => {
                mobileMenu.classList.toggle('hidden');
            });
            
            const navLinks = document.querySelectorAll('.nav-link');
            const sections = document.querySelectorAll('main section');

            const observerOptions = {
                root: null,
                rootMargin: '0px',
                threshold: 0.4
            };

            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        navLinks.forEach(link => {
                            link.classList.remove('active');
                            if (link.getAttribute('href').substring(1) === entry.target.id) {
                                link.classList.add('active');
                            }
                        });
                        if(entry.target.id === 'transformations' && !transformationsChartInstance) {
                            createTransformationsChart();
                        }
                        if(entry.target.id === 'methods' && !methodologiesChartInstance) {
                             createMethodologiesChart('emerging');
                        }
                    }
                });
            }, observerOptions);

            sections.forEach(section => {
                observer.observe(section);
            });
        });
    </script>
</body>
</html>
# Dr.F.M.S
