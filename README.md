<!DOCTYPE html>
<html lang="ar" dir="rtl" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>محاسبي - المنصة المحاسبية المتخصصة الشاملة</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#f0fdf4',
                            100: '#dcfce7',
                            500: '#22c55e',
                            600: '#16a34a',
                            700: '#15803d',
                            900: '#14532d',
                        },
                        darkbg: '#0b0f19',
                        glass: 'rgba(17, 24, 39, 0.75)',
                        glassBorder: 'rgba(255, 255, 255, 0.08)'
                    },
                    fontFamily: {
                        sans: ['Tajawal', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <!-- Google Font: Tajawal -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700;800;900&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons CDN -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        body {
            font-family: 'Tajawal', sans-serif;
            background-color: #0b0f19;
            color: #f3f4f6;
            overflow-x: hidden;
        }

        .glass-panel {
            background: rgba(17, 24, 39, 0.75);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.08);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
        }

        .glass-card {
            background: rgba(31, 41, 55, 0.5);
            backdrop-filter: blur(8px);
            border: 1px solid rgba(255, 255, 255, 0.05);
            transition: all 0.3s ease;
        }

        .glass-card:hover {
            border-color: rgba(34, 197, 94, 0.4);
            transform: translateY(-2px);
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0b0f19;
        }
        ::-webkit-scrollbar-thumb {
            background: #1f2937;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #374151;
        }

        /* Print styles */
        @media print {
            body {
                background: white !important;
                color: black !important;
            }
            .no-print {
                display: none !important;
            }
            .print-only {
                display: block !important;
            }
            .glass-panel, .glass-card {
                background: white !important;
                border: 1px solid #ccc !important;
                box-shadow: none !important;
                color: black !important;
            }
            .text-gray-300, .text-gray-400, .text-gray-100 {
                color: #111 !important;
            }
        }
        .print-only {
            display: none;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between selection:bg-brand-500 selection:text-white">

    <div id="pinLockModal" class="fixed inset-0 z-50 flex items-center justify-center bg-darkbg/95 backdrop-blur-xl hidden">
        <div class="glass-panel p-8 rounded-3xl w-full max-w-md text-center space-y-6 border border-emerald-500/20 shadow-2xl relative overflow-hidden">
            <div class="absolute -top-10 -right-10 w-32 h-32 bg-emerald-500/10 rounded-full blur-2xl"></div>
            
            <div class="inline-flex p-4 rounded-2xl bg-emerald-500/10 text-emerald-400 text-3xl mb-2">
                <i class="fa-solid fa-user-lock"></i>
            </div>
            
            <div>
                <h2 class="text-2xl font-bold text-white mb-1">تطبيقات المحاسبة الآمنة</h2>
                <p class="text-xs text-emerald-400 font-medium">تطوير وإعداد المحاسب: براء نادر توفيق ناصر</p>
                <p class="text-sm text-gray-400 mt-3">أدخل رمز PIN المكون من 4 أرقام لفتح التطبيق</p>
            </div>

            <div class="flex justify-center gap-3 dir-ltr" id="pinDots">
                <div class="w-4 h-4 rounded-full border-2 border-emerald-500/50 dot"></div>
                <div class="w-4 h-4 rounded-full border-2 border-emerald-500/50 dot"></div>
                <div class="w-4 h-4 rounded-full border-2 border-emerald-500/50 dot"></div>
                <div class="w-4 h-4 rounded-full border-2 border-emerald-500/50 dot"></div>
            </div>

            <p id="pinErrorMsg" class="text-xs text-red-400 hidden font-semibold"></p>

            <div class="grid grid-cols-3 gap-3 max-w-xs mx-auto">
                <button onclick="appendPin('1')" class="py-3 text-xl font-bold rounded-xl glass-card text-white hover:bg-emerald-500/20 transition">1</button>
                <button onclick="appendPin('2')" class="py-3 text-xl font-bold rounded-xl glass-card text-white hover:bg-emerald-500/20 transition">2</button>
                <button onclick="appendPin('3')" class="py-3 text-xl font-bold rounded-xl glass-card text-white hover:bg-emerald-500/20 transition">3</button>
                <button onclick="appendPin('4')" class="py-3 text-xl font-bold rounded-xl glass-card text-white hover:bg-emerald-500/20 transition">4</button>
                <button onclick="appendPin('5')" class="py-3 text-xl font-bold rounded-xl glass-card text-white hover:bg-emerald-500/20 transition">5</button>
                <button onclick="appendPin('6')" class="py-3 text-xl font-bold rounded-xl glass-card text-white hover:bg-emerald-500/20 transition">6</button>
                <button onclick="appendPin('7')" class="py-3 text-xl font-bold rounded-xl glass-card text-white hover:bg-emerald-500/20 transition">7</button>
                <button onclick="appendPin('8')" class="py-3 text-xl font-bold rounded-xl glass-card text-white hover:bg-emerald-500/20 transition">8</button>
                <button onclick="appendPin('9')" class="py-3 text-xl font-bold rounded-xl glass-card text-white hover:bg-emerald-500/20 transition">9</button>
                <button onclick="clearPin()" class="py-3 text-sm font-semibold text-red-400 rounded-xl glass-card hover:bg-red-500/20 transition">مسح</button>
                <button onclick="appendPin('0')" class="py-3 text-xl font-bold rounded-xl glass-card text-white hover:bg-emerald-500/20 transition">0</button>
                <button onclick="verifyPin()" class="py-3 text-sm font-semibold text-emerald-400 rounded-xl glass-card hover:bg-emerald-500/20 transition">دخول</button>
            </div>
        </div>
    </div>

    <header class="no-print sticky top-0 z-40 glass-panel border-b border-gray-800">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3 flex flex-wrap justify-between items-center gap-4">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-2xl bg-gradient-to-tr from-emerald-600 to-emerald-400 flex items-center justify-center text-white text-xl shadow-lg shadow-emerald-500/20">
                    <i class="fa-solid fa-calculator"></i>
                </div>
                <div>
                    <div class="flex items-center gap-2">
                        <h1 class="text-xl font-extrabold text-white tracking-wide">محاسبي</h1>
                        <span id="headerActivityBadge" class="px-2.5 py-0.5 text-xs rounded-full bg-emerald-500/10 text-emerald-400 border border-emerald-500/20 font-medium">تجارة وتجزئة</span>
                    </div>
                    <p class="text-xs text-gray-400">تطوير وإعداد المحاسب: <span class="text-emerald-400 font-medium">براء نادر توفيق ناصر</span></p>
                </div>
            </div>

            <div class="flex items-center gap-2 flex-wrap">
                <button onclick="loadDemoData()" class="px-3 py-1.5 text-xs font-semibold rounded-xl bg-gradient-to-r from-emerald-600 to-teal-600 hover:from-emerald-500 hover:to-teal-500 text-white shadow-md shadow-emerald-600/20 flex items-center gap-1.5 transition">
                    <i class="fa-solid fa-wand-magic-sparkles"></i> تحميل بيانات تجريبية 🚀
                </button>
                <button onclick="window.print()" class="px-3 py-1.5 text-xs font-semibold rounded-xl glass-card text-gray-300 hover:text-white hover:bg-gray-800 flex items-center gap-1.5 transition">
                    <i class="fa-solid fa-print"></i> طباعة رسمية
                </button>
                <button onclick="lockAppManual()" class="px-3 py-1.5 text-xs font-semibold rounded-xl glass-card text-amber-400 hover:bg-amber-500/10 border-amber-500/20 flex items-center gap-1.5 transition">
                    <i class="fa-solid fa-lock"></i> قفل
                </button>
            </div>
        </div>
    </header>

    <div class="no-print bg-darkbg/80 border-b border-gray-800/80 sticky top-[65px] z-30 backdrop-blur-md">
        <div class="max-w-7xl mx-auto px-4 overflow-x-auto scrollbar-none">
            <nav class="flex space-x-1 space-x-reverse min-w-max py-2" id="mainTabs">
                <button onclick="switchTab('dashboard')" id="tab-dashboard" class="px-4 py-2 text-sm font-semibold rounded-xl text-emerald-400 bg-emerald-500/10 border border-emerald-500/20 flex items-center gap-2 transition">
                    <i class="fa-solid fa-chart-pie"></i> الملخص واللوحة
                </button>
                <button onclick="switchTab('transactions')" id="tab-transactions" class="px-4 py-2 text-sm font-semibold rounded-xl text-gray-400 hover:text-white hover:bg-gray-800 flex items-center gap-2 transition">
                    <i class="fa-solid fa-list-check"></i> القيود والمعاملات
                </button>
                <button onclick="switchTab('specialized')" id="tab-specialized" class="px-4 py-2 text-sm font-semibold rounded-xl text-gray-400 hover:text-white hover:bg-gray-800 flex items-center gap-2 transition">
                    <i class="fa-solid fa-briefcase"></i> <span id="specializedTabLabel">نشاطي المتخصص</span>
                </button>
                <button onclick="switchTab('assets')" id="tab-assets" class="px-4 py-2 text-sm font-semibold rounded-xl text-gray-400 hover:text-white hover:bg-gray-800 flex items-center gap-2 transition">
                    <i class="fa-solid fa-building-columns"></i> الأصول والإهلاك
                </button>
                <button onclick="switchTab('checks')" id="tab-checks" class="px-4 py-2 text-sm font-semibold rounded-xl text-gray-400 hover:text-white hover:bg-gray-800 flex items-center gap-2 transition">
                    <i class="fa-solid fa-money-check-dollar"></i> إدارة الشيكات
                </button>
                <button onclick="switchTab('equity')" id="tab-equity" class="px-4 py-2 text-sm font-semibold rounded-xl text-gray-400 hover:text-white hover:bg-gray-800 flex items-center gap-2 transition">
                    <i class="fa-solid fa-hand-holding-dollar"></i> المسحوبات والشركاء
                </button>
                <button onclick="switchTab('damaged')" id="tab-damaged" class="px-4 py-2 text-sm font-semibold rounded-xl text-gray-400 hover:text-white hover:bg-gray-800 flex items-center gap-2 transition">
                    <i class="fa-solid fa-box-archive"></i> الهالك والتالفيات
                </button>
                <button onclick="switchTab('reports')" id="tab-reports" class="px-4 py-2 text-sm font-semibold rounded-xl text-gray-400 hover:text-white hover:bg-gray-800 flex items-center gap-2 transition">
                    <i class="fa-solid fa-file-invoice-dollar"></i> القوائم والتقارير
                </button>
                <button onclick="switchTab('settings')" id="tab-settings" class="px-4 py-2 text-sm font-semibold rounded-xl text-gray-400 hover:text-white hover:bg-gray-800 flex items-center gap-2 transition">
                    <i class="fa-solid fa-gear"></i> الإعدادات والأمان
                </button>
            </nav>
        </div>
    </div>

    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 flex-1 w-full space-y-6">

        <!-- Header for Print mode only -->
        <div class="print-only mb-6 border-b pb-4 text-right">
            <div class="flex justify-between items-center">
                <div>
                    <h1 class="text-2xl font-bold text-black" id="printCompanyName">شركة الأعمال الحديثة</h1>
                    <p class="text-sm text-gray-700">تقرير المالي المحاسبي الشامل - القوائم السنوية / الشهرية</p>
                </div>
                <div class="text-left">
                    <p class="text-sm font-bold">إعداد وتطوير المحاسب: براء نادر توفيق ناصر</p>
                    <p class="text-xs text-gray-600">التاريخ: <span id="printDate"></span></p>
                </div>
            </div>
        </div>

        <!-- 1. DASHBOARD VIEW -->
        <section id="view-dashboard" class="space-y-6">
            <!-- Welcome Banner -->
            <div class="glass-panel p-6 rounded-3xl relative overflow-hidden flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
                <div class="space-y-1">
                    <div class="flex items-center gap-2">
                        <span class="text-2xl">👋</span>
                        <h2 class="text-2xl font-bold text-white">مرحباً بك في أداة "محاسبي" المتقدمة</h2>
                    </div>
                    <p class="text-sm text-gray-400">نظام محاسبي متخصص صُمم ليناسب نشاطك العملي بدقة وأمان عالي.</p>
                    <p class="text-xs text-emerald-400 font-semibold pt-1"><i class="fa-solid fa-certificate"></i> إعداد وتطوير المحاسب: براء نادر توفيق ناصر</p>
                </div>
                <div class="flex items-center gap-3 bg-gray-900/60 p-3 rounded-2xl border border-gray-800">
                    <div class="text-right">
                        <div class="text-xs text-gray-400">النشاط التجاري المفعّل</div>
                        <div id="dashActivityTitle" class="text-sm font-bold text-emerald-400">تجارة وتجزئة</div>
                    </div>
                    <button onclick="switchTab('settings')" class="p-2 rounded-xl glass-card text-xs text-gray-300 hover:text-white">
                        تغيير <i class="fa-solid fa-chevron-left mr-1"></i>
                    </button>
                </div>
            </div>

            <!-- KPI Cards -->
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                <div class="glass-panel p-5 rounded-2xl border-r-4 border-r-emerald-500">
                    <div class="flex justify-between items-center text-gray-400 mb-2">
                        <span class="text-xs font-semibold">إجمالي الإيرادات</span>
                        <i class="fa-solid fa-arrow-trend-up text-emerald-400"></i>
                    </div>
                    <div class="text-2xl font-extrabold text-white"><span id="dashIncome">0</span> <span class="currencySymbol text-sm font-normal text-emerald-400">USD</span></div>
                    <p class="text-xs text-gray-400 mt-2">من العمليات التشغيلية المباشرة</p>
                </div>

                <div class="glass-panel p-5 rounded-2xl border-r-4 border-r-red-500">
                    <div class="flex justify-between items-center text-gray-400 mb-2">
                        <span class="text-xs font-semibold">إجمالي المصاريف + الهالك</span>
                        <i class="fa-solid fa-arrow-trend-down text-red-400"></i>
                    </div>
                    <div class="text-2xl font-extrabold text-white"><span id="dashExpenses">0</span> <span class="currencySymbol text-sm font-normal text-red-400">USD</span></div>
                    <p class="text-xs text-gray-400 mt-2">تشمل مصاريف التشغيل والمواد التالفة</p>
                </div>

                <div class="glass-panel p-5 rounded-2xl border-r-4 border-r-blue-500">
                    <div class="flex justify-between items-center text-gray-400 mb-2">
                        <span class="text-xs font-semibold">صافي الربح قبل الضريبة</span>
                        <i class="fa-solid fa-scale-balanced text-blue-400"></i>
                    </div>
                    <div class="text-2xl font-extrabold text-white"><span id="dashNetProfit">0</span> <span class="currencySymbol text-sm font-normal text-blue-400">USD</span></div>
                    <p class="text-xs text-gray-400 mt-2" id="profitMarginText">هامش الربح: 0%</p>
                </div>

                <div class="glass-panel p-5 rounded-2xl border-r-4 border-r-purple-500">
                    <div class="flex justify-between items-center text-gray-400 mb-2">
                        <span class="text-xs font-semibold">صافي الأصول والسيولة</span>
                        <i class="fa-solid fa-vault text-purple-400"></i>
                    </div>
                    <div class="text-2xl font-extrabold text-white"><span id="dashAssetsVal">0</span> <span class="currencySymbol text-sm font-normal text-purple-400">USD</span></div>
                    <p class="text-xs text-gray-400 mt-2">القيمة الدفترية المتبقية للأصول</p>
                </div>
            </div>

            <!-- Quick Metrics Overview -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <div class="glass-card p-5 rounded-2xl space-y-3">
                    <h3 class="text-sm font-bold text-gray-200 flex items-center gap-2">
                        <i class="fa-solid fa-receipt text-emerald-400"></i> ملخص الضريبة المقدرة (<span id="dashTaxRate">16</span>%)
                    </h3>
                    <div class="flex justify-between items-center pt-2">
                        <span class="text-xs text-gray-400">ضريبة المبيعات/الإيراد:</span>
                        <span class="text-sm font-bold text-emerald-400" id="dashTaxVal">0</span>
                    </div>
                    <div class="text-xs text-gray-400">تُحتسب بناءً على الإيرادات المرفقة الخاضعة للضريبة.</div>
                </div>

                <div class="glass-card p-5 rounded-2xl space-y-3">
                    <h3 class="text-sm font-bold text-gray-200 flex items-center gap-2">
                        <i class="fa-solid fa-user-minus text-amber-400"></i> مسحوبات المالك والشركاء
                    </h3>
                    <div class="flex justify-between items-center pt-2">
                        <span class="text-xs text-gray-400">إجمالي المسحوبات الشخصية:</span>
                        <span class="text-sm font-bold text-amber-400" id="dashWithdrawalsVal">0</span>
                    </div>
                    <div class="text-xs text-gray-400">تُخصم مباشرة من حقوق الملكية ولا تعتبر مصاريف.</div>
                </div>

                <div class="glass-card p-5 rounded-2xl space-y-3">
                    <h3 class="text-sm font-bold text-gray-200 flex items-center gap-2">
                        <i class="fa-solid fa-money-check text-indigo-400"></i> معلقة بالشيكات
                    </h3>
                    <div class="flex justify-between items-center pt-2">
                        <span class="text-xs text-gray-400">شيكات برسم التحصيل:</span>
                        <span class="text-sm font-bold text-indigo-400" id="dashPendingChecksVal">0</span>
                    </div>
                    <div class="text-xs text-gray-400">مجموع الشيكات المقبوضة التي لم تُصرف بعد.</div>
                </div>
            </div>
        </section>

        <!-- 2. TRANSACTIONS VIEW -->
        <section id="view-transactions" class="space-y-6 hidden">
            <div class="glass-panel p-6 rounded-3xl space-y-6">
                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4">
                    <div>
                        <h2 class="text-xl font-bold text-white">دفتر القيود والمعاملات اليومية</h2>
                        <p class="text-xs text-gray-400">سجل الإيرادات والمصاريف اليومية مع حساب الضريبة تلقائياً</p>
                    </div>
                    <button onclick="openTransactionModal()" class="px-4 py-2 text-xs font-bold rounded-xl bg-emerald-600 hover:bg-emerald-500 text-white flex items-center gap-2 transition shadow-lg shadow-emerald-600/20">
                        <i class="fa-solid fa-plus"></i> إضافة قيد جديد
                    </button>
                </div>

                <!-- Filters -->
                <div class="flex flex-wrap gap-3 pt-2 border-t border-gray-800">
                    <input type="text" id="txSearch" oninput="renderTransactions()" placeholder="بحث في البيان أو التصنيف..." class="px-3 py-2 text-xs rounded-xl bg-gray-900 border border-gray-700 text-gray-200 focus:outline-none focus:border-emerald-500 w-full sm:w-64">
                    <select id="txFilterType" onchange="renderTransactions()" class="px-3 py-2 text-xs rounded-xl bg-gray-900 border border-gray-700 text-gray-200 focus:outline-none focus:border-emerald-500">
                        <option value="all">كل الأنواع</option>
                        <option value="income">إيرادات فقط</option>
                        <option value="expense">مصاريف فقط</option>
                    </select>
                </div>

                <!-- Table -->
                <div class="overflow-x-auto">
                    <table class="w-full text-right text-xs">
                        <thead>
                            <tr class="text-gray-400 border-b border-gray-800 bg-gray-900/40">
                                <th class="p-3">التاريخ</th>
                                <th class="p-3">النوع</th>
                                <th class="p-3">البيان / الوصف</th>
                                <th class="p-3">التصنيف</th>
                                <th class="p-3">المبلغ الصافي</th>
                                <th class="p-3">الضريبة المضافة</th>
                                <th class="p-3">الإجمالي</th>
                                <th class="p-3 text-center">إجراءات</th>
                            </tr>
                        </thead>
                        <tbody id="txTableBody" class="divide-y divide-gray-800/50">
                            <!-- JS Inject -->
                        </tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- 3. SPECIALIZED ACTIVITY HUB -->
        <section id="view-specialized" class="space-y-6 hidden">
            <!-- Dynamic Container based on active activity -->
            <div id="specializedContainer">
                <!-- Injected via JavaScript based on selected activity type -->
            </div>
        </section>

        <!-- 4. FIXED ASSETS & DEPRECIATION -->
        <section id="view-assets" class="space-y-6 hidden">
            <div class="glass-panel p-6 rounded-3xl space-y-6">
                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4">
                    <div>
                        <h2 class="text-xl font-bold text-white">الأصول الثابتة وحاسبة الإهلاك (Straight-line Depreciation)</h2>
                        <p class="text-xs text-gray-400">إدارة معدات، أجهزة، سيارات وعقارات المنشأة وحساب القسط الثابت سنوياً</p>
                    </div>
                    <button onclick="openAssetModal()" class="px-4 py-2 text-xs font-bold rounded-xl bg-emerald-600 hover:bg-emerald-500 text-white flex items-center gap-2 transition shadow-lg shadow-emerald-600/20">
                        <i class="fa-solid fa-plus"></i> إضافة أصل جديد
                    </button>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div class="glass-card p-4 rounded-2xl">
                        <div class="text-xs text-gray-400 mb-1">إجمالي تكلفة الشراء للأصول</div>
                        <div class="text-xl font-bold text-white"><span id="assetsTotalCost">0</span> <span class="currencySymbol text-xs text-emerald-400">USD</span></div>
                    </div>
                    <div class="glass-card p-4 rounded-2xl">
                        <div class="text-xs text-gray-400 mb-1">مجمع الإهلاك التراكمي المقدر</div>
                        <div class="text-xl font-bold text-amber-400"><span id="assetsAccDepreciation">0</span> <span class="currencySymbol text-xs">USD</span></div>
                    </div>
                    <div class="glass-card p-4 rounded-2xl">
                        <div class="text-xs text-gray-400 mb-1">صافي القيمة الدفترية الحالية</div>
                        <div class="text-xl font-bold text-emerald-400"><span id="assetsNetBookValue">0</span> <span class="currencySymbol text-xs">USD</span></div>
                    </div>
                </div>

                <div class="overflow-x-auto">
                    <table class="w-full text-right text-xs">
                        <thead>
                            <tr class="text-gray-400 border-b border-gray-800 bg-gray-900/40">
                                <th class="p-3">اسم الأصل</th>
                                <th class="p-3">تاريخ الشراء</th>
                                <th class="p-3">تكلفة الشراء</th>
                                <th class="p-3">قيمة النفاية (Salvage)</th>
                                <th class="p-3">العمر الإنتاجي (سنوات)</th>
                                <th class="p-3">الإهلاك السنوي</th>
                                <th class="p-3">القيمة الدفترية الحالية</th>
                                <th class="p-3 text-center">حذف</th>
                            </tr>
                        </thead>
                        <tbody id="assetsTableBody" class="divide-y divide-gray-800/50">
                            <!-- JS Inject -->
                        </tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- 5. CHECKS MANAGEMENT -->
        <section id="view-checks" class="space-y-6 hidden">
            <div class="glass-panel p-6 rounded-3xl space-y-6">
                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4">
                    <div>
                        <h2 class="text-xl font-bold text-white">إدارة متابعة الشيكات</h2>
                        <p class="text-xs text-gray-400">تسجيل وتتبع الشيكات المقبوضة، المحررة، والراجعة وتسويتها</p>
                    </div>
                    <button onclick="openCheckModal()" class="px-4 py-2 text-xs font-bold rounded-xl bg-emerald-600 hover:bg-emerald-500 text-white flex items-center gap-2 transition shadow-lg shadow-emerald-600/20">
                        <i class="fa-solid fa-plus"></i> إضافة شيك جديد
                    </button>
                </div>

                <div class="overflow-x-auto">
                    <table class="w-full text-right text-xs">
                        <thead>
                            <tr class="text-gray-400 border-b border-gray-800 bg-gray-900/40">
                                <th class="p-3">رقم الشيك</th>
                                <th class="p-3">النوع</th>
                                <th class="p-3">البنك والساحب/المستفيد</th>
                                <th class="p-3">المبلغ</th>
                                <th class="p-3">تاريخ الاستحقاق</th>
                                <th class="p-3">الحالة الحالية</th>
                                <th class="p-3 text-center">تغيير الحالة / إجراء</th>
                            </tr>
                        </thead>
                        <tbody id="checksTableBody" class="divide-y divide-gray-800/50">
                            <!-- JS Inject -->
                        </tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- 6. OWNER EQUITY & WITHDRAWALS -->
        <section id="view-equity" class="space-y-6 hidden">
            <div class="glass-panel p-6 rounded-3xl space-y-6">
                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4">
                    <div>
                        <h2 class="text-xl font-bold text-white">حقوق الملكية والمسحوبات الشخصية</h2>
                        <p class="text-xs text-gray-400">فصل مسحوبات المالك والشركاء عن المصاريف التشغيلية للمنشأة</p>
                    </div>
                    <button onclick="openWithdrawalModal()" class="px-4 py-2 text-xs font-bold rounded-xl bg-amber-600 hover:bg-amber-500 text-white flex items-center gap-2 transition shadow-lg shadow-amber-600/20">
                        <i class="fa-solid fa-hand-holding-dollar"></i> تسجيل مسحوبات للمالك
                    </button>
                </div>

                <div class="overflow-x-auto">
                    <table class="w-full text-right text-xs">
                        <thead>
                            <tr class="text-gray-400 border-b border-gray-800 bg-gray-900/40">
                                <th class="p-3">التاريخ</th>
                                <th class="p-3">اسم الشريك / المالك</th>
                                <th class="p-3">المبلغ المسحوب</th>
                                <th class="p-3">ملاحظات والسبب</th>
                                <th class="p-3 text-center">إجراء</th>
                            </tr>
                        </thead>
                        <tbody id="withdrawalsTableBody" class="divide-y divide-gray-800/50">
                            <!-- JS Inject -->
                        </tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- 7. DAMAGED GOODS & SCRAP -->
        <section id="view-damaged" class="space-y-6 hidden">
            <div class="glass-panel p-6 rounded-3xl space-y-6">
                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4">
                    <div>
                        <h2 class="text-xl font-bold text-white">تسجيل البضاعة التالفة والهالك</h2>
                        <p class="text-xs text-gray-400">حصر الخسائر الناتجة عن التلف، انتهاء الصلاحية، أو أخطاء التخزين وترحيلها كخسائر</p>
                    </div>
                    <button onclick="openDamagedModal()" class="px-4 py-2 text-xs font-bold rounded-xl bg-red-600 hover:bg-red-500 text-white flex items-center gap-2 transition shadow-lg shadow-red-600/20">
                        <i class="fa-solid fa-triangle-exclamation"></i> إثبات تلفيات / هالك
                    </button>
                </div>

                <div class="overflow-x-auto">
                    <table class="w-full text-right text-xs">
                        <thead>
                            <tr class="text-gray-400 border-b border-gray-800 bg-gray-900/40">
                                <th class="p-3">التاريخ</th>
                                <th class="p-3">الصنف / المادة</th>
                                <th class="p-3">الكمية التالفة</th>
                                <th class="p-3">تكلفة الوحدة</th>
                                <th class="p-3">إجمالي الخسارة</th>
                                <th class="p-3">سبب التلف</th>
                                <th class="p-3 text-center">إجراء</th>
                            </tr>
                        </thead>
                        <tbody id="damagedTableBody" class="divide-y divide-gray-800/50">
                            <!-- JS Inject -->
                        </tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- 8. FINANCIAL REPORTS & STATEMENTS -->
        <section id="view-reports" class="space-y-6 hidden">
            <div class="glass-panel p-6 rounded-3xl space-y-6">
                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4">
                    <div>
                        <h2 class="text-xl font-bold text-white">التقارير والقوائم المالية الختامية</h2>
                        <p class="text-xs text-gray-400">عرض قائمة الدخل والميزانية العمومية المختصرة مع جاهزية كاملة للطباعة والتصدير</p>
                    </div>
                    <button onclick="window.print()" class="px-4 py-2 text-xs font-bold rounded-xl bg-blue-600 hover:bg-blue-500 text-white flex items-center gap-2 transition">
                        <i class="fa-solid fa-print"></i> طباعة القوائم رسمياً
                    </button>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- Income Statement -->
                    <div class="glass-card p-5 rounded-2xl space-y-4">
                        <div class="border-b border-gray-700 pb-2 flex justify-between items-center">
                            <h3 class="text-base font-bold text-emerald-400"><i class="fa-solid fa-file-invoice"></i> قائمة الدخل (Income Statement)</h3>
                            <span class="text-xs text-gray-400">عن الفترة المحددة</span>
                        </div>
                        <div class="space-y-2 text-xs">
                            <div class="flex justify-between py-1 border-b border-gray-800">
                                <span class="text-gray-300">إجمالي المبيعات / الإيرادات:</span>
                                <span class="font-bold text-emerald-400" id="repIncome">0</span>
                            </div>
                            <div class="flex justify-between py-1 border-b border-gray-800">
                                <span class="text-gray-300">يُخصم: المصاريف التشغيلية:</span>
                                <span class="font-bold text-red-400" id="repExpenses">0</span>
                            </div>
                            <div class="flex justify-between py-1 border-b border-gray-800">
                                <span class="text-gray-300">يُخصم: خسائر البضاعة التالفة:</span>
                                <span class="font-bold text-red-400" id="repDamaged">0</span>
                            </div>
                            <div class="flex justify-between py-1 border-b border-gray-800">
                                <span class="text-gray-300">يُخصم: إهلاك الأصول السنوي المقدر:</span>
                                <span class="font-bold text-amber-400" id="repDepreciations">0</span>
                            </div>
                            <div class="flex justify-between py-2 font-extrabold text-sm border-t-2 border-emerald-500/40 pt-2">
                                <span class="text-white">صافي الربح / الخسارة التشغيلية:</span>
                                <span class="text-emerald-400" id="repNetProfit">0</span>
                            </div>
                        </div>
                    </div>

                    <!-- Balance Sheet Overview -->
                    <div class="glass-card p-5 rounded-2xl space-y-4">
                        <div class="border-b border-gray-700 pb-2 flex justify-between items-center">
                            <h3 class="text-base font-bold text-blue-400"><i class="fa-solid fa-scale-balanced"></i> ملخص المركز المالي (Balance Sheet)</h3>
                            <span class="text-xs text-gray-400">تقديري</span>
                        </div>
                        <div class="space-y-2 text-xs">
                            <div class="flex justify-between py-1 border-b border-gray-800">
                                <span class="text-gray-300">القيمة الدفترية للأصول الثابتة:</span>
                                <span class="font-bold text-blue-400" id="repAssetsBookVal">0</span>
                            </div>
                            <div class="flex justify-between py-1 border-b border-gray-800">
                                <span class="text-gray-300">شيكات برسم التحصيل (أصول متداولة):</span>
                                <span class="font-bold text-indigo-400" id="repPendingChecks">0</span>
                            </div>
                            <div class="flex justify-between py-1 border-b border-gray-800">
                                <span class="text-gray-300">إجمالي المسحوبات الشخصية للمالك:</span>
                                <span class="font-bold text-amber-400" id="repOwnerWithdrawals">0</span>
                            </div>
                            <div class="flex justify-between py-2 font-extrabold text-sm border-t-2 border-blue-500/40 pt-2">
                                <span class="text-white">صافي حقوق الملكية + الأصول:</span>
                                <span class="text-blue-400" id="repTotalEquity">0</span>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Footer note on reports -->
                <div class="text-center pt-4 border-t border-gray-800 text-xs text-gray-400">
                    تم توليد هذا التقرير تلقائياً عبر نظام <strong class="text-white">محاسبي</strong> | تطوير وإعداد المحاسب: <strong class="text-emerald-400">براء نادر توفيق ناصر</strong>
                </div>
            </div>
        </section>

        <!-- 9. SETTINGS & SECURITY VIEW -->
        <section id="view-settings" class="space-y-6 hidden">
            <div class="glass-panel p-6 rounded-3xl space-y-6">
                <div>
                    <h2 class="text-xl font-bold text-white">مركز الإعدادات المتطور والأمان</h2>
                    <p class="text-xs text-gray-400">إدارة رمز الأمان، التنسيق، نوع النشاط، والنسخ الاحتياطي</p>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- Security PIN Settings -->
                    <div class="glass-card p-5 rounded-2xl space-y-4">
                        <h3 class="text-sm font-bold text-white flex items-center gap-2">
                            <i class="fa-solid fa-shield-halved text-emerald-400"></i> حماية التطبيق بـ PIN Code
                        </h3>
                        <p class="text-xs text-gray-400">تفعيل رمز أمان مكون من 4 أرقام يمنع غير المصرح لهم من فتح واستعراض بياناتك المالية.</p>
                        
                        <div class="space-y-3 pt-2">
                            <div class="flex items-center justify-between">
                                <span class="text-xs text-gray-300">حالة رمز القفل:</span>
                                <span id="pinStatusBadge" class="px-2.5 py-0.5 text-xs rounded-full bg-red-500/10 text-red-400 border border-red-500/20">غير مفعّل</span>
                            </div>
                            <div class="flex gap-2">
                                <input type="password" id="newPinInput" maxlength="4" placeholder="أدخل 4 أرقام" class="px-3 py-2 text-xs rounded-xl bg-gray-900 border border-gray-700 text-white w-full focus:outline-none focus:border-emerald-500 text-center tracking-widest">
                                <button onclick="savePinSetting()" class="px-4 py-2 text-xs font-bold rounded-xl bg-emerald-600 hover:bg-emerald-500 text-white transition whitespace-nowrap">حفظ PIN</button>
                                <button onclick="removePinSetting()" class="px-3 py-2 text-xs font-bold rounded-xl bg-red-600/20 text-red-400 hover:bg-red-600/30 transition whitespace-nowrap">إلغاء</button>
                            </div>
                        </div>
                    </div>

                    <!-- General Accounting Settings -->
                    <div class="glass-card p-5 rounded-2xl space-y-4">
                        <h3 class="text-sm font-bold text-white flex items-center gap-2">
                            <i class="fa-solid fa-sliders text-blue-400"></i> إعدادات المنشأة والعملة
                        </h3>
                        <div class="space-y-3">
                            <div>
                                <label class="text-xs text-gray-300 block mb-1">اسم الشركة / المنشأة</label>
                                <input type="text" id="settingCompanyName" onchange="updateGeneralSettings()" class="w-full px-3 py-2 text-xs rounded-xl bg-gray-900 border border-gray-700 text-white focus:outline-none focus:border-emerald-500">
                            </div>
                            <div class="grid grid-cols-2 gap-3">
                                <div>
                                    <label class="text-xs text-gray-300 block mb-1">العملة الرئيسية</label>
                                    <select id="settingCurrency" onchange="updateGeneralSettings()" class="w-full px-3 py-2 text-xs rounded-xl bg-gray-900 border border-gray-700 text-white focus:outline-none focus:border-emerald-500">
                                        <option value="USD">دولار أمريكي (USD)</option>
                                        <option value="JOD">دينار أردني (JOD)</option>
                                        <option value="ILS">شيقل جديد (ILS)</option>
                                        <option value="SAR">ريال سعودي (SAR)</option>
                                        <option value="AED">درهم إماراتي (AED)</option>
                                        <option value="EGP">جنيه مصري (EGP)</option>
                                    </select>
                                </div>
                                <div>
                                    <label class="text-xs text-gray-300 block mb-1">نسبة الضريبة (%)</label>
                                    <input type="number" id="settingTaxRate" onchange="updateGeneralSettings()" class="w-full px-3 py-2 text-xs rounded-xl bg-gray-900 border border-gray-700 text-white focus:outline-none focus:border-emerald-500">
                                </div>
                            </div>
                            <div>
                                <label class="text-xs text-gray-300 block mb-1">تغيير نوع النشاط التجاري المتخصص</label>
                                <select id="settingActivityType" onchange="changeActivityType(this.value)" class="w-full px-3 py-2 text-xs rounded-xl bg-gray-900 border border-gray-700 text-emerald-400 font-bold focus:outline-none focus:border-emerald-500">
                                    <option value="retail">تجارة وتجزئة (Retail & Trade)</option>
                                    <option value="real_estate">عقارات ومخازن (Real Estate & Storage)</option>
                                    <option value="services">خدمات واستشارات (Services & Consulting)</option>
                                    <option value="restaurant">مطاعم وأغذية (Restaurants & Food)</option>
                                    <option value="manufacturing">تصنيع وإنتاج (Manufacturing)</option>
                                </select>
                            </div>
                        </div>
                    </div>

                    <!-- Data Backup & Restore -->
                    <div class="glass-card p-5 rounded-2xl space-y-4">
                        <h3 class="text-sm font-bold text-white flex items-center gap-2">
                            <i class="fa-solid fa-database text-purple-400"></i> النسخ الاحتياطي والاستعادة (JSON)
                        </h3>
                        <p class="text-xs text-gray-400">حفظ كافة بياناتك وقيدك في ملف خارجي أمان أو استرجاعها بضغطة زر واحدة.</p>
                        <div class="flex gap-3">
                            <button onclick="exportDataJSON()" class="px-4 py-2 text-xs font-bold rounded-xl bg-purple-600 hover:bg-purple-500 text-white transition flex-1 flex items-center justify-center gap-2">
                                <i class="fa-solid fa-download"></i> تصدير نسخة احتياطية
                            </button>
                            <label class="px-4 py-2 text-xs font-bold rounded-xl bg-gray-800 hover:bg-gray-700 text-gray-200 transition flex-1 flex items-center justify-center gap-2 cursor-pointer">
                                <i class="fa-solid fa-upload"></i> استعادة من ملف
                                <input type="file" id="importJsonInput" accept=".json" onchange="importDataJSON(event)" class="hidden">
                            </label>
                        </div>
                    </div>

                    <!-- Reset Data Safe Zone -->
                    <div class="glass-card p-5 rounded-2xl space-y-4 border-red-500/20">
                        <h3 class="text-sm font-bold text-red-400 flex items-center gap-2">
                            <i class="fa-solid fa-trash-arrow-up"></i> منطقة الخطر وإعادة التعيين
                        </h3>
                        <p class="text-xs text-gray-400">مسح جميع البيانات المسجلة والعودة إلى الإعدادات الأولية.</p>
                        <button onclick="resetAllDataModal()" class="px-4 py-2 text-xs font-bold rounded-xl bg-red-600/20 text-red-400 hover:bg-red-600 hover:text-white transition w-full">
                            تصفير وإعادة تعيين كافة البيانات
                        </button>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- MODALS CONTAINER -->
    <!-- 1. Transaction Add Modal -->
    <div id="txModal" class="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-md hidden">
        <div class="glass-panel p-6 rounded-3xl w-full max-w-md space-y-4 border border-gray-700">
            <h3 class="text-base font-bold text-white flex justify-between items-center">
                <span>إضافة قيد محاسبي جديد</span>
                <button onclick="closeModal('txModal')" class="text-gray-400 hover:text-white">&times;</button>
            </h3>
            <form id="txForm" onsubmit="handleSaveTx(event)" class="space-y-3 text-xs">
                <div>
                    <label class="text-gray-300 block mb-1">نوع القيد</label>
                    <select id="txType" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                        <option value="income">إيراد (+) (مبيعات / تحصيل)</option>
                        <option value="expense">مصروف (-) (تشغيلي / إداري)</option>
                    </select>
                </div>
                <div>
                    <label class="text-gray-300 block mb-1">البيان / الوصف</label>
                    <input type="text" id="txDesc" required placeholder="مثال: فاتورة مبيعات بضاعة" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                </div>
                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="text-gray-300 block mb-1">المبلغ (غير شامل الضريبة)</label>
                        <input type="number" step="0.01" id="txAmount" required placeholder="0.00" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                    </div>
                    <div>
                        <label class="text-gray-300 block mb-1">التصنيف</label>
                        <input type="text" id="txCategory" placeholder="مبيعات، إيجار، أدوات..." class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                    </div>
                </div>
                <div class="flex items-center gap-2 pt-1">
                    <input type="checkbox" id="txTaxable" checked class="rounded bg-gray-900 border-gray-700 text-emerald-500">
                    <label for="txTaxable" class="text-gray-300">خاضع لضريبة القيمة المضافة (<span class="taxRateDisplay">16</span>%)</label>
                </div>
                <div class="pt-3 flex gap-2">
                    <button type="submit" class="w-full py-2.5 text-xs font-bold rounded-xl bg-emerald-600 hover:bg-emerald-500 text-white transition">حفظ القيد</button>
                    <button type="button" onclick="closeModal('txModal')" class="w-full py-2.5 text-xs font-bold rounded-xl bg-gray-800 text-gray-300 hover:bg-gray-700 transition">إلغاء</button>
                </div>
            </form>
        </div>
    </div>

    <!-- 2. Asset Add Modal -->
    <div id="assetModal" class="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-md hidden">
        <div class="glass-panel p-6 rounded-3xl w-full max-w-md space-y-4 border border-gray-700">
            <h3 class="text-base font-bold text-white flex justify-between items-center">
                <span>إضافة أصل ثابت جديد</span>
                <button onclick="closeModal('assetModal')" class="text-gray-400 hover:text-white">&times;</button>
            </h3>
            <form id="assetForm" onsubmit="handleSaveAsset(event)" class="space-y-3 text-xs">
                <div>
                    <label class="text-gray-300 block mb-1">اسم الأصل / المعدات</label>
                    <input type="text" id="assetName" required placeholder="مثال: سيارة توصيل، ماكينة قهوة" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                </div>
                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="text-gray-300 block mb-1">تكلفة الشراء الأصلية</label>
                        <input type="number" step="0.01" id="assetCost" required placeholder="0.00" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                    </div>
                    <div>
                        <label class="text-gray-300 block mb-1">قيمة النفاية (Salvage)</label>
                        <input type="number" step="0.01" id="assetSalvage" value="0" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                    </div>
                </div>
                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="text-gray-300 block mb-1">العمر الإنتاجي (سنوات)</label>
                        <input type="number" id="assetLifespan" value="5" required class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                    </div>
                    <div>
                        <label class="text-gray-300 block mb-1">تاريخ الشراء</label>
                        <input type="date" id="assetDate" required class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                    </div>
                </div>
                <div class="pt-3 flex gap-2">
                    <button type="submit" class="w-full py-2.5 text-xs font-bold rounded-xl bg-emerald-600 hover:bg-emerald-500 text-white transition">حفظ الأصل</button>
                    <button type="button" onclick="closeModal('assetModal')" class="w-full py-2.5 text-xs font-bold rounded-xl bg-gray-800 text-gray-300 hover:bg-gray-700 transition">إلغاء</button>
                </div>
            </form>
        </div>
    </div>

    <!-- 3. Check Add Modal -->
    <div id="checkModal" class="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-md hidden">
        <div class="glass-panel p-6 rounded-3xl w-full max-w-md space-y-4 border border-gray-700">
            <h3 class="text-base font-bold text-white flex justify-between items-center">
                <span>تسجيل شيك جديد</span>
                <button onclick="closeModal('checkModal')" class="text-gray-400 hover:text-white">&times;</button>
            </h3>
            <form id="checkForm" onsubmit="handleSaveCheck(event)" class="space-y-3 text-xs">
                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="text-gray-300 block mb-1">رقم الشيك</label>
                        <input type="text" id="chkNumber" required placeholder="100234" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                    </div>
                    <div>
                        <label class="text-gray-300 block mb-1">نوع الشيك</label>
                        <select id="chkType" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                            <option value="received">مقبوض (لصالح المنشأة)</option>
                            <option value="issued">محرر (على المنشأة)</option>
                        </select>
                    </div>
                </div>
                <div>
                    <label class="text-gray-300 block mb-1">البنك والساحب / المستفيد</label>
                    <input type="text" id="chkPayee" required placeholder="بنك فلسطين - شركة السلام" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                </div>
                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="text-gray-300 block mb-1">المبلغ</label>
                        <input type="number" step="0.01" id="chkAmount" required placeholder="0.00" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                    </div>
                    <div>
                        <label class="text-gray-300 block mb-1">تاريخ الاستحقاق</label>
                        <input type="date" id="chkDueDate" required class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                    </div>
                </div>
                <div class="pt-3 flex gap-2">
                    <button type="submit" class="w-full py-2.5 text-xs font-bold rounded-xl bg-emerald-600 hover:bg-emerald-500 text-white transition">حفظ الشيك</button>
                    <button type="button" onclick="closeModal('checkModal')" class="w-full py-2.5 text-xs font-bold rounded-xl bg-gray-800 text-gray-300 hover:bg-gray-700 transition">إلغاء</button>
                </div>
            </form>
        </div>
    </div>

    <!-- 4. Owner Withdrawal Modal -->
    <div id="withdrawalModal" class="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-md hidden">
        <div class="glass-panel p-6 rounded-3xl w-full max-w-md space-y-4 border border-gray-700">
            <h3 class="text-base font-bold text-white flex justify-between items-center">
                <span>تسجيل مسحوبات شريك / مالك</span>
                <button onclick="closeModal('withdrawalModal')" class="text-gray-400 hover:text-white">&times;</button>
            </h3>
            <form id="withdrawalForm" onsubmit="handleSaveWithdrawal(event)" class="space-y-3 text-xs">
                <div>
                    <label class="text-gray-300 block mb-1">اسم المالك / الشريك</label>
                    <input type="text" id="wdPartner" required placeholder="مثال: براء ناصر" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                </div>
                <div>
                    <label class="text-gray-300 block mb-1">المبلغ المسحوب</label>
                    <input type="number" step="0.01" id="wdAmount" required placeholder="0.00" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                </div>
                <div>
                    <label class="text-gray-300 block mb-1">سبب السحب / ملاحظات</label>
                    <input type="text" id="wdNotes" placeholder="سحب شخصي نقدية" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                </div>
                <div class="pt-3 flex gap-2">
                    <button type="submit" class="w-full py-2.5 text-xs font-bold rounded-xl bg-amber-600 hover:bg-amber-500 text-white transition">حفظ القيد</button>
                    <button type="button" onclick="closeModal('withdrawalModal')" class="w-full py-2.5 text-xs font-bold rounded-xl bg-gray-800 text-gray-300 hover:bg-gray-700 transition">إلغاء</button>
                </div>
            </form>
        </div>
    </div>

    <!-- 5. Damaged Goods Modal -->
    <div id="damagedModal" class="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-md hidden">
        <div class="glass-panel p-6 rounded-3xl w-full max-w-md space-y-4 border border-gray-700">
            <h3 class="text-base font-bold text-white flex justify-between items-center">
                <span>إثبات بضاعة تالفة / هالك</span>
                <button onclick="closeModal('damagedModal')" class="text-gray-400 hover:text-white">&times;</button>
            </h3>
            <form id="damagedForm" onsubmit="handleSaveDamaged(event)" class="space-y-3 text-xs">
                <div>
                    <label class="text-gray-300 block mb-1">الصنف / المادة التالفة</label>
                    <input type="text" id="dmgItem" required placeholder="مثال: ألبان انتهت صلاحيتها، زجاج مكسور" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                </div>
                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="text-gray-300 block mb-1">الكمية التالفة</label>
                        <input type="number" id="dmgQty" required placeholder="1" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                    </div>
                    <div>
                        <label class="text-gray-300 block mb-1">تكلفة الوحدة</label>
                        <input type="number" step="0.01" id="dmgUnitCost" required placeholder="0.00" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                    </div>
                </div>
                <div>
                    <label class="text-gray-300 block mb-1">سبب التلف</label>
                    <input type="text" id="dmgReason" placeholder="سوء تخزين / انتهاء صلاحية" class="w-full px-3 py-2 rounded-xl bg-gray-900 border border-gray-700 text-white">
                </div>
                <div class="pt-3 flex gap-2">
                    <button type="submit" class="w-full py-2.5 text-xs font-bold rounded-xl bg-red-600 hover:bg-red-500 text-white transition">تسجيل الهالك</button>
                    <button type="button" onclick="closeModal('damagedModal')" class="w-full py-2.5 text-xs font-bold rounded-xl bg-gray-800 text-gray-300 hover:bg-gray-700 transition">إلغاء</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Confirmation Modal Dialog -->
    <div id="confirmModal" class="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-md hidden">
        <div class="glass-panel p-6 rounded-3xl w-full max-w-sm text-center space-y-4 border border-red-500/30">
            <div class="w-12 h-12 rounded-2xl bg-red-500/10 text-red-400 text-2xl mx-auto flex items-center justify-center">
                <i class="fa-solid fa-triangle-exclamation"></i>
            </div>
            <h3 class="text-base font-bold text-white" id="confirmTitle">تأكيد الإجراء</h3>
            <p class="text-xs text-gray-400" id="confirmMessage">هل أنت أكرر متأكد من هذا الإجراء؟</p>
            <div class="flex gap-2 pt-2">
                <button id="confirmYesBtn" class="w-full py-2 text-xs font-bold rounded-xl bg-red-600 hover:bg-red-500 text-white transition">تأكيد</button>
                <button onclick="closeModal('confirmModal')" class="w-full py-2 text-xs font-bold rounded-xl bg-gray-800 text-gray-300 hover:bg-gray-700 transition">إلغاء</button>
            </div>
        </div>
    </div>

    <!-- Notification Toast -->
    <div id="toast" class="fixed bottom-6 left-6 z-50 px-4 py-3 rounded-2xl glass-panel border border-emerald-500/30 text-white text-xs font-bold shadow-xl flex items-center gap-3 translate-y-20 opacity-0 transition-all duration-300">
        <i class="fa-solid fa-circle-check text-emerald-400 text-base" id="toastIcon"></i>
        <span id="toastMsg">تم تنفيذ العملية بنجاح!</span>
    </div>

    <footer class="no-print border-t border-gray-800/80 bg-darkbg py-4 text-center text-xs text-gray-400 mt-auto">
        <div class="max-w-7xl mx-auto px-4 flex flex-col sm:flex-row justify-between items-center gap-2">
            <div>
                منصة <strong class="text-white">محاسبي</strong> - النظام المحاسبي المتخصص المتقدم
            </div>
            <div class="text-emerald-400 font-medium">
                <i class="fa-solid fa-code"></i> تطوير وإعداد المحاسب: براء نادر توفيق ناصر
            </div>
        </div>
    </footer>

    <script>
        const STORAGE_KEY = 'muhasibi_app_state_v3';

        // Default App State Structure
        let state = {
            pin: null, // string e.g. "1234"
            isLocked: false,
            companyName: "شركة الأعمال المتطورة",
            currency: "USD",
            currencySymbol: "USD",
            taxRate: 16,
            activityType: "retail", // retail, real_estate, services, restaurant, manufacturing
            transactions: [],
            assets: [],
            checks: [],
            withdrawals: [],
            damaged: [],
            // Activity Specific Data Stores
            specializedData: {
                retail: { cogsBeginning: 5000, cogsPurchases: 12000, cogsEnding: 4500, discountsAllowed: 250, discountsEarned: 180 },
                realEstate: { leases: [], investmentCost: 150000, occupancyTotal: 10, occupancyRented: 8 },
                services: { billableHours: 120, hourlyRate: 45, unbilledProjects: 3 },
                restaurant: { foodWasteDailyCost: 40, shiftExpectedCash: 1200, shiftActualCash: 1195 },
                manufacturing: { bomItems: [], overheadCosts: 850 }
            }
        };

        let tempEnteredPin = "";

        function loadState() {
            try {
                const saved = localStorage.getItem(STORAGE_KEY);
                if (saved) {
                    state = Object.assign({}, state, JSON.parse(saved));
                }
            } catch (e) {
                console.error("Failed to load local storage", e);
            }
        }

        function saveState() {
            try {
                localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
            } catch (e) {
                console.error("Failed to save state", e);
            }
        }

        window.onload = function() {
            loadState();
            
            // Set print date
            document.getElementById('printDate').innerText = new Date().toLocaleDateString('ar-EG');
            
            // Check PIN lock
            if (state.pin && state.pin.length === 4) {
                state.isLocked = true;
                document.getElementById('pinLockModal').classList.remove('hidden');
            }

            syncSettingsUI();
            renderAllViews();
        };

        function appendPin(num) {
            if (tempEnteredPin.length < 4) {
                tempEnteredPin += num;
                updatePinDots();
            }
            if (tempEnteredPin.length === 4) {
                verifyPin();
            }
        }

        function clearPin() {
            tempEnteredPin = "";
            updatePinDots();
            document.getElementById('pinErrorMsg').classList.add('hidden');
        }

        function updatePinDots() {
            const dots = document.querySelectorAll('#pinDots .dot');
            dots.forEach((dot, idx) => {
                if (idx < tempEnteredPin.length) {
                    dot.classList.add('bg-emerald-500', 'border-emerald-500');
                } else {
                    dot.classList.remove('bg-emerald-500', 'border-emerald-500');
                }
            });
        }

        function verifyPin() {
            if (tempEnteredPin === state.pin) {
                state.isLocked = false;
                document.getElementById('pinLockModal').classList.add('hidden');
                tempEnteredPin = "";
                updatePinDots();
                showToast("تم فتح القفل بنجاح");
            } else {
                document.getElementById('pinErrorMsg').innerText = "رمز PIN غير صحيح!";
                document.getElementById('pinErrorMsg').classList.remove('hidden');
                tempEnteredPin = "";
                updatePinDots();
            }
        }

        function lockAppManual() {
            if (!state.pin) {
                showToast("يرجى تعيين رمز PIN أولاً من قسم الإعدادات", "warn");
                switchTab('settings');
                return;
            }
            state.isLocked = true;
            document.getElementById('pinLockModal').classList.remove('hidden');
        }

        function savePinSetting() {
            const val = document.getElementById('newPinInput').value;
            if (val.length === 4 && /^\d+$/.test(val)) {
                state.pin = val;
                saveState();
                syncSettingsUI();
                showToast("تم حفظ وتفعيل رمز PIN بنجاح");
                document.getElementById('newPinInput').value = "";
            } else {
                showToast("يرجى إدخال 4 أرقام فقط لرمز PIN", "warn");
            }
        }

        function removePinSetting() {
            state.pin = null;
            saveState();
            syncSettingsUI();
            showToast("تم إلغاء حماية رمز PIN");
        }

        function switchTab(tabId) {
            const sections = ['dashboard', 'transactions', 'specialized', 'assets', 'checks', 'equity', 'damaged', 'reports', 'settings'];
            sections.forEach(s => {
                const el = document.getElementById(`view-${s}`);
                const btn = document.getElementById(`tab-${s}`);
                if (el) el.classList.add('hidden');
                if (btn) {
                    btn.classList.remove('text-emerald-400', 'bg-emerald-500/10', 'border', 'border-emerald-500/20');
                    btn.classList.add('text-gray-400');
                }
            });

            const activeView = document.getElementById(`view-${tabId}`);
            const activeBtn = document.getElementById(`tab-${tabId}`);
            if (activeView) activeView.classList.remove('hidden');
            if (activeBtn) {
                activeBtn.classList.remove('text-gray-400');
                activeBtn.classList.add('text-emerald-400', 'bg-emerald-500/10', 'border', 'border-emerald-500/20');
            }
        }

        function syncSettingsUI() {
            document.getElementById('settingCompanyName').value = state.companyName || '';
            document.getElementById('settingCurrency').value = state.currency || 'USD';
            document.getElementById('settingTaxRate').value = state.taxRate || 16;
            document.getElementById('settingActivityType').value = state.activityType || 'retail';
            document.getElementById('printCompanyName').innerText = state.companyName || 'شركة الأعمال';

            // Currency symbol updates
            document.querySelectorAll('.currencySymbol').forEach(el => el.innerText = state.currency);
            document.querySelectorAll('.taxRateDisplay').forEach(el => el.innerText = state.taxRate);

            // PIN status
            const badge = document.getElementById('pinStatusBadge');
            if (state.pin) {
                badge.innerText = "مفعّل 🔒";
                badge.className = "px-2.5 py-0.5 text-xs rounded-full bg-emerald-500/10 text-emerald-400 border border-emerald-500/20";
            } else {
                badge.innerText = "غير مفعّل";
                badge.className = "px-2.5 py-0.5 text-xs rounded-full bg-red-500/10 text-red-400 border border-red-500/20";
            }

            // Activity Badge
            const names = {
                retail: "تجارة وتجزئة",
                real_estate: "عقارات ومخازن",
                services: "خدمات واستشارات",
                restaurant: "مطاعم وأغذية",
                manufacturing: "تصنيع وإنتاج"
            };
            const name = names[state.activityType] || "تجارة وتجزئة";
            document.getElementById('headerActivityBadge').innerText = name;
            document.getElementById('dashActivityTitle').innerText = name;
            document.getElementById('specializedTabLabel').innerText = `نشاط: ${name}`;
        }

        function updateGeneralSettings() {
            state.companyName = document.getElementById('settingCompanyName').value;
            state.currency = document.getElementById('settingCurrency').value;
            state.taxRate = parseFloat(document.getElementById('settingTaxRate').value) || 0;
            saveState();
            syncSettingsUI();
            renderAllViews();
            showToast("تم تحديث الإعدادات العادية بنجاح");
        }

        function changeActivityType(newType) {
            state.activityType = newType;
            saveState();
            syncSettingsUI();
            renderSpecializedHub();
            showToast("تم تغيير نوع النشاط المتخصص");
        }

        function renderAllViews() {
            renderDashboard();
            renderTransactions();
            renderSpecializedHub();
            renderAssets();
            renderChecks();
            renderWithdrawals();
            renderDamaged();
            renderReports();
        }

        function renderDashboard() {
            let totalIncome = 0;
            let totalExpense = 0;
            let totalTax = 0;

            state.transactions.forEach(t => {
                if (t.type === 'income') {
                    totalIncome += t.amount;
                    if (t.taxable) totalTax += (t.amount * (state.taxRate / 100));
                } else if (t.type === 'expense') {
                    totalExpense += t.amount;
                }
            });

            let totalDamagedLoss = state.damaged.reduce((sum, d) => sum + (d.qty * d.unitCost), 0);
            let totalExpenseWithDamaged = totalExpense + totalDamagedLoss;
            let netProfit = totalIncome - totalExpenseWithDamaged;

            let totalAssetsNetVal = state.assets.reduce((sum, a) => {
                let dep = ((a.cost - a.salvage) / a.lifespan);
                return sum + Math.max(0, a.cost - dep);
            }, 0);

            let totalWithdrawals = state.withdrawals.reduce((sum, w) => sum + w.amount, 0);
            let pendingChecks = state.checks.filter(c => c.status === 'pending' && c.type === 'received').reduce((sum, c) => sum + c.amount, 0);

            document.getElementById('dashIncome').innerText = totalIncome.toFixed(2);
            document.getElementById('dashExpenses').innerText = totalExpenseWithDamaged.toFixed(2);
            document.getElementById('dashNetProfit').innerText = netProfit.toFixed(2);
            document.getElementById('dashAssetsVal').innerText = totalAssetsNetVal.toFixed(2);
            document.getElementById('dashTaxVal').innerText = totalTax.toFixed(2);
            document.getElementById('dashWithdrawalsVal').innerText = totalWithdrawals.toFixed(2);
            document.getElementById('dashPendingChecksVal').innerText = pendingChecks.toFixed(2);
            document.getElementById('dashTaxRate').innerText = state.taxRate;

            let margin = totalIncome > 0 ? ((netProfit / totalIncome) * 100).toFixed(1) : 0;
            document.getElementById('profitMarginText').innerText = `هامش الربح التشغيلي: ${margin}%`;
        }

        function renderTransactions() {
            const tbody = document.getElementById('txTableBody');
            tbody.innerHTML = '';

            const search = document.getElementById('txSearch').value.toLowerCase();
            const filterType = document.getElementById('txFilterType').value;

            const filtered = state.transactions.filter(t => {
                const matchesSearch = t.desc.toLowerCase().includes(search) || (t.category && t.category.toLowerCase().includes(search));
                const matchesType = filterType === 'all' || t.type === filterType;
                return matchesSearch && matchesType;
            });

            if (filtered.length === 0) {
                tbody.innerHTML = `<tr><td colspan="8" class="p-6 text-center text-gray-500">لا يوجد قيود سجلت بعد</td></tr>`;
                return;
            }

            filtered.forEach(t => {
                const taxVal = t.taxable ? (t.amount * (state.taxRate / 100)) : 0;
                const grandTotal = t.amount + taxVal;
                const isInc = t.type === 'income';

                const tr = document.createElement('tr');
                tr.className = "hover:bg-gray-800/30 transition";
                tr.innerHTML = `
                    <td class="p-3 text-gray-400">${t.date}</td>
                    <td class="p-3">
                        <span class="px-2 py-0.5 rounded-md text-[10px] font-bold ${isInc ? 'bg-emerald-500/10 text-emerald-400 border border-emerald-500/20' : 'bg-red-500/10 text-red-400 border border-red-500/20'}">
                            ${isInc ? 'إيراد (+)' : 'مصروف (-)'}
                        </span>
                    </td>
                    <td class="p-3 font-semibold text-white">${t.desc}</td>
                    <td class="p-3 text-gray-400">${t.category || '-'}</td>
                    <td class="p-3 font-bold ${isInc ? 'text-emerald-400' : 'text-red-400'}">${t.amount.toFixed(2)}</td>
                    <td class="p-3 text-gray-400">${taxVal.toFixed(2)}</td>
                    <td class="p-3 font-bold text-gray-200">${grandTotal.toFixed(2)}</td>
                    <td class="p-3 text-center">
                        <button onclick="deleteTransaction('${t.id}')" class="text-gray-500 hover:text-red-400 p-1"><i class="fa-solid fa-trash"></i></button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function openTransactionModal() {
            document.getElementById('txModal').classList.remove('hidden');
        }

        function handleSaveTx(e) {
            e.preventDefault();
            const newTx = {
                id: 'tx_' + Date.now(),
                type: document.getElementById('txType').value,
                desc: document.getElementById('txDesc').value,
                amount: parseFloat(document.getElementById('txAmount').value),
                category: document.getElementById('txCategory').value,
                taxable: document.getElementById('txTaxable').checked,
                date: new Date().toLocaleDateString('ar-EG')
            };
            state.transactions.unshift(newTx);
            saveState();
            closeModal('txModal');
            document.getElementById('txForm').reset();
            renderAllViews();
            showToast("تم تسجيل القيد بنجاح");
        }

        function deleteTransaction(id) {
            showConfirm("حذف القيد", "هل أنت تأكيد تريد حذف هذا القيد؟", () => {
                state.transactions = state.transactions.filter(t => t.id !== id);
                saveState();
                renderAllViews();
                showToast("تم حذف القيد");
            });
        }

        function renderSpecializedHub() {
            const container = document.getElementById('specializedContainer');
            const type = state.activityType;

            if (type === 'retail') {
                const r = state.specializedData.retail;
                const cogs = (r.cogsBeginning + r.cogsPurchases) - r.cogsEnding;
                container.innerHTML = `
                    <div class="glass-panel p-6 rounded-3xl space-y-6">
                        <div class="border-b border-gray-800 pb-3">
                            <h2 class="text-xl font-bold text-white"><i class="fa-solid fa-boxes-packing text-emerald-400"></i> حاسبة تكلفة المبيعات وجرد المخزون (COGS)</h2>
                            <p class="text-xs text-gray-400">احتساب تكلفة البضاعة المباعة وتتبع الخصومات المسموح بها والمكتسبة</p>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                            <div class="glass-card p-4 rounded-2xl">
                                <label class="text-xs text-gray-400 block mb-1">بضاعة أول المدة</label>
                                <input type="number" value="${r.cogsBeginning}" onchange="updateRetailData('cogsBeginning', this.value)" class="w-full px-3 py-1.5 text-xs rounded-xl bg-gray-900 border border-gray-700 text-white">
                            </div>
                            <div class="glass-card p-4 rounded-2xl">
                                <label class="text-xs text-gray-400 block mb-1">إجمالي المشتريات خلال الفترة</label>
                                <input type="number" value="${r.cogsPurchases}" onchange="updateRetailData('cogsPurchases', this.value)" class="w-full px-3 py-1.5 text-xs rounded-xl bg-gray-900 border border-gray-700 text-white">
                            </div>
                            <div class="glass-card p-4 rounded-2xl">
                                <label class="text-xs text-gray-400 block mb-1">بضاعة آخر المدة (الجرد)</label>
                                <input type="number" value="${r.cogsEnding}" onchange="updateRetailData('cogsEnding', this.value)" class="w-full px-3 py-1.5 text-xs rounded-xl bg-gray-900 border border-gray-700 text-white">
                            </div>
                        </div>
                        <div class="p-4 rounded-2xl bg-emerald-500/10 border border-emerald-500/30 flex justify-between items-center">
                            <span class="text-sm font-bold text-white">تكلفة البضاعة المباعة المقدرة (COGS):</span>
                            <span class="text-xl font-extrabold text-emerald-400">${cogs.toFixed(2)} ${state.currency}</span>
                        </div>
                    </div>
                `;
            } else if (type === 'real_estate') {
                const re = state.specializedData.realEstate;
                const occRate = re.occupancyTotal > 0 ? ((re.occupancyRented / re.occupancyTotal) * 100).toFixed(1) : 0;
                container.innerHTML = `
                    <div class="glass-panel p-6 rounded-3xl space-y-6">
                        <div class="border-b border-gray-800 pb-3">
                            <h2 class="text-xl font-bold text-white"><i class="fa-solid fa-building text-blue-400"></i> إدارة العقارات ونسبة الإشغال وعائد الاستثمار (ROI)</h2>
                            <p class="text-xs text-gray-400">متابعة إيجارات الوحدات وحساب نسبة الإشغال الفعلية</p>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                            <div class="glass-card p-4 rounded-2xl">
                                <label class="text-xs text-gray-400 block mb-1">إجمالي عدد الوحدات / المخازن</label>
                                <input type="number" value="${re.occupancyTotal}" onchange="updateRealEstateData('occupancyTotal', this.value)" class="w-full px-3 py-1.5 text-xs rounded-xl bg-gray-900 border border-gray-700 text-white">
                            </div>
                            <div class="glass-card p-4 rounded-2xl">
                                <label class="text-xs text-gray-400 block mb-1">عدد الوحدات المؤجرة فعلياً</label>
                                <input type="number" value="${re.occupancyRented}" onchange="updateRealEstateData('occupancyRented', this.value)" class="w-full px-3 py-1.5 text-xs rounded-xl bg-gray-900 border border-gray-700 text-white">
                            </div>
                            <div class="glass-card p-4 rounded-2xl">
                                <label class="text-xs text-gray-400 block mb-1">إجمالي تكلفة الاستثمار العقاري</label>
                                <input type="number" value="${re.investmentCost}" onchange="updateRealEstateData('investmentCost', this.value)" class="w-full px-3 py-1.5 text-xs rounded-xl bg-gray-900 border border-gray-700 text-white">
                            </div>
                        </div>
                        <div class="p-4 rounded-2xl bg-blue-500/10 border border-blue-500/30 flex justify-between items-center">
                            <span class="text-sm font-bold text-white">نسبة إشغال العقارات الحالية:</span>
                            <span class="text-xl font-extrabold text-blue-400">${occRate}%</span>
                        </div>
                    </div>
                `;
            } else if (type === 'services') {
                const s = state.specializedData.services;
                const totalBillable = s.billableHours * s.hourlyRate;
                container.innerHTML = `
                    <div class="glass-panel p-6 rounded-3xl space-y-6">
                        <div class="border-b border-gray-800 pb-3">
                            <h2 class="text-xl font-bold text-white"><i class="fa-solid fa-user-gear text-purple-400"></i> تتبع الساعات القابلة للفوترة والاستشارات</h2>
                            <p class="text-xs text-gray-400">حساب فواتير الخدمات بالساعة والمشاريع المنجزة</p>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div class="glass-card p-4 rounded-2xl">
                                <label class="text-xs text-gray-400 block mb-1">الساعات القابلة للفوترة المسجلة</label>
                                <input type="number" value="${s.billableHours}" onchange="updateServicesData('billableHours', this.value)" class="w-full px-3 py-1.5 text-xs rounded-xl bg-gray-900 border border-gray-700 text-white">
                            </div>
                            <div class="glass-card p-4 rounded-2xl">
                                <label class="text-xs text-gray-400 block mb-1">سعر الساعة الاستشارية المعياري</label>
                                <input type="number" value="${s.hourlyRate}" onchange="updateServicesData('hourlyRate', this.value)" class="w-full px-3 py-1.5 text-xs rounded-xl bg-gray-900 border border-gray-700 text-white">
                            </div>
                        </div>
                        <div class="p-4 rounded-2xl bg-purple-500/10 border border-purple-500/30 flex justify-between items-center">
                            <span class="text-sm font-bold text-white">إجمالي الإيراد المستحق للساعات:</span>
                            <span class="text-xl font-extrabold text-purple-400">${totalBillable.toFixed(2)} ${state.currency}</span>
                        </div>
                    </div>
                `;
            } else if (type === 'restaurant') {
                const r = state.specializedData.restaurant;
                const diff = r.shiftActualCash - r.shiftExpectedCash;
                container.innerHTML = `
                    <div class="glass-panel p-6 rounded-3xl space-y-6">
                        <div class="border-b border-gray-800 pb-3">
                            <h2 class="text-xl font-bold text-white"><i class="fa-solid fa-utensils text-amber-400"></i> جرد الكاشير اليومي ونهاية الوردية والهدر</h2>
                            <p class="text-xs text-gray-400">مطابقة الكاشير اليومية وتتبع الهدر في الوجبات والمواد الأوليّة</p>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                            <div class="glass-card p-4 rounded-2xl">
                                <label class="text-xs text-gray-400 block mb-1">النقد المتوقع بالنظام (Expected)</label>
                                <input type="number" value="${r.shiftExpectedCash}" onchange="updateRestData('shiftExpectedCash', this.value)" class="w-full px-3 py-1.5 text-xs rounded-xl bg-gray-900 border border-gray-700 text-white">
                            </div>
                            <div class="glass-card p-4 rounded-2xl">
                                <label class="text-xs text-gray-400 block mb-1">النقد الفعلي بالدرج (Actual)</label>
                                <input type="number" value="${r.shiftActualCash}" onchange="updateRestData('shiftActualCash', this.value)" class="w-full px-3 py-1.5 text-xs rounded-xl bg-gray-900 border border-gray-700 text-white">
                            </div>
                            <div class="glass-card p-4 rounded-2xl">
                                <label class="text-xs text-gray-400 block mb-1">تكلفة هدر الأغذية اليومي</label>
                                <input type="number" value="${r.foodWasteDailyCost}" onchange="updateRestData('foodWasteDailyCost', this.value)" class="w-full px-3 py-1.5 text-xs rounded-xl bg-gray-900 border border-gray-700 text-white">
                            </div>
                        </div>
                        <div class="p-4 rounded-2xl ${diff >= 0 ? 'bg-emerald-500/10 border-emerald-500/30' : 'bg-red-500/10 border-red-500/30'} border flex justify-between items-center">
                            <span class="text-sm font-bold text-white">فرق الدرج / الكاشير (عجز / زيادة):</span>
                            <span class="text-xl font-extrabold ${diff >= 0 ? 'text-emerald-400' : 'text-red-400'}">${diff >= 0 ? '+' : ''}${diff.toFixed(2)} ${state.currency}</span>
                        </div>
                    </div>
                `;
            } else if (type === 'manufacturing') {
                const m = state.specializedData.manufacturing;
                container.innerHTML = `
                    <div class="glass-panel p-6 rounded-3xl space-y-6">
                        <div class="border-b border-gray-800 pb-3">
                            <h2 class="text-xl font-bold text-white"><i class="fa-solid fa-industry text-indigo-400"></i> قائمة المواد (BOM) والمصاريف الصناعية غير المباشرة</h2>
                            <p class="text-xs text-gray-400">توزيع المصاريف الصناعية غير المباشرة وتحديد تكلفة تصنيع الوحدة</p>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div class="glass-card p-4 rounded-2xl">
                                <label class="text-xs text-gray-400 block mb-1">المصاريف الصناعية غير المباشرة الشهرية</label>
                                <input type="number" value="${m.overheadCosts}" onchange="updateMfgData('overheadCosts', this.value)" class="w-full px-3 py-1.5 text-xs rounded-xl bg-gray-900 border border-gray-700 text-white">
                            </div>
                            <div class="glass-card p-4 rounded-2xl flex items-center justify-between">
                                <span class="text-xs text-gray-400">حالة خطوط الإنتاج:</span>
                                <span class="px-2.5 py-1 text-xs rounded-full bg-emerald-500/10 text-emerald-400 font-bold border border-emerald-500/20">جاهز للتصنيع</span>
                            </div>
                        </div>
                    </div>
                `;
            }
        }

        // Helper updates for specialized inputs
        function updateRetailData(key, val) {
            state.specializedData.retail[key] = parseFloat(val) || 0;
            saveState();
            renderSpecializedHub();
        }
        function updateRealEstateData(key, val) {
            state.specializedData.realEstate[key] = parseFloat(val) || 0;
            saveState();
            renderSpecializedHub();
        }
        function updateServicesData(key, val) {
            state.specializedData.services[key] = parseFloat(val) || 0;
            saveState();
            renderSpecializedHub();
        }
        function updateRestData(key, val) {
            state.specializedData.restaurant[key] = parseFloat(val) || 0;
            saveState();
            renderSpecializedHub();
        }
        function updateMfgData(key, val) {
            state.specializedData.manufacturing[key] = parseFloat(val) || 0;
            saveState();
            renderSpecializedHub();
        }

        function renderAssets() {
            const tbody = document.getElementById('assetsTableBody');
            tbody.innerHTML = '';

            let totalCost = 0;
            let totalAccDep = 0;

            if (state.assets.length === 0) {
                tbody.innerHTML = `<tr><td colspan="8" class="p-6 text-center text-gray-500">لا يوجد أصول ثابتة مسجلة</td></tr>`;
            }

            state.assets.forEach(a => {
                totalCost += a.cost;
                let annualDep = (a.cost - a.salvage) / a.lifespan;
                totalAccDep += annualDep; // annual estimated
                let netBookVal = Math.max(0, a.cost - annualDep);

                const tr = document.createElement('tr');
                tr.className = "hover:bg-gray-800/30 transition";
                tr.innerHTML = `
                    <td class="p-3 font-semibold text-white">${a.name}</td>
                    <td class="p-3 text-gray-400">${a.purchaseDate}</td>
                    <td class="p-3 font-bold text-gray-200">${a.cost.toFixed(2)}</td>
                    <td class="p-3 text-gray-400">${a.salvage.toFixed(2)}</td>
                    <td class="p-3 text-gray-400">${a.lifespan} سنة</td>
                    <td class="p-3 text-amber-400 font-bold">${annualDep.toFixed(2)}</td>
                    <td class="p-3 text-emerald-400 font-bold">${netBookVal.toFixed(2)}</td>
                    <td class="p-3 text-center">
                        <button onclick="deleteAsset('${a.id}')" class="text-gray-500 hover:text-red-400 p-1"><i class="fa-solid fa-trash"></i></button>
                    </td>
                `;
                tbody.appendChild(tr);
            });

            document.getElementById('assetsTotalCost').innerText = totalCost.toFixed(2);
            document.getElementById('assetsAccDepreciation').innerText = totalAccDep.toFixed(2);
            document.getElementById('assetsNetBookValue').innerText = Math.max(0, totalCost - totalAccDep).toFixed(2);
        }

        function openAssetModal() {
            document.getElementById('assetModal').classList.remove('hidden');
        }

        function handleSaveAsset(e) {
            e.preventDefault();
            const newAsset = {
                id: 'ast_' + Date.now(),
                name: document.getElementById('assetName').value,
                cost: parseFloat(document.getElementById('assetCost').value),
                salvage: parseFloat(document.getElementById('assetSalvage').value) || 0,
                lifespan: parseInt(document.getElementById('assetLifespan').value) || 1,
                purchaseDate: document.getElementById('assetDate').value || new Date().toLocaleDateString('ar-EG')
            };
            state.assets.push(newAsset);
            saveState();
            closeModal('assetModal');
            document.getElementById('assetForm').reset();
            renderAllViews();
            showToast("تم تسجيل الأصل الثابت بنجاح");
        }

        function deleteAsset(id) {
            showConfirm("حذف الأصل", "هل أنت تأكيد تريد حذف هذا الأصل؟", () => {
                state.assets = state.assets.filter(a => a.id !== id);
                saveState();
                renderAllViews();
                showToast("تم حذف الأصل");
            });
        }

        function renderChecks() {
            const tbody = document.getElementById('checksTableBody');
            tbody.innerHTML = '';

            if (state.checks.length === 0) {
                tbody.innerHTML = `<tr><td colspan="7" class="p-6 text-center text-gray-500">لا يوجد شيكات مسجلة</td></tr>`;
                return;
            }

            state.checks.forEach(c => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-gray-800/30 transition";

                let statusBadge = "";
                if (c.status === 'pending') statusBadge = `<span class="px-2 py-0.5 rounded-md text-[10px] bg-amber-500/10 text-amber-400 border border-amber-500/20">برسم التحصيل</span>`;
                else if (c.status === 'cleared') statusBadge = `<span class="px-2 py-0.5 rounded-md text-[10px] bg-emerald-500/10 text-emerald-400 border border-emerald-500/20">متحصل / محصل</span>`;
                else statusBadge = `<span class="px-2 py-0.5 rounded-md text-[10px] bg-red-500/10 text-red-400 border border-red-500/20">راجع / مرفوض</span>`;

                tr.innerHTML = `
                    <td class="p-3 font-bold text-white">${c.number}</td>
                    <td class="p-3 text-gray-300">${c.type === 'received' ? 'مقبوض (+)' : 'محرر (-)'}</td>
                    <td class="p-3 text-gray-300">${c.payee}</td>
                    <td class="p-3 font-bold text-emerald-400">${c.amount.toFixed(2)}</td>
                    <td class="p-3 text-gray-400">${c.dueDate}</td>
                    <td class="p-3">${statusBadge}</td>
                    <td class="p-3 text-center flex items-center justify-center gap-2">
                        <button onclick="toggleCheckStatus('${c.id}', 'cleared')" class="text-xs text-emerald-400 hover:underline">تحصيل</button>
                        <button onclick="toggleCheckStatus('${c.id}', 'returned')" class="text-xs text-red-400 hover:underline">إرجاع</button>
                        <button onclick="deleteCheck('${c.id}')" class="text-gray-500 hover:text-red-400 p-1"><i class="fa-solid fa-trash"></i></button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function openCheckModal() {
            document.getElementById('checkModal').classList.remove('hidden');
        }

        function handleSaveCheck(e) {
            e.preventDefault();
            const newCheck = {
                id: 'chk_' + Date.now(),
                number: document.getElementById('chkNumber').value,
                type: document.getElementById('chkType').value,
                payee: document.getElementById('chkPayee').value,
                amount: parseFloat(document.getElementById('chkAmount').value),
                dueDate: document.getElementById('chkDueDate').value,
                status: 'pending'
            };
            state.checks.push(newCheck);
            saveState();
            closeModal('checkModal');
            document.getElementById('checkForm').reset();
            renderAllViews();
            showToast("تم حفظ الشيك بنجاح");
        }

        function toggleCheckStatus(id, newStatus) {
            const chk = state.checks.find(c => c.id === id);
            if (chk) {
                chk.status = newStatus;
                saveState();
                renderAllViews();
                showToast("تم تحديث حالة الشيك");
            }
        }

        function deleteCheck(id) {
            showConfirm("حذف الشيك", "هل تأكيد تريد حذف هذا الشيك؟", () => {
                state.checks = state.checks.filter(c => c.id !== id);
                saveState();
                renderAllViews();
                showToast("تم حذف الشيك");
            });
        }

        function renderWithdrawals() {
            const tbody = document.getElementById('withdrawalsTableBody');
            tbody.innerHTML = '';

            if (state.withdrawals.length === 0) {
                tbody.innerHTML = `<tr><td colspan="5" class="p-6 text-center text-gray-500">لا يوجد مسحوبات شخصية مسجلة</td></tr>`;
                return;
            }

            state.withdrawals.forEach(w => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-gray-800/30 transition";
                tr.innerHTML = `
                    <td class="p-3 text-gray-400">${w.date}</td>
                    <td class="p-3 font-bold text-white">${w.partner}</td>
                    <td class="p-3 font-bold text-amber-400">${w.amount.toFixed(2)}</td>
                    <td class="p-3 text-gray-400">${w.notes || '-'}</td>
                    <td class="p-3 text-center">
                        <button onclick="deleteWithdrawal('${w.id}')" class="text-gray-500 hover:text-red-400 p-1"><i class="fa-solid fa-trash"></i></button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function openWithdrawalModal() {
            document.getElementById('withdrawalModal').classList.remove('hidden');
        }

        function handleSaveWithdrawal(e) {
            e.preventDefault();
            const newW = {
                id: 'wd_' + Date.now(),
                partner: document.getElementById('wdPartner').value,
                amount: parseFloat(document.getElementById('wdAmount').value),
                notes: document.getElementById('wdNotes').value,
                date: new Date().toLocaleDateString('ar-EG')
            };
            state.withdrawals.push(newW);
            saveState();
            closeModal('withdrawalModal');
            document.getElementById('withdrawalForm').reset();
            renderAllViews();
            showToast("تم تسجيل مسحوبات الشريك");
        }

        function deleteWithdrawal(id) {
            showConfirm("حذف قيد المسحوبات", "هل تأكيد تريد مسح قيد المسحوبات؟", () => {
                state.withdrawals = state.withdrawals.filter(w => w.id !== id);
                saveState();
                renderAllViews();
                showToast("تم حذف القيد");
            });
        }

        function renderDamaged() {
            const tbody = document.getElementById('damagedTableBody');
            tbody.innerHTML = '';

            if (state.damaged.length === 0) {
                tbody.innerHTML = `<tr><td colspan="7" class="p-6 text-center text-gray-500">لا يوجد بضاعة تالفة مسجلة</td></tr>`;
                return;
            }

            state.damaged.forEach(d => {
                const totalLoss = d.qty * d.unitCost;
                const tr = document.createElement('tr');
                tr.className = "hover:bg-gray-800/30 transition";
                tr.innerHTML = `
                    <td class="p-3 text-gray-400">${d.date}</td>
                    <td class="p-3 font-bold text-white">${d.item}</td>
                    <td class="p-3 text-gray-300">${d.qty}</td>
                    <td class="p-3 text-gray-300">${d.unitCost.toFixed(2)}</td>
                    <td class="p-3 font-bold text-red-400">${totalLoss.toFixed(2)}</td>
                    <td class="p-3 text-gray-400">${d.reason || '-'}</td>
                    <td class="p-3 text-center">
                        <button onclick="deleteDamaged('${d.id}')" class="text-gray-500 hover:text-red-400 p-1"><i class="fa-solid fa-trash"></i></button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function openDamagedModal() {
            document.getElementById('damagedModal').classList.remove('hidden');
        }

        function handleSaveDamaged(e) {
            e.preventDefault();
            const newD = {
                id: 'dmg_' + Date.now(),
                item: document.getElementById('dmgItem').value,
                qty: parseFloat(document.getElementById('dmgQty').value),
                unitCost: parseFloat(document.getElementById('dmgUnitCost').value),
                reason: document.getElementById('dmgReason').value,
                date: new Date().toLocaleDateString('ar-EG')
            };
            state.damaged.push(newD);
            saveState();
            closeModal('damagedModal');
            document.getElementById('damagedForm').reset();
            renderAllViews();
            showToast("تم إثبات هالك البضاعة");
        }

        function deleteDamaged(id) {
            showConfirm("حذف هالك البضاعة", "هل تأكيد تريد حذف هذا السجل؟", () => {
                state.damaged = state.damaged.filter(d => d.id !== id);
                saveState();
                renderAllViews();
                showToast("تم الحذف");
            });
        }

        function renderReports() {
            let totalInc = state.transactions.filter(t => t.type === 'income').reduce((s, t) => s + t.amount, 0);
            let totalExp = state.transactions.filter(t => t.type === 'expense').reduce((s, t) => s + t.amount, 0);
            let totalDamagedLoss = state.damaged.reduce((s, d) => s + (d.qty * d.unitCost), 0);
            let totalDepreciation = state.assets.reduce((s, a) => s + ((a.cost - a.salvage) / a.lifespan), 0);

            let netProfit = totalInc - (totalExp + totalDamagedLoss + totalDepreciation);

            let totalAssetCost = state.assets.reduce((s, a) => s + a.cost, 0);
            let totalAssetNet = Math.max(0, totalAssetCost - totalDepreciation);
            let pendingChecks = state.checks.filter(c => c.status === 'pending' && c.type === 'received').reduce((s, c) => s + c.amount, 0);
            let ownerWithdrawals = state.withdrawals.reduce((s, w) => s + w.amount, 0);

            document.getElementById('repIncome').innerText = `${totalInc.toFixed(2)} ${state.currency}`;
            document.getElementById('repExpenses').innerText = `${totalExp.toFixed(2)} ${state.currency}`;
            document.getElementById('repDamaged').innerText = `${totalDamagedLoss.toFixed(2)} ${state.currency}`;
            document.getElementById('repDepreciations').innerText = `${totalDepreciation.toFixed(2)} ${state.currency}`;
            document.getElementById('repNetProfit').innerText = `${netProfit.toFixed(2)} ${state.currency}`;

            document.getElementById('repAssetsBookVal').innerText = `${totalAssetNet.toFixed(2)} ${state.currency}`;
            document.getElementById('repPendingChecks').innerText = `${pendingChecks.toFixed(2)} ${state.currency}`;
            document.getElementById('repOwnerWithdrawals').innerText = `${ownerWithdrawals.toFixed(2)} ${state.currency}`;
            document.getElementById('repTotalEquity').innerText = `${(totalAssetNet + pendingChecks - ownerWithdrawals).toFixed(2)} ${state.currency}`;
        }

        function loadDemoData() {
            showConfirm("تحميل البيانات التجريبية 🚀", "سيتم ملء جميع أقسام أداة محاسبي ببيانات مالية نموذجية متكاملة. هل تود المتابعة؟", () => {
                state.companyName = "شركة القدس التجارية العالمية";
                state.currency = "USD";
                state.taxRate = 16;
                state.activityType = "retail";

                state.transactions = [
                    { id: 'tx_1', type: 'income', desc: 'مبيعات بضاعة جملة - شركة الأمل', amount: 4500, category: 'مبيعات', taxable: true, date: '2026-09-01' },
                    { id: 'tx_2', type: 'income', desc: 'خدمات استشارية وصيانة دورية', amount: 1200, category: 'خدمات', taxable: true, date: '2026-09-05' },
                    { id: 'tx_3', type: 'expense', desc: 'إيجار المقر الرئيسي والشواغر', amount: 800, category: 'إيجار', taxable: false, date: '2026-09-02' },
                    { id: 'tx_4', type: 'expense', desc: 'فاتورة الكهرباء والانترنت للمكتب', amount: 180, category: 'مرافق', taxable: true, date: '2026-09-10' },
                    { id: 'tx_5', type: 'expense', desc: 'شراء مواد وقرطاسية مكتبية', amount: 120, category: 'مصاريف إدارية', taxable: true, date: '2026-09-12' }
                ];

                state.assets = [
                    { id: 'ast_1', name: 'سيارة توزيع فورد نtrans', cost: 18000, salvage: 3000, lifespan: 5, purchaseDate: '2024-01-15' },
                    { id: 'ast_2', name: 'أجهزة حاسوب وسيرفرات مركزية', cost: 4500, salvage: 500, lifespan: 3, purchaseDate: '2025-06-10' }
                ];

                state.checks = [
                    { id: 'chk_1', number: '900451', type: 'received', payee: 'بنك العربي - شركة النور', amount: 2500, dueDate: '2026-10-15', status: 'pending' },
                    { id: 'chk_2', number: '300102', type: 'issued', payee: 'بنك فلسطين - المورد الرئيسي', amount: 1400, dueDate: '2026-09-20', status: 'cleared' }
                ];

                state.withdrawals = [
                    { id: 'wd_1', partner: 'براء نادر توفيق ناصر', amount: 500, notes: 'سحب شخصي نقدية', date: '2026-09-15' }
                ];

                state.damaged = [
                    { id: 'dmg_1', item: 'كرتونة زجاج عصير تالفة', qty: 4, unitCost: 15, reason: 'كسر أثناء التفريغ', date: '2026-09-08' }
                ];

                state.specializedData.retail = {
                    cogsBeginning: 6000,
                    cogsPurchases: 14000,
                    cogsEnding: 5200,
                    discountsAllowed: 300,
                    discountsEarned: 200
                };

                saveState();
                syncSettingsUI();
                renderAllViews();
                showToast("تم تحميل البيانات التجريبية المتكاملة 🚀");
            });
        }

        function exportDataJSON() {
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(state, null, 2));
            const downloadAnchor = document.createElement('a');
            downloadAnchor.setAttribute("href", dataStr);
            downloadAnchor.setAttribute("download", `muhasibi_backup_${new Date().toISOString().slice(0,10)}.json`);
            document.body.appendChild(downloadAnchor);
            downloadAnchor.click();
            downloadAnchor.remove();
            showToast("تم تحميل ملف النسخة الاحتياطية JSON");
        }

        function importDataJSON(e) {
            const fileReader = new FileReader();
            fileReader.onload = function (event) {
                try {
                    const importedState = JSON.parse(event.target.result);
                    if (importedState && typeof importedState === 'object') {
                        state = Object.assign({}, state, importedState);
                        saveState();
                        syncSettingsUI();
                        renderAllViews();
                        showToast("تم استعادة كافة البيانات بنجاح!");
                    }
                } catch (err) {
                    showToast("ملف JSON غير صالحة!", "error");
                }
            };
            if (e.target.files[0]) {
                fileReader.readAsText(e.target.files[0]);
            }
        }

        function resetAllDataModal() {
            showConfirm("تصفير البيانات بالكامل", "هل أنت تأكيد تماماً من حذف كافة البيانات والمستندات؟ لا يمكن التراجع عن هذا الإجراء.", () => {
                localStorage.removeItem(STORAGE_KEY);
                location.reload();
            });
        }

        function closeModal(modalId) {
            document.getElementById(modalId).classList.add('hidden');
        }

        let onConfirmCallback = null;
        function showConfirm(title, msg, onConfirm) {
            document.getElementById('confirmTitle').innerText = title;
            document.getElementById('confirmMessage').innerText = msg;
            onConfirmCallback = onConfirm;
            document.getElementById('confirmModal').classList.remove('hidden');

            document.getElementById('confirmYesBtn').onclick = function() {
                if (onConfirmCallback) onConfirmCallback();
                closeModal('confirmModal');
            };
        }

        function showToast(msg, type = "success") {
            const toast = document.getElementById('toast');
            const toastMsg = document.getElementById('toastMsg');
            const toastIcon = document.getElementById('toastIcon');

            toastMsg.innerText = msg;
            if (type === 'warn' || type === 'error') {
                toastIcon.className = "fa-solid fa-circle-exclamation text-amber-400 text-base";
            } else {
                toastIcon.className = "fa-solid fa-circle-check text-emerald-400 text-base";
            }

            toast.classList.remove('translate-y-20', 'opacity-0');
            setTimeout(() => {
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }
    </script>
</body>
</html>
