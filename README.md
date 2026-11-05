background-color: #f8fafc;
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Metro Track DPR Dashboard - Multi-Package System</title>
    <!-- Tailwind CSS for modern aesthetics -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome for icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Font: Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
    </style>
</head>
<body class="text-slate-800 antialiased min-h-screen flex flex-col">

    <!-- Top Navigation Header -->
    <header class="bg-slate-900 text-white shadow-lg sticky top-0 z-30">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 flex flex-col md:flex-row items-center justify-between gap-4">
            <div class="flex items-center gap-3">
                <div class="p-2.5 bg-blue-600 rounded-xl shadow-md flex items-center justify-center text-white">
                    <i class="fa-solid fa-train-subway text-2xl"></i>
                </div>
                <div>
                    <h1 class="text-xl font-bold tracking-tight">Metro Track Project DPR System</h1>
                    <p class="text-xs text-slate-400">Daily Progress Report Management & Multi-Package Analytics</p>
                </div>
            </div>

            <!-- Controls: Package Selector & Renamer -->
            <div class="flex flex-wrap items-center gap-2 sm:gap-3 w-full md:w-auto justify-end">
                <div class="flex items-center bg-slate-800 rounded-lg p-1 border border-slate-700">
                    <i class="fa-solid fa-cubes text-blue-400 ml-2.5 mr-2"></i>
                    <select id="packageSelect" onchange="switchPackage(this.value)" class="bg-transparent text-white font-medium text-sm focus:outline-none pr-3 py-1.5 cursor-pointer">
                        <!-- Options generated dynamically -->
                    </select>
                </div>

                <button onclick="openRenameModal()" class="px-3 py-2 bg-slate-800 hover:bg-slate-700 text-slate-200 text-sm font-medium rounded-lg border border-slate-700 transition flex items-center gap-2" title="Rename Active Package">
                    <i class="fa-solid fa-pen-to-square text-amber-400"></i>
                    <span class="hidden sm:inline">Rename Package</span>
                </button>

                <div class="h-6 w-px bg-slate-700 hidden sm:block"></div>

                <button onclick="exportToCSV()" class="px-3 py-2 bg-emerald-700 hover:bg-emerald-600 text-white text-sm font-medium rounded-lg shadow-sm transition flex items-center gap-1.5" title="Export to CSV">
                    <i class="fa-solid fa-file-csv"></i>
                    <span class="hidden sm:inline">Export</span>
                </button>

                <button onclick="resetAllData()" class="px-3 py-2 bg-rose-900/60 hover:bg-rose-800 text-rose-200 text-sm font-medium rounded-lg border border-rose-800/80 transition flex items-center gap-1.5" title="Reset all packages to default PDF data">
                    <i class="fa-solid fa-arrow-rotate-left"></i>
                    <span class="hidden sm:inline">Reset</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content Area -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 space-y-6">

        <!-- Active Package Title Banner & Quick Add -->
        <div class="flex flex-col sm:flex-row sm:items-center justify-between bg-white p-5 rounded-2xl shadow-sm border border-slate-200 gap-4">
            <div>
                <div class="flex items-center gap-2 text-xs font-semibold uppercase tracking-wider text-blue-600">
                    <span class="inline-block w-2 h-2 rounded-full bg-blue-600 animate-pulse"></span>
                    Selected Active Package Data
                </div>
                <h2 id="activePackageTitle" class="text-2xl font-extrabold text-slate-900 mt-0.5">Package 1</h2>
                <p class="text-xs text-slate-500 mt-1">Real-time tracked parameters & scope achievement status.</p>
            </div>
            
            <div class="flex items-center gap-3">
                <button onclick="openActivityModal()" class="w-full sm:w-auto px-4 py-2.5 bg-blue-600 hover:bg-blue-700 text-white text-sm font-semibold rounded-xl shadow-md hover:shadow-lg transition flex items-center justify-center gap-2">
                    <i class="fa-solid fa-circle-plus"></i>
                    <span>Add New Activity</span>
                </button>
            </div>
        </div>

        <!-- Metric KPI Cards -->
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
            <!-- Total Scope Card -->
            <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm relative overflow-hidden group hover:border-blue-300 transition">
                <div class="absolute top-0 right-0 w-24 h-24 bg-blue-50 rounded-bl-full -mr-4 -mt-4 transition-transform group-hover:scale-110"></div>
                <div class="relative z-10">
                    <div class="flex items-center justify-between">
                        <span class="text-xs font-bold uppercase tracking-wider text-slate-500">Total Scope</span>
                        <div class="p-2 bg-blue-100 text-blue-600 rounded-lg">
                            <i class="fa-solid fa-layer-group"></i>
                        </div>
                    </div>
                    <div id="kpiTotalScope" class="text-2xl font-black text-slate-900 mt-3">0.00</div>
                    <div class="text-xs text-slate-400 mt-1 font-medium">Sum of all activity scope</div>
                </div>
            </div>

            <!-- Cumulative Achieved Card -->
            <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm relative overflow-hidden group hover:border-emerald-300 transition">
                <div class="absolute top-0 right-0 w-24 h-24 bg-emerald-50 rounded-bl-full -mr-4 -mt-4 transition-transform group-hover:scale-110"></div>
                <div class="relative z-10">
                    <div class="flex items-center justify-between">
                        <span class="text-xs font-bold uppercase tracking-wider text-slate-500">Achieved Scope</span>
                        <div class="p-2 bg-emerald-100 text-emerald-600 rounded-lg">
                            <i class="fa-solid fa-circle-check"></i>
                        </div>
                    </div>
                    <div id="kpiAchieved" class="text-2xl font-black text-emerald-600 mt-3">0.00</div>
                    <div class="text-xs text-slate-400 mt-1 font-medium">Cumulative completed till date</div>
                </div>
            </div>

            <!-- Balance Scope Card -->
            <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm relative overflow-hidden group hover:border-amber-300 transition">
                <div class="absolute top-0 right-0 w-24 h-24 bg-amber-50 rounded-bl-full -mr-4 -mt-4 transition-transform group-hover:scale-110"></div>
                <div class="relative z-10">
                    <div class="flex items-center justify-between">
                        <span class="text-xs font-bold uppercase tracking-wider text-slate-500">Balance Scope</span>
                        <div class="p-2 bg-amber-100 text-amber-600 rounded-lg">
                            <i class="fa-solid fa-clock font-normal"></i>
                        </div>
                    </div>
                    <div id="kpiBalance" class="text-2xl font-black text-amber-600 mt-3">0.00</div>
                    <div class="text-xs text-slate-400 mt-1 font-medium">Remaining work to execute</div>
                </div>
            </div>

            <!-- Overall Progress % Card -->
            <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm relative overflow-hidden group hover:border-purple-300 transition">
                <div class="absolute top-0 right-0 w-24 h-24 bg-purple-50 rounded-bl-full -mr-4 -mt-4 transition-transform group-hover:scale-110"></div>
                <div class="relative z-10">
                    <div class="flex items-center justify-between">
                        <span class="text-xs font-bold uppercase tracking-wider text-slate-500">Package Progress</span>
                        <div class="p-2 bg-purple-100 text-purple-600 rounded-lg">
                            <i class="fa-solid fa-chart-line"></i>
                        </div>
                    </div>
                    <div id="kpiProgress" class="text-2xl font-black text-purple-600 mt-3">0.00%</div>
                    <div class="w-full bg-slate-100 rounded-full h-2 mt-2 overflow-hidden">
                        <div id="kpiProgressBar" class="bg-purple-600 h-2 rounded-full transition-all duration-500" style="width: 0%"></div>
                    </div>
                </div>
            </div>
        </div>

        <!-- All Packages Overview Section -->
        <div class="bg-white p-6 rounded-2xl border border-slate-200 shadow-sm">
            <div class="flex flex-col sm:flex-row sm:items-center justify-between mb-4 gap-2">
                <div>
                    <h3 class="text-base font-bold text-slate-900 flex items-center gap-2">
                        <i class="fa-solid fa-chart-simple text-blue-600"></i>
                        6-Package Comparison Matrix
                    </h3>
                    <p class="text-xs text-slate-500">Overall progress completion across all assigned contract packages.</p>
                </div>
                <span class="text-xs font-medium bg-slate-100 text-slate-600 px-2.5 py-1 rounded-md self-start sm:self-auto">Live Sync</span>
            </div>
            
            <div id="packagesComparisonContainer" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 pt-2">
                <!-- Dynamic progress bars for 6 packages -->
            </div>
        </div>

        <!-- Detailed Activity Table Section -->
        <div class="bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden">
            <!-- Table Header Toolbar -->
            <div class="p-5 border-b border-slate-100 flex flex-col md:flex-row items-center justify-between gap-4 bg-slate-50/50">
                <div>
                    <h3 class="text-base font-bold text-slate-900 flex items-center gap-2">
                        <i class="fa-solid fa-list-check text-blue-600"></i>
                        Activities & Progress Breakdown
                    </h3>
                    <p class="text-xs text-slate-500">Comprehensive schedule data with dates, units, scope, and progress percentage.</p>
                </div>

                <div class="flex flex-wrap items-center gap-3 w-full md:w-auto">
                    <!-- Search Input -->
                    <div class="relative flex-grow sm:flex-grow-0">
                        <i class="fa-solid fa-magnifying-glass absolute left-3 top-1/2 -translate-y-1/2 text-slate-400 text-xs"></i>
                        <input type="text" id="searchInput" oninput="renderTable()" placeholder="Search activities..." class="w-full sm:w-64 pl-8 pr-3 py-1.5 text-xs bg-white border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500/20 focus:border-blue-500">
                    </div>
                </div>
            </div>

            <!-- Table Container -->
            <div class="overflow-x-auto">
                <table class="w-full text-left border-collapse">
                    <thead>
                        <tr class="bg-slate-100/70 border-b border-slate-200 text-[11px] font-bold text-slate-600 uppercase tracking-wider">
                            <th class="py-3.5 px-4 w-12 text-center">#</th>
                            <th class="py-3.5 px-4 min-w-[220px]">Activity Description</th>
                            <th class="py-3.5 px-3 min-w-[100px]">Start Date</th>
                            <th class="py-3.5 px-3 min-w-[100px]">Finish Date</th>
                            <th class="py-3.5 px-3 text-center">U.O.M</th>
                            <th class="py-3.5 px-3 text-right">Total Scope</th>
                            <th class="py-3.5 px-3 text-right">Balance</th>
                            <th class="py-3.5 px-3 text-right">Achieved</th>
                            <th class="py-3.5 px-3 text-right">Progress %</th>
                            <th class="py-3.5 px-3 text-center">Status</th>
                            <th class="py-3.5 px-4 text-center w-24">Actions</th>
                        </tr>
                    </thead>
                    <tbody id="activityTableBody" class="divide-y divide-slate-100 text-xs text-slate-700">
                        <!-- Table rows populated dynamically -->
                    </tbody>
                </table>
            </div>
            
            <!-- Table Footer Stats -->
            <div class="p-4 bg-slate-50 border-t border-slate-200 flex flex-col sm:flex-row items-center justify-between text-xs text-slate-500 gap-2">
                <div id="tableRecordCount">Showing 0 activities</div>
                <div class="flex items-center gap-4 font-medium">
                    <span>Legend:</span>
                    <span class="flex items-center gap-1.5"><span class="w-2.5 h-2.5 rounded-full bg-emerald-500"></span> 100% Done</span>
                    <span class="flex items-center gap-1.5"><span class="w-2.5 h-2.5 rounded-full bg-amber-500"></span> In Progress</span>
                    <span class="flex items-center gap-1.5"><span class="w-2.5 h-2.5 rounded-full bg-slate-300"></span> Not Started</span>
                </div>
            </div>
        </div>

    </main>

    <!-- Footer -->
    <footer class="bg-white border-t border-slate-200 py-4 mt-8">
        <div class="max-w-7xl mx-auto px-4 text-center text-xs text-slate-500">
            Metro Track Daily Progress Reporting (DPR) Portal &copy; 2026. Data dynamically stored in browser LocalStorage.
        </div>
    </footer>

    <!-- MODAL 1: Add / Edit Activity Modal -->
    <div id="activityModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-white rounded-2xl shadow-2xl max-w-lg w-full overflow-hidden transform transition-all">
            <div class="bg-slate-900 px-6 py-4 flex items-center justify-between text-white">
                <h3 id="modalTitle" class="font-bold text-base flex items-center gap-2">
                    <i class="fa-solid fa-pen-to-square text-blue-400"></i>
                    <span>Add New Activity</span>
                </h3>
                <button onclick="closeActivityModal()" class="text-slate-400 hover:text-white transition">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>
            
            <form id="activityForm" onsubmit="saveActivity(event)" class="p-6 space-y-4">
                <input type="hidden" id="editIndex" value="-1">

                <div>
                    <label class="block text-xs font-semibold text-slate-700 uppercase mb-1">Activity Name *</label>
                    <input type="text" id="inputName" required placeholder="e.g. Track Installation" class="w-full px-3 py-2 text-xs border border-slate-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 uppercase mb-1">Start Date</label>
                        <input type="text" id="inputStart" placeholder="DD/MM/YYYY" class="w-full px-3 py-2 text-xs border border-slate-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 uppercase mb-1">Finish Date</label>
                        <input type="text" id="inputFinish" placeholder="DD/MM/YYYY" class="w-full px-3 py-2 text-xs border border-slate-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 uppercase mb-1">U.O.M *</label>
                        <select id="inputUom" required class="w-full px-3 py-2 text-xs border border-slate-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                            <option value="TRM">TRM</option>
                            <option value="Nos.">Nos.</option>
                            <option value="MT">MT</option>
                            <option value="Sqm">Sqm</option>
                            <option value="Cu.m">Cu.m</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 uppercase mb-1">Total Scope *</label>
                        <input type="number" step="any" id="inputTotal" required min="0" oninput="calculateBalanceAndProgress()" placeholder="0.00" class="w-full px-3 py-2 text-xs border border-slate-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 uppercase mb-1">Cumulative Achieved *</label>
                        <input type="number" step="any" id="inputAchieved" required min="0" oninput="calculateBalanceAndProgress()" placeholder="0.00" class="w-full px-3 py-2 text-xs border border-slate-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 uppercase mb-1">Calculated Balance</label>
                        <input type="number" step="any" id="inputBalance" readonly placeholder="Auto-calculated" class="w-full px-3 py-2 text-xs bg-slate-100 border border-slate-300 rounded-lg text-slate-600 font-semibold focus:outline-none">
                    </div>
                </div>

                <div>
                    <label class="block text-xs font-semibold text-slate-700 uppercase mb-1">Calculated Progress %</label>
                    <input type="text" id="inputProgress" readonly placeholder="Auto-calculated" class="w-full px-3 py-2 text-xs bg-slate-100 border border-slate-300 rounded-lg text-blue-600 font-bold focus:outline-none">
                </div>

                <div class="pt-4 flex items-center justify-end gap-3 border-t border-slate-100">
                    <button type="button" onclick="closeActivityModal()" class="px-4 py-2 text-xs font-medium text-slate-600 hover:text-slate-800 bg-slate-100 hover:bg-slate-200 rounded-lg transition">Cancel</button>
                    <button type="submit" class="px-4 py-2 text-xs font-semibold text-white bg-blue-600 hover:bg-blue-700 rounded-lg shadow transition">Save Activity</button>
                </div>
            </form>
        </div>
    </div>

    <!-- MODAL 2: Rename Package Modal -->
    <div id="renameModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-white rounded-2xl shadow-2xl max-w-md w-full overflow-hidden">
            <div class="bg-slate-900 px-6 py-4 flex items-center justify-between text-white">
                <h3 class="font-bold text-base flex items-center gap-2">
                    <i class="fa-solid fa-pen text-amber-400"></i>
                    <span>Rename Active Package</span>
                </h3>
                <button onclick="closeRenameModal()" class="text-slate-400 hover:text-white transition">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>
            
            <form onsubmit="savePackageName(event)" class="p-6 space-y-4">
                <div>
                    <label class="block text-xs font-semibold text-slate-700 uppercase mb-1">Package Custom Name</label>
                    <input type="text" id="newPackageNameInput" required placeholder="Enter new package title..." class="w-full px-3 py-2 text-xs border border-slate-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-amber-500">
                    <p class="text-[11px] text-slate-400 mt-1">This name will be saved in LocalStorage and updated across all views.</p>
                </div>

                <div class="pt-2 flex items-center justify-end gap-3">
                    <button type="button" onclick="closeRenameModal()" class="px-4 py-2 text-xs font-medium text-slate-600 hover:text-slate-800 bg-slate-100 hover:bg-slate-200 rounded-lg transition">Cancel</button>
                    <button type="submit" class="px-4 py-2 text-xs font-semibold text-white bg-amber-600 hover:bg-amber-700 rounded-lg shadow transition">Save Name</button>
                </div>
            </form>
        </div>
    </div>

    <!-- JavaScript Application Logic -->
    <script>
        // Storage Key
        const STORAGE_KEY = 'METRO_DPR_MULTI_PACKAGE_DATA';

        // Default Master Data populated with Package 1 PDF specifications
        const defaultPackage1Activities = [
            { sr: 1, name: "Civil Access to Track Team (P106 to P269) including 3rd line & Div Track", start: "22/04/2024", finish: "", uom: "TRM", total: 22308.494, balance: 2079.302, achieved: 20229.192, progress: 90.68 },
            { sr: 2, name: "Asbuilt Survey & Detailing Work", start: "24/04/2024", finish: "", uom: "TRM", total: 22308.494, balance: 2587.302, achieved: 19721.192, progress: 88.40 },
            { sr: 3, name: "Flash Butt Welding", start: "01/06/2024", finish: "", uom: "TRM", total: 22308.494, balance: 2079.302, achieved: 20229.192, progress: 90.68 },
            { sr: 4, name: "Track Installation", start: "17/08/2024", finish: "", uom: "TRM", total: 22308.494, balance: 2175.365, achieved: 20133.129, progress: 90.25 },
            { sr: 5, name: "Rear Work", start: "10/10/2024", finish: "", uom: "TRM", total: 22308.494, balance: 2971.949, achieved: 19336.545, progress: 86.68 },
            { sr: 6, name: "Rail Painting", start: "08/01/2025", finish: "", uom: "TRM", total: 22308.494, balance: 4156.865, achieved: 18151.629, progress: 81.37 },
            { sr: 7, name: "Destressing Work ATW", start: "05/03/2025", finish: "17/05/2026", uom: "TRM", total: 22308.494, balance: 3332.852, achieved: 18975.642, progress: 85.06 },
            { sr: 8, name: "Final Parameter", start: "03/04/2025", finish: "", uom: "TRM", total: 22308.494, balance: 4827.400, achieved: 17481.094, progress: 78.36 },
            { sr: 9, name: "Turnout Installation", start: "16/11/2024", finish: "17/02/2025", uom: "Nos.", total: 10, balance: 0, achieved: 10, progress: 100.00 },
            { sr: 10, name: "Scissor Cross-over Installation & Rear Work", start: "25/02/2026", finish: "02/04/2026", uom: "Nos.", total: 1, balance: 0, achieved: 1, progress: 100.00 },
            { sr: 11, name: "CMRS Inspection / Approval", start: "02/01/2026", finish: "", uom: "TRM", total: 22308.494, balance: 11579.850, achieved: 10728.644, progress: 48.09 },
            { sr: 12, name: "Rail Handover", start: "31/05/2024", finish: "", uom: "Nos.", total: 2342, balance: 688, achieved: 1654, progress: 70.62 },
            { sr: 13, name: "Handover Track to PST", start: "-", finish: "-", uom: "TRM", total: 22308.494, balance: 4437, achieved: 17871.574, progress: 80.11 },
            { sr: 14, name: "Handover Track to Signalling with Design Speed", start: "-", finish: "-", uom: "TRM", total: 22308.494, balance: 8532, achieved: 13776.266, progress: 61.75 },
            { sr: 15, name: "Scissor Crossover Handover to Signalling", start: "-", finish: "-", uom: "Nos.", total: 1, balance: 0, achieved: 1, progress: 100.00 },
            { sr: 16, name: "Earthing Connectivity", start: "-", finish: "-", uom: "TRM", total: 22308.494, balance: 3929, achieved: 18379.574, progress: 82.39 },
            { sr: 17, name: "Marking of Station on Curves & Turnouts", start: "-", finish: "-", uom: "TRM", total: 5720.732, balance: 1061, achieved: 4659.293, progress: 81.45 },
            { sr: 18, name: "USFD Testing ATW", start: "-", finish: "-", uom: "Nos.", total: 82, balance: 0, achieved: 82, progress: 100.00 },
            { sr: 19, name: "USFD Testing FBW", start: "-", finish: "-", uom: "Nos.", total: 2552, balance: 0, achieved: 2552, progress: 100.00 },
            { sr: 20, name: "Fixing of Signage Board", start: "-", finish: "-", uom: "TRM", total: 22308.494, balance: 8532, achieved: 13776.27, progress: 61.75 }
        ];

        // Sample placeholder data for Packages 2 to 6
        function generateSamplePackage(namePrefix, completionRatio) {
            return defaultPackage1Activities.map(act => {
                const total = act.total;
                const achieved = parseFloat((total * completionRatio).toFixed(3));
                const balance = parseFloat((total - achieved).toFixed(3));
                const progress = parseFloat(((achieved / total) * 100).toFixed(2));
                return { ...act, total, achieved, balance, progress };
            });
        }

        const defaultAppStructure = {
            activePackageKey: 'pkg1',
            packages: {
                pkg1: { name: 'Package 1 (MM L09 & L07 CA-167)', activities: defaultPackage1Activities },
                pkg2: { name: 'Package 2 (North Extension Corridor)', activities: generateSamplePackage('Package 2', 0.72) },
                pkg3: { name: 'Package 3 (South Elevated Line)', activities: generateSamplePackage('Package 3', 0.55) },
                pkg4: { name: 'Package 4 (Depot Connection Line)', activities: generateSamplePackage('Package 4', 0.88) },
                pkg5: { name: 'Package 5 (Underground Phase II)', activities: generateSamplePackage('Package 5', 0.40) },
                pkg6: { name: 'Package 6 (East-West Interchange Track)', activities: generateSamplePackage('Package 6', 0.25) }
            }
        };

        // State Store
        let appState = {};

        // Load or initialize state
        function initApp() {
            const stored = localStorage.getItem(STORAGE_KEY);
            if (stored) {
                try {
                    appState = JSON.parse(stored);
                } catch (e) {
                    console.error('Failed to parse localstorage, resetting', e);
                    appState = JSON.parse(JSON.stringify(defaultAppStructure));
                }
            } else {
                appState = JSON.parse(JSON.stringify(defaultAppStructure));
                saveToLocalStorage();
            }

            renderPackageSelectorOptions();
            renderDashboard();
        }

        // Save current state to LocalStorage
        function saveToLocalStorage() {
            localStorage.setItem(STORAGE_KEY, JSON.stringify(appState));
        }

        // Render Dropdown options
        function renderPackageSelectorOptions() {
            const select = document.getElementById('packageSelect');
            select.innerHTML = '';
            
            Object.keys(appState.packages).forEach(key => {
                const option = document.createElement('option');
                option.value = key;
                option.textContent = appState.packages[key].name;
                if (key === appState.activePackageKey) {
                    option.selected = true;
                }
                select.appendChild(option);
            });
        }

        // Switch Active Package
        function switchPackage(key) {
            appState.activePackageKey = key;
            saveToLocalStorage();
            renderDashboard();
        }

        // Render whole UI
        function renderDashboard() {
            const activeKey = appState.activePackageKey;
            const currentPackage = appState.packages[activeKey];

            // Set Title
            document.getElementById('activePackageTitle').innerText = currentPackage.name;

            // Recalculate KPIs & Render Table
            renderKPIs(currentPackage.activities);
            renderTable();
            renderPackageComparison();
        }

        // Calculate and display KPIs
        function renderKPIs(activities) {
            let totalScope = 0;
            let totalAchieved = 0;
            let totalBalance = 0;

            activities.forEach(act => {
                totalScope += Number(act.total) || 0;
                totalAchieved += Number(act.achieved) || 0;
                totalBalance += Number(act.balance) || 0;
            });

            const overallProg = totalScope > 0 ? (totalAchieved / totalScope) * 100 : 0;

            document.getElementById('kpiTotalScope').innerText = totalScope.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 2 });
            document.getElementById('kpiAchieved').innerText = totalAchieved.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 2 });
            document.getElementById('kpiBalance').innerText = totalBalance.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 2 });
            document.getElementById('kpiProgress').innerText = overallProg.toFixed(2) + '%';
            document.getElementById('kpiProgressBar').style.width = Math.min(overallProg, 100) + '%';
        }

        // Render Activity Data Table
        function renderTable() {
            const activeKey = appState.activePackageKey;
            const activities = appState.packages[activeKey].activities;
            const tbody = document.getElementById('activityTableBody');
            const searchVal = document.getElementById('searchInput').value.toLowerCase().trim();

            tbody.innerHTML = '';

            const filtered = activities.filter(act => act.name.toLowerCase().includes(searchVal));

            if (filtered.length === 0) {
                tbody.innerHTML = `
                    <tr>
                        <td colspan="11" class="py-8 text-center text-slate-400">
                            <i class="fa-solid fa-folder-open text-3xl mb-2"></i>
                            <p>No activity records found matching query.</p>
                        </td>
                    </tr>`;
                document.getElementById('tableRecordCount').innerText = 'Showing 0 activities';
                return;
            }

            filtered.forEach((act, idx) => {
                const originalIndex = activities.indexOf(act);
                
                // Badge color calculation
                let statusBadge = '';
                if (act.progress >= 100) {
                    statusBadge = `<span class="px-2 py-0.5 rounded-full text-[10px] font-bold bg-emerald-100 text-emerald-700 border border-emerald-200">Completed</span>`;
                } else if (act.progress > 0) {
                    statusBadge = `<span class="px-2 py-0.5 rounded-full text-[10px] font-bold bg-amber-100 text-amber-700 border border-amber-200">In Progress</span>`;
                } else {
                    statusBadge = `<span class="px-2 py-0.5 rounded-full text-[10px] font-bold bg-slate-100 text-slate-600 border border-slate-200">Pending</span>`;
                }

                const tr = document.createElement('tr');
                tr.className = 'hover:bg-slate-50/80 transition border-b border-slate-100';
                tr.innerHTML = `
                    <td class="py-3 px-4 text-center font-semibold text-slate-400">${act.sr || (originalIndex + 1)}</td>
                    <td class="py-3 px-4 font-semibold text-slate-900">${escapeHtml(act.name)}</td>
                    <td class="py-3 px-3 text-slate-500 font-mono text-[11px]">${act.start || '-'}</td>
                    <td class="py-3 px-3 text-slate-500 font-mono text-[11px]">${act.finish || '-'}</td>
                    <td class="py-3 px-3 text-center"><span class="px-2 py-0.5 bg-slate-100 text-slate-700 rounded text-[10px] font-bold">${act.uom}</span></td>
                    <td class="py-3 px-3 text-right font-medium">${Number(act.total).toLocaleString(undefined, {minimumFractionDigits: 2})}</td>
                    <td class="py-3 px-3 text-right font-medium text-amber-600">${Number(act.balance).toLocaleString(undefined, {minimumFractionDigits: 2})}</td>
                    <td class="py-3 px-3 text-right font-semibold text-emerald-600">${Number(act.achieved).toLocaleString(undefined, {minimumFractionDigits: 2})}</td>
                    <td class="py-3 px-3 text-right font-bold text-slate-900">${Number(act.progress).toFixed(2)}%</td>
                    <td class="py-3 px-3 text-center">${statusBadge}</td>
                    <td class="py-3 px-4 text-center">
                        <div class="flex items-center justify-center gap-1.5">
                            <button onclick="openActivityModal(${originalIndex})" class="p-1.5 text-blue-600 hover:bg-blue-50 rounded-md transition" title="Edit Activity">
                                <i class="fa-solid fa-pen-to-square"></i>
                            </button>
                            <button onclick="deleteActivity(${originalIndex})" class="p-1.5 text-rose-600 hover:bg-rose-50 rounded-md transition" title="Delete Activity">
                                <i class="fa-solid fa-trash-can"></i>
                            </button>
                        </div>
                    </td>
                `;
                tbody.appendChild(tr);
            });

            document.getElementById('tableRecordCount').innerText = `Showing ${filtered.length} of ${activities.length} activities`;
        }

        // Render Multi-Package Comparison Progress Bars
        function renderPackageComparison() {
            const container = document.getElementById('packagesComparisonContainer');
            container.innerHTML = '';

            Object.keys(appState.packages).forEach(key => {
                const pkg = appState.packages[key];
                
                // calculate overall package progress
                let tScope = 0;
                let tAchieved = 0;
                pkg.activities.forEach(a => {
                    tScope += Number(a.total) || 0;
                    tAchieved += Number(a.achieved) || 0;
                });
                const pkgProgress = tScope > 0 ? (tAchieved / tScope) * 100 : 0;

                const isActive = key === appState.activePackageKey;
                const borderClass = isActive ? 'border-blue-500 bg-blue-50/30' : 'border-slate-200 bg-white';

                const card = document.createElement('div');
                card.className = `p-4 rounded-xl border ${borderClass} shadow-sm transition hover:shadow-md cursor-pointer`;
                card.onclick = () => switchPackage(key);

                card.innerHTML = `
                    <div class="flex items-center justify-between mb-2">
                        <div class="font-bold text-xs truncate max-w-[180px] text-slate-800" title="${escapeHtml(pkg.name)}">
                            ${isActive ? '<i class="fa-solid fa-circle-check text-blue-600 mr-1.5"></i>' : ''}${escapeHtml(pkg.name)}
                        </div>
                        <span class="text-xs font-black text-slate-900">${pkgProgress.toFixed(1)}%</span>
                    </div>
                    <div class="w-full bg-slate-200 rounded-full h-2 overflow-hidden">
                        <div class="bg-blue-600 h-2 rounded-full transition-all duration-500" style="width: ${Math.min(pkgProgress, 100)}%"></div>
                    </div>
                    <div class="flex justify-between items-center mt-2 text-[10px] text-slate-400">
                        <span>${pkg.activities.length} Activities</span>
                        <span>${tAchieved.toLocaleString(undefined, {maximumFractionDigits:0})} / ${tScope.toLocaleString(undefined, {maximumFractionDigits:0})}</span>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        // --- Activity Modal Functions ---
        function openActivityModal(index = -1) {
            const modal = document.getElementById('activityModal');
            const activeKey = appState.activePackageKey;
            const activities = appState.packages[activeKey].activities;

            document.getElementById('editIndex').value = index;

            if (index >= 0) {
                const act = activities[index];
                document.getElementById('modalTitle').innerHTML = '<i class="fa-solid fa-pen-to-square text-blue-400"></i> Edit Activity';
                document.getElementById('inputName').value = act.name;
                document.getElementById('inputStart').value = act.start || '';
                document.getElementById('inputFinish').value = act.finish || '';
                document.getElementById('inputUom').value = act.uom || 'TRM';
                document.getElementById('inputTotal').value = act.total;
                document.getElementById('inputAchieved').value = act.achieved;
                calculateBalanceAndProgress();
            } else {
                document.getElementById('modalTitle').innerHTML = '<i class="fa-solid fa-circle-plus text-blue-400"></i> Add New Activity';
                document.getElementById('activityForm').reset();
                document.getElementById('editIndex').value = -1;
            }

            modal.classList.remove('hidden');
        }

        function closeActivityModal() {
            document.getElementById('activityModal').classList.add('hidden');
        }

        function calculateBalanceAndProgress() {
            const total = parseFloat(document.getElementById('inputTotal').value) || 0;
            const achieved = parseFloat(document.getElementById('inputAchieved').value) || 0;

            const balance = Math.max(0, total - achieved);
            const progress = total > 0 ? ((achieved / total) * 100).toFixed(2) : '0.00';

            document.getElementById('inputBalance').value = balance.toFixed(3);
            document.getElementById('inputProgress').value = progress + '%';
        }

        function saveActivity(e) {
            e.preventDefault();
            const activeKey = appState.activePackageKey;
            const index = parseInt(document.getElementById('editIndex').value);

            const total = parseFloat(document.getElementById('inputTotal').value) || 0;
            const achieved = parseFloat(document.getElementById('inputAchieved').value) || 0;
            const balance = Math.max(0, total - achieved);
            const progress = total > 0 ? parseFloat(((achieved / total) * 100).toFixed(2)) : 0;

            const newAct = {
                sr: index >= 0 ? appState.packages[activeKey].activities[index].sr : appState.packages[activeKey].activities.length + 1,
                name: document.getElementById('inputName').value.trim(),
                start: document.getElementById('inputStart').value.trim(),
                finish: document.getElementById('inputFinish').value.trim(),
                uom: document.getElementById('inputUom').value,
                total: total,
                achieved: achieved,
                balance: balance,
                progress: progress
            };

            if (index >= 0) {
                appState.packages[activeKey].activities[index] = newAct;
            } else {
                appState.packages[activeKey].activities.push(newAct);
            }

            saveToLocalStorage();
            closeActivityModal();
            renderDashboard();
        }

        function deleteActivity(index) {
            if (confirm("Are you sure you want to delete this activity?")) {
                const activeKey = appState.activePackageKey;
                appState.packages[activeKey].activities.splice(index, 1);
                saveToLocalStorage();
                renderDashboard();
            }
        }

        // --- Package Rename Modal Functions ---
        function openRenameModal() {
            const activeKey = appState.activePackageKey;
            document.getElementById('newPackageNameInput').value = appState.packages[activeKey].name;
            document.getElementById('renameModal').classList.remove('hidden');
        }

        function closeRenameModal() {
            document.getElementById('renameModal').classList.add('hidden');
        }

        function savePackageName(e) {
            e.preventDefault();
            const activeKey = appState.activePackageKey;
            const newName = document.getElementById('newPackageNameInput').value.trim();

            if (newName) {
                appState.packages[activeKey].name = newName;
                saveToLocalStorage();
                renderPackageSelectorOptions();
                renderDashboard();
                closeRenameModal();
            }
        }

        // Reset Data to Default
        function resetAllData() {
            if (confirm("This will reset all 6 packages back to the original default PDF dataset. Continue?")) {
                localStorage.removeItem(STORAGE_KEY);
                appState = JSON.parse(JSON.stringify(defaultAppStructure));
                saveToLocalStorage();
                renderPackageSelectorOptions();
                renderDashboard();
            }
        }

        // Export active Package data to CSV
        function exportToCSV() {
            const activeKey = appState.activePackageKey;
            const pkg = appState.packages[activeKey];
            
            let csvContent = "data:text/csv;charset=utf-8,";
            csvContent += "Sr No,Activity Description,Start Date,Finish Date,UOM,Total Scope,Balance Scope,Cumulative Achieved,Progress %\n";

            pkg.activities.forEach(a => {
                const row = [
                    a.sr,
                    `"${a.name.replace(/"/g, '""')}"`,
                    `"${a.start || ''}"`,
                    `"${a.finish || ''}"`,
                    `"${a.uom}"`,
                    a.total,
                    a.balance,
                    a.achieved,
                    a.progress
                ].join(",");
                csvContent += row + "\n";
            });

            const encodedUri = encodeURI(csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", `${pkg.name.replace(/[^a-zA-Z0-9]/g, '_')}_DPR_Report.csv`);
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }

        // Utility: HTML Sanitizer
        function escapeHtml(str) {
            if (!str) return '';
            return str.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/'/g, "&#039;");
        }

        // Start App
        window.onload = initApp;
    </script>
</body>
</html>
