# -Growth-Model
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Agrotech Bioscience: Derivative of Growth</title>
    
    <!-- Tailwind CSS for styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Chart.js for interactive visualizations -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    
    <!-- MathJax for rendering beautiful mathematical formulas -->
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

    <!-- Google Fonts: Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
    
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f4fdf4;
            color: #1a4d2e;
        }
        .glass-panel {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.3);
            box-shadow: 0 8px 32px 0 rgba(31, 100, 48, 0.05);
        }
        .fade-in {
            animation: fadeIn 0.4s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body class="min-h-screen p-4 md:p-8">

    <header class="max-w-7xl mx-auto mb-8 text-center md:text-left">
        <h1 class="text-3xl md:text-5xl font-bold text-green-900 mb-2">Agrotech Bioscience Model</h1>
        <p class="text-lg text-green-700">Applying Calculus (Derivatives) to Livestock Growth Rates in Malaysia</p>
    </header>

    <main class="max-w-7xl mx-auto grid grid-cols-1 xl:grid-cols-12 gap-8">
        
        <!-- LEFT PANEL: Theory & Context -->
        <div class="xl:col-span-4 space-y-6">
            <div class="glass-panel rounded-2xl p-6">
                <h2 class="text-xl font-bold mb-3 border-b border-green-200 pb-2">Bioscience Context</h2>
                <p class="text-sm leading-relaxed mb-4">
                    As an Agrotech student in Malaysia, optimizing the yield of local breeds is crucial. This model represents the weight gain of <strong>Ayam Kampung Kacukan (AKK)</strong> over 16 weeks. 
                </p>
                <p class="text-xs text-green-600 italic bg-green-50 p-2 rounded">
                    Data Source Inspiration: Simulated based on generalized growth patterns from the 
                    <a href="#" class="underline hover:text-green-800">MARDI Animal Husbandry Dataset (Ayam Kampung Growth Performance)</a>.
                </p>
            </div>

            <div class="glass-panel rounded-2xl p-6">
                <h2 class="text-xl font-bold mb-3 border-b border-green-200 pb-2">The Mathematics</h2>
                <p class="text-sm mb-4">
                    The growth can be modeled by a cubic polynomial function where \( x \) is the age in weeks, and \( f(x) \) is the body weight in grams.
                </p>
                
                <div class="bg-green-100 p-4 rounded-xl mb-4 text-center">
                    <p class="font-semibold text-sm mb-1 text-green-800">Growth Function (Weight):</p>
                    <p class="text-lg overflow-x-auto">\( f(x) = -0.5x^3 + 12x^2 + 20x + 40 \)</p>
                </div>

                <p class="text-sm mb-4">
                    To find the <strong>rate of change</strong> (how fast the chicken is growing at any exact moment), we find the derivative, \( f'(x) \).
                </p>

                <div class="bg-green-800 text-white p-4 rounded-xl text-center shadow-inner">
                    <p class="font-semibold text-sm mb-1 text-green-200">Derivative Function (Growth Rate):</p>
                    <p class="text-lg overflow-x-auto">\( f'(x) = -1.5x^2 + 24x + 20 \)</p>
                </div>
            </div>
            
            <div class="glass-panel rounded-2xl p-6 bg-gradient-to-br from-green-50 to-emerald-100">
                <h3 class="font-bold text-green-900 mb-2 flex items-center">
                    <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
                    Instructions
                </h3>
                <p class="text-sm text-green-800">
                    <strong>Click anywhere on the blue curve</strong> in the chart to calculate the derivative at that exact week. The app will draw a tangent line to visualize the instantaneous rate of change!
                </p>
            </div>
        </div>

        <!-- RIGHT PANEL: Interactive Chart & Output -->
        <div class="xl:col-span-8 space-y-6 flex flex-col">
            
            <!-- Chart Container -->
            <div class="glass-panel rounded-2xl p-4 md:p-6 flex-grow relative min-h-[400px]">
                <canvas id="growthChart"></canvas>
            </div>

            <!-- Dynamic Output Container (Changes on Click) -->
            <div id="outputBox" class="glass-panel rounded-2xl p-6 hidden">
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-4">
                    <div class="bg-blue-50 p-4 rounded-xl border border-blue-200 text-center">
                        <p class="text-xs text-blue-600 font-bold uppercase tracking-wide">Selected Time (x)</p>
                        <p class="text-2xl font-bold text-blue-900 mt-1">Week <span id="out-week">0</span></p>
                    </div>
                    <div class="bg-green-50 p-4 rounded-xl border border-green-200 text-center">
                        <p class="text-xs text-green-600 font-bold uppercase tracking-wide">Current Weight (f(x))</p>
                        <p class="text-2xl font-bold text-green-900 mt-1"><span id="out-weight">0</span> g</p>
                    </div>
                    <div class="bg-orange-50 p-4 rounded-xl border border-orange-200 text-center shadow-md transform scale-105">
                        <p class="text-xs text-orange-600 font-bold uppercase tracking-wide">Growth Rate (f'(x))</p>
                        <p class="text-2xl font-bold text-orange-900 mt-1"><span id="out-rate">0</span> g/wk</p>
                    </div>
                </div>

                <div class="bg-white p-5 rounded-xl border-l-4 border-green-500 shadow-sm">
                    <h4 class="font-bold text-gray-800 mb-1">👨‍🌾 Agrotechnologist Analysis:</h4>
                    <p id="out-explanation" class="text-gray-600 text-sm leading-relaxed"></p>
                </div>
            </div>

        </div>
    </main>

    <script>
        // Mathematical Functions
        // Weight function: f(x) = -0.5x^3 + 12x^2 + 20x + 40
        function calculateWeight(x) {
            return (-0.5 * Math.pow(x, 3)) + (12 * Math.pow(x, 2)) + (20 * x) + 40;
        }

        // Derivative function (Rate of growth): f'(x) = -1.5x^2 + 24x + 20
        function calculateDerivative(x) {
            return (-1.5 * Math.pow(x, 2)) + (24 * x) + 20;
        }

        // Generate data for weeks 0 to 16
        const labels = [];
        const weightData = [];
        for (let i = 0; i <= 16; i++) {
            labels.push(i);
            weightData.push(calculateWeight(i));
        }

        let myChart;
        const ctx = document.getElementById('growthChart').getContext('2d');

        const initialConfig = {
            type: 'line',
            data: {
                labels: labels,
                datasets: [
                    {
                        label: 'AKK Body Weight (g)',
                        data: weightData,
                        borderColor: '#2563eb', // Blue
                        backgroundColor: 'rgba(37, 99, 235, 0.1)',
                        borderWidth: 3,
                        pointBackgroundColor: '#fff',
                        pointBorderColor: '#2563eb',
                        pointRadius: 5,
                        pointHoverRadius: 8,
                        fill: true,
                        tension: 0.4 // Smooth curve
                    },
                    {
                        // Hidden dataset for the tangent line, updated on click
                        label: "Instantaneous Growth Rate (Tangent)",
                        data: Array(17).fill(null), 
                        borderColor: '#ea580c', // Orange
                        borderWidth: 3,
                        borderDash: [5, 5],
                        pointRadius: 0,
                        fill: false,
                        tension: 0 
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                interaction: {
                    mode: 'index',
                    intersect: false,
                },
                plugins: {
                    title: {
                        display: true,
                        text: 'Ayam Kampung Kacukan (AKK) Growth Curve (0-16 Weeks)',
                        font: { size: 16, family: 'Inter' }
                    },
                    tooltip: {
                        callbacks: {
                            label: function(context) {
                                if(context.datasetIndex === 1) return null; // Hide tooltip for tangent
                                return `Weight: ${context.parsed.y.toFixed(1)} g`;
                            }
                        }
                    }
                },
                scales: {
                    x: {
                        title: { display: true, text: 'Age (Weeks)', font: {weight: 'bold'} }
                    },
                    y: {
                        title: { display: true, text: 'Body Weight (grams)', font: {weight: 'bold'} },
                        suggestedMin: 0
                    }
                },
                onClick: (e, elements) => {
                    if (elements.length > 0) {
                        const dataIndex = elements[0].index;
                        const week = labels[dataIndex];
                        handleGraphClick(week);
                    }
                }
            }
        };

        myChart = new Chart(ctx, initialConfig);

        function handleGraphClick(x) {
            const weight = calculateWeight(x);
            const rate = calculateDerivative(x);

            // Update DOM elements
            document.getElementById('out-week').innerText = x;
            document.getElementById('out-weight').innerText = weight.toFixed(1);
            document.getElementById('out-rate').innerText = rate.toFixed(1);

            // Generate Layman Explanation based on the derivative (rate of change)
            const explanationEl = document.getElementById('out-explanation');
            let explanation = "";

            if (x < 8) {
                explanation = `At week ${x}, the chicken is growing at a rate of <strong>${rate.toFixed(1)} grams per week</strong>. Because \( f''(x) \) is still positive, the growth rate is accelerating. <strong>Agrotech insight:</strong> This is the crucial starter phase. High protein feed is essential here because the bird is rapidly building bone and muscle structure.`;
            } else if (x === 8) {
                explanation = `At week ${x}, we hit the inflection point! The growth rate is at its absolute peak: <strong>${rate.toFixed(1)} grams per week</strong>. <strong>Agrotech insight:</strong> The chicken is gaining weight faster now than at any other point in its life. Nutrient absorption is at its maximum efficiency.`;
            } else if (x > 8 && x < 15) {
                explanation = `At week ${x}, the chicken is still growing (adding <strong>${rate.toFixed(1)} grams per week</strong>), but the rate is slowing down (decelerating). <strong>Agrotech insight:</strong> The bird is approaching mature weight. Feed conversion ratio (FCR) is dropping, meaning it costs more feed to produce the same weight gain. Time to plan for harvest soon!`;
            } else {
                explanation = `At week ${x}, the growth rate has plummeted to just <strong>${rate.toFixed(1)} grams per week</strong>. The curve is flattening out. <strong>Agrotech insight:</strong> Keeping the chickens past this point is economically inefficient. They are consuming feed just for maintenance, not growth. This is the optimal time for market sale.`;
            }

            explanationEl.innerHTML = explanation;

            // Update Tangent Line on the Chart
            // Tangent line equation: y - y1 = m(x - x1)  =>  y = m(x - x1) + y1
            const newTangentData = Array(17).fill(null);
            
            // Draw a line segment spanning 4 weeks (x-2 to x+2) to show the slope
            for (let i = Math.max(0, x - 2); i <= Math.min(16, x + 2); i++) {
                newTangentData[i] = (rate * (i - x)) + weight;
            }

            myChart.data.datasets[1].data = newTangentData;
            myChart.update();

            // Reveal and animate output box
            const outputBox = document.getElementById('outputBox');
            outputBox.classList.remove('hidden');
            
            // Retrigger CSS animation
            outputBox.classList.remove('fade-in');
            void outputBox.offsetWidth; // Trigger reflow
            outputBox.classList.add('fade-in');
        }
    </script>
</body>
</html>
