<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>家庭保单保障分析 - 直观图表版</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --primary: #2c3e50;
            --secondary: #3498db;
            --accent: #e74c3c;
            --light: #ecf0f1;
            --dark: #2c3e50;
            --success: #2ecc71;
            --warning: #f39c12;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Microsoft JhengHei', sans-serif;
        }
        
        body {
            background-color: #f5f7fa;
            color: #333;
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            padding: 30px 20px;
            border-radius: 10px;
            margin-bottom: 30px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            text-align: center;
        }
        
        h1 {
            font-size: 2.2rem;
            margin-bottom: 10px;
        }
        
        .subtitle {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        
        .card {
            background: white;
            border-radius: 10px;
            padding: 25px;
            margin-bottom: 30px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }
        
        .card-title {
            font-size: 1.5rem;
            color: var(--primary);
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid var(--light);
            text-align: center;
        }
        
        .chart-container {
            position: relative;
            height: 400px;
            margin: 20px 0;
        }
        
        .comparison-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .comparison-item {
            background: var(--light);
            padding: 15px;
            border-radius: 8px;
            text-align: center;
        }
        
        .comparison-value {
            font-size: 1.8rem;
            font-weight: bold;
            color: var(--secondary);
            margin: 10px 0;
        }
        
        .radar-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-top: 20px;
        }
        
        .radar-item {
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.08);
            text-align: center;
        }
        
        .radar-title {
            font-size: 1.2rem;
            margin-bottom: 15px;
            color: var(--primary);
        }
        
        .radar-value {
            font-size: 1.5rem;
            font-weight: bold;
            margin: 10px 0;
        }
        
        .coverage-good {
            color: var(--success);
        }
        
        .coverage-bad {
            color: var(--accent);
        }
        
        .future-medical {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .future-item {
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.08);
            text-align: center;
        }
        
        .future-cost {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--accent);
            margin: 10px 0;
        }
        
        .summary {
            background: linear-gradient(135deg, #3498db, #2c3e50);
            color: white;
            padding: 25px;
            border-radius: 10px;
            margin-top: 30px;
        }
        
        .summary-title {
            font-size: 1.5rem;
            margin-bottom: 15px;
            text-align: center;
        }
        
        footer {
            text-align: center;
            margin-top: 50px;
            padding: 20px;
            color: #7f8c8d;
            font-size: 0.9rem;
        }
        
        /* 新增標籤頁樣式 */
        .tab-container {
            margin: 20px 0;
        }
        
        .tab-buttons {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        .tab-button {
            padding: 12px 24px;
            background-color: var(--light);
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 1rem;
            transition: all 0.3s ease;
        }
        
        .tab-button.active {
            background-color: var(--secondary);
            color: white;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        /* 輸入表單樣式 */
        .input-form {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        .form-label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--primary);
        }
        
        .form-input {
            width: 100%;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 6px;
            font-size: 1rem;
            transition: border-color 0.3s;
        }
        
        .form-input:focus {
            border-color: var(--secondary);
            outline: none;
        }
        
        .submit-btn {
            background: linear-gradient(135deg, var(--secondary), var(--primary));
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 8px;
            font-size: 1.1rem;
            cursor: pointer;
            transition: transform 0.3s;
            margin-top: 20px;
            width: 100%;
        }
        
        .submit-btn:hover {
            transform: translateY(-2px);
        }
        
        .input-section {
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            margin-bottom: 30px;
        }
        
        @media (max-width: 768px) {
            .chart-container {
                height: 300px;
            }
            
            .comparison-grid {
                grid-template-columns: 1fr;
            }
            
            .radar-grid {
                grid-template-columns: 1fr;
            }
            
            .future-medical {
                grid-template-columns: 1fr;
            }
            
            .tab-buttons {
                flex-direction: column;
            }
            
            .input-form {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>家庭保單保障分析</h1>
            <p class="subtitle">直觀圖表版 · 國泰人壽 · 顧問：楊平主任</p>
        </header>
        
        <!-- 輸入參數頁面 -->
        <section class="input-section">
            <h2 class="card-title">請輸入您的保單保障內容</h2>
            <form id="insuranceForm">
                <div class="input-form">
                    <div>
                        <div class="form-group">
                            <label class="form-label">一般身故保障 (萬元)</label>
                            <input type="number" class="form-input" id="deathBenefit" value="448.64" step="0.01">
                        </div>
                        <div class="form-group">
                            <label class="form-label">意外身故保障 (萬元)</label>
                            <input type="number" class="form-input" id="accidentDeath" value="660.64" step="0.01">
                        </div>
                        <div class="form-group">
                            <label class="form-label">實支實付醫療限額 (萬元)</label>
                            <input type="number" class="form-input" id="medicalLimit" value="20" step="0.01">
                        </div>
                        <div class="form-group">
                            <label class="form-label">重大疾病一次金 (萬元)</label>
                            <input type="number" class="form-input" id="criticalIllness" value="130" step="0.01">
                        </div>
                    </div>
                    <div>
                        <div class="form-group">
                            <label class="form-label">意外住院日額 (元)</label>
                            <input type="number" class="form-input" id="accidentHospital" value="6500" step="100">
                        </div>
                        <div class="form-group">
                            <label class="form-label">疾病住院日額 (元)</label>
                            <input type="number" class="form-input" id="diseaseHospital" value="5000" step="100">
                        </div>
                        <div class="form-group">
                            <label class="form-label">癌症初次罹患 (萬元)</label>
                            <input type="number" class="form-input" id="cancerBenefit" value="24" step="0.01">
                        </div>
                        <div class="form-group">
                            <label class="form-label">手術險最高給付 (萬元)</label>
                            <input type="number" class="form-input" id="surgeryBenefit" value="16" step="0.01">
                        </div>
                    </div>
                    <div>
                        <div class="form-group">
                            <label class="form-label">失能險月給付 (元)</label>
                            <input type="number" class="form-input" id="disabilityBenefit" value="9150" step="100">
                        </div>
                        <div class="form-group">
                            <label class="form-label">長照險狀態</label>
                            <select class="form-input" id="longTermCare">
                                <option value="0">未啟用</option>
                                <option value="50">基本保障</option>
                                <option value="80">完整保障</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label class="form-label">客戶姓名</label>
                            <input type="text" class="form-input" id="clientName" value="屈伸儀" placeholder="請輸入客戶姓名">
                        </div>
                    </div>
                </div>
                <button type="button" class="submit-btn" onclick="generateAnalysis()">生成保障分析報告</button>
            </form>
        </section>
        
        <!-- 分析結果頁面 -->
        <div id="analysisResults" style="display: none;">
            <section class="card">
                <h2 class="card-title">保障強度雷達圖</h2>
                <p style="text-align: center; margin-bottom: 20px;">9大险种一目了然 · 客戶：<span id="clientNameDisplay">屈伸儀</span></p>
                
                <div class="chart-container">
                    <canvas id="radarChart"></canvas>
                </div>
                
                <div class="radar-grid">
                    <div class="radar-item">
                        <div class="radar-title">身故给付</div>
                        <div class="radar-value" id="deathDisplay">最高660.64萬</div>
                    </div>
                    <div class="radar-item">
                        <div class="radar-title">实支实付</div>
                        <div class="radar-value coverage-bad" id="medicalDisplay">限额20萬</div>
                    </div>
                    <div class="radar-item">
                        <div class="radar-title">意外住院</div>
                        <div class="radar-value" id="accidentHospitalDisplay">日額6,500元</div>
                    </div>
                    <div class="radar-item">
                        <div class="radar-title">癌症险</div>
                        <div class="radar-value" id="cancerDisplay">初次罹患24萬</div>
                    </div>
                    <div class="radar-item">
                        <div class="radar-title">失能险</div>
                        <div class="radar-value" id="disabilityDisplay">月領6,100~1.22萬</div>
                    </div>
                    <div class="radar-item">
                        <div class="radar-title">疾病住院</div>
                        <div class="radar-value" id="diseaseHospitalDisplay">日額4,000~6,000元</div>
                    </div>
                    <div class="radar-item">
                        <div class="radar-title">重大疾病</div>
                        <div class="radar-value" id="criticalDisplay">給付130萬</div>
                    </div>
                    <div class="radar-item">
                        <div class="radar-title">手术险</div>
                        <div class="radar-value" id="surgeryDisplay">最高16萬</div>
                    </div>
                    <div class="radar-item">
                        <div class="radar-title">长照险</div>
                        <div class="radar-value coverage-bad" id="longTermCareDisplay">未启用</div>
                    </div>
                </div>
            </section>
            
            <section class="card">
                <h2 class="card-title">关键保障项目对比</h2>
                
                <div class="comparison-grid">
                    <div class="comparison-item">
                        <h3>一般身故保障</h3>
                        <div class="comparison-value" id="deathBenefitDisplay">448.64萬</div>
                        <p id="deathClientDisplay">屈伸儀</p>
                    </div>
                    <div class="comparison-item">
                        <h3>意外身故保障</h3>
                        <div class="comparison-value" id="accidentDeathDisplay">660.64萬</div>
                        <p id="accidentClientDisplay">屈伸儀</p>
                    </div>
                    <div class="comparison-item">
                        <h3>实支实付医疗限额</h3>
                        <div class="comparison-value" id="medicalLimitDisplay">20萬</div>
                        <p id="medicalClientDisplay">屈伸儀</p>
                    </div>
                    <div class="comparison-item">
                        <h3>重大疾病一次金</h3>
                        <div class="comparison-value" id="criticalIllnessDisplay">130萬</div>
                        <p id="criticalClientDisplay">屈伸儀、陳蘇彥、陳虹霖</p>
                    </div>
                </div>
            </section>
            
            <section class="card">
                <h2 class="card-title">實際醫療開銷 vs 保單賠付</h2>
                
                <div class="tab-container">
                    <div class="tab-buttons">
                        <button class="tab-button active" data-tab="cancer">癌症治療</button>
                        <button class="tab-button" data-tab="pelvis">骨盆粉碎性骨折</button>
                        <button class="tab-button" data-tab="stroke">急性腦中風</button>
                        <button class="tab-button" data-tab="heart">冠狀動脈繞道手術</button>
                    </div>
                    
                    <!-- 癌症治療標籤頁 -->
                    <div class="tab-content active" id="cancer-tab">
                        <p style="text-align: center; margin-bottom: 20px;">癌症三期新式治疗总费用100万元分析</p>
                        
                        <div class="chart-container">
                            <canvas id="cancerCostChart"></canvas>
                        </div>
                        
                        <div class="comparison-grid">
                            <div class="comparison-item">
                                <h3>总治疗费用</h3>
                                <div class="comparison-value">100萬</div>
                                <p>标靶/基因治疗</p>
                            </div>
                            <div class="comparison-item">
                                <h3>健保覆盖</h3>
                                <div class="comparison-value">10萬</div>
                                <p>部分项目给付</p>
                            </div>
                            <div class="comparison-item">
                                <h3>保单赔付</h3>
                                <div class="comparison-value" id="cancerPayout">44萬</div>
                                <p>实支<span id="cancerMedicalPayout">20</span>万+癌症<span id="cancerCancerPayout">24</span>万</p>
                            </div>
                            <div class="comparison-item">
                                <h3>客户自付</h3>
                                <div class="comparison-value coverage-bad" id="cancerSelfPay">46萬</div>
                                <p>需额外准备</p>
                            </div>
                        </div>
                    </div>
                    
                    <!-- 骨盆粉碎性骨折標籤頁 -->
                    <div class="tab-content" id="pelvis-tab">
                        <p style="text-align: center; margin-bottom: 20px;">骨盆粉碎性骨折重建手术总费用80万元分析</p>
                        
                        <div class="chart-container">
                            <canvas id="pelvisCostChart"></canvas>
                        </div>
                        
                        <div class="comparison-grid">
                            <div class="comparison-item">
                                <h3>总治疗费用</h3>
                                <div class="comparison-value">80萬</div>
                                <p>重建手术+复健</p>
                            </div>
                            <div class="comparison-item">
                                <h3>健保覆盖</h3>
                                <div class="comparison-value">15萬</div>
                                <p>基本手术费用</p>
                            </div>
                            <div class="comparison-item">
                                <h3>保单赔付</h3>
                                <div class="comparison-value" id="pelvisPayout">36萬</div>
                                <p>实支<span id="pelvisMedicalPayout">20</span>万+手术<span id="pelvisSurgeryPayout">16</span>万</p>
                            </div>
                            <div class="comparison-item">
                                <h3>客户自付</h3>
                                <div class="comparison-value coverage-bad" id="pelvisSelfPay">29萬</div>
                                <p>需额外准备</p>
                            </div>
                        </div>
                    </div>
                    
                    <!-- 急性腦中風標籤頁 -->
                    <div class="tab-content" id="stroke-tab">
                        <p style="text-align: center; margin-bottom: 20px;">急性腦中風先進治療總費用120萬元分析</p>
                        
                        <div class="chart-container">
                            <canvas id="strokeCostChart"></canvas>
                        </div>
                        
                        <div class="comparison-grid">
                            <div class="comparison-item">
                                <h3>总治疗费用</h3>
                                <div class="comparison-value">120萬</div>
                                <p>取栓手術+復健</p>
                            </div>
                            <div class="comparison-item">
                                <h3>健保覆盖</h3>
                                <div class="comparison-value">20萬</div>
                                <p>部分項目給付</p>
                            </div>
                            <div class="comparison-item">
                                <h3>保单赔付</h3>
                                <div class="comparison-value" id="strokePayout">50萬</div>
                                <p>实支<span id="strokeMedicalPayout">20</span>万+重大疾病<span id="strokeCriticalPayout">30</span>万</p>
                            </div>
                            <div class="comparison-item">
                                <h3>客户自付</h3>
                                <div class="comparison-value coverage-bad" id="strokeSelfPay">50萬</div>
                                <p>需額外準備</p>
                            </div>
                        </div>
                    </div>
                    
                    <!-- 冠狀動脈繞道手術標籤頁 -->
                    <div class="tab-content" id="heart-tab">
                        <p style="text-align: center; margin-bottom: 20px;">冠狀動脈繞道手術總費用90萬元分析</p>
                        
                        <div class="chart-container">
                            <canvas id="heartCostChart"></canvas>
                        </div>
                        
                        <div class="comparison-grid">
                            <div class="comparison-item">
                                <h3>总治疗费用</h3>
                                <div class="comparison-value">90萬</div>
                                <p>達文西手術+住院</p>
                            </div>
                            <div class="comparison-item">
                                <h3>健保覆盖</h3>
                                <div class="comparison-value">12萬</div>
                                <p>傳統手術給付</p>
                            </div>
                            <div class="comparison-item">
                                <h3>保单赔付</h3>
                                <div class="comparison-value" id="heartPayout">36萬</div>
                                <p>实支<span id="heartMedicalPayout">20</span>万+手术<span id="heartSurgeryPayout">16</span>万</p>
                            </div>
                            <div class="comparison-item">
                                <h3>客户自付</h3>
                                <div class="comparison-value coverage-bad" id="heartSelfPay">42萬</div>
                                <p>需額外準備</p>
                            </div>
                        </div>
                    </div>
                </div>
            </section>
            
            <section class="card">
                <h2 class="card-title">未来医疗趋势与费用预估</h2>
                
                <div class="future-medical">
                    <div class="future-item">
                        <h3>基因编辑治疗</h3>
                        <p>CRISPR等基因编辑技术</p>
                        <div class="future-cost">50-200万元</div>
                        <p>预计2028年后普及</p>
                    </div>
                    
                    <div class="future-item">
                        <h3>AI精准手术机器人</h3>
                        <p>下一代手术机器人</p>
                        <div class="future-cost">40-120万元</div>
                        <p>预计2030年后普及</p>
                    </div>
                    
                    <div class="future-item">
                        <h3>纳米靶向药物</h3>
                        <p>精准送达病灶</p>
                        <div class="future-cost">30-80万元/疗程</div>
                        <p>预计2032年后普及</p>
                    </div>
                    
                    <div class="future-item">
                        <h3>器官3D生物打印</h3>
                        <p>定制化器官移植</p>
                        <div class="future-cost">100-300万元</div>
                        <p>预计2035年后普及</p>
                    </div>
                </div>
                
                <div class="chart-container">
                    <canvas id="futureTrendChart"></canvas>
                </div>
            </section>
            
            <section class="summary">
                <h2 class="summary-title">保障分析总结</h2>
                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
                    <div>
                        <h3 style="margin-bottom: 15px;">✅ 优势保障</h3>
                        <ul style="list-style-type: none;">
                            <li style="padding: 8px 0;">✔ 身故保障充足</li>
                            <li style="padding: 8px 0;">✔ 重大疾病一次金</li>
                            <li style="padding: 8px 0;">✔ 意外住院日额</li>
                        </ul>
                    </div>
                    <div>
                        <h3 style="margin-bottom: 15px;">⚠️ 保障缺口</h3>
                        <ul style="list-style-type: none;">
                            <li style="padding: 8px 0;">❌ 实支实付额度不足</li>
                            <li style="padding: 8px 0;">❌ 长照险未启用</li>
                            <li style="padding: 8px 0;">❌ 高额自费项目覆盖不足</li>
                        </ul>
                    </div>
                </div>
            </section>
        </div>
        
        <footer>
            <p>本分析报告基于提供的保单信息生成，仅供参考。具体保障范围及理赔金额以保单条款为准。</p>
            <p>國泰人壽 · 顾问：楊平主任 0921565682</p>
        </footer>
    </div>

    <script>
        // 儲存圖表實例
        let radarChart, cancerChart, pelvisChart, strokeChart, heartChart, futureChart;
        
        // 生成分析報告
        function generateAnalysis() {
            // 獲取表單數據
            const formData = {
                deathBenefit: parseFloat(document.getElementById('deathBenefit').value),
                accidentDeath: parseFloat(document.getElementById('accidentDeath').value),
                medicalLimit: parseFloat(document.getElementById('medicalLimit').value),
                criticalIllness: parseFloat(document.getElementById('criticalIllness').value),
                accidentHospital: parseInt(document.getElementById('accidentHospital').value),
                diseaseHospital: parseInt(document.getElementById('diseaseHospital').value),
                cancerBenefit: parseFloat(document.getElementById('cancerBenefit').value),
                surgeryBenefit: parseFloat(document.getElementById('surgeryBenefit').value),
                disabilityBenefit: parseInt(document.getElementById('disabilityBenefit').value),
                longTermCare: parseInt(document.getElementById('longTermCare').value),
                clientName: document.getElementById('clientName').value
            };
            
            // 更新顯示數據
            updateDisplayData(formData);
            
            // 計算雷達圖數據
            const radarData = calculateRadarData(formData);
            
            // 生成圖表
            generateCharts(formData, radarData);
            
            // 顯示分析結果
            document.getElementById('analysisResults').style.display = 'block';
            
            // 滾動到分析結果
            document.getElementById('analysisResults').scrollIntoView({ behavior: 'smooth' });
        }
        
        // 更新顯示數據
        function updateDisplayData(data) {
            // 更新客戶姓名
            document.getElementById('clientNameDisplay').textContent = data.clientName;
            
            // 更新雷達圖顯示
            document.getElementById('deathDisplay').textContent = `最高${data.accidentDeath}萬`;
            document.getElementById('medicalDisplay').textContent = `限额${data.medicalLimit}萬`;
            document.getElementById('accidentHospitalDisplay').textContent = `日額${data.accidentHospital.toLocaleString()}元`;
            document.getElementById('cancerDisplay').textContent = `初次罹患${data.cancerBenefit}萬`;
            document.getElementById('disabilityDisplay').textContent = `月領${(data.disabilityBenefit/2).toLocaleString()}~${data.disabilityBenefit.toLocaleString()}元`;
            document.getElementById('diseaseHospitalDisplay').textContent = `日額${(data.diseaseHospital-1000).toLocaleString()}~${data.diseaseHospital.toLocaleString()}元`;
            document.getElementById('criticalDisplay').textContent = `給付${data.criticalIllness}萬`;
            document.getElementById('surgeryDisplay').textContent = `最高${data.surgeryBenefit}萬`;
            
            const longTermCareText = data.longTermCare === 0 ? '未启用' : 
                                   data.longTermCare === 50 ? '基本保障' : '完整保障';
            document.getElementById('longTermCareDisplay').textContent = longTermCareText;
            if (data.longTermCare > 0) {
                document.getElementById('longTermCareDisplay').className = 'radar-value coverage-good';
            }
            
            // 更新關鍵保障項目
            document.getElementById('deathBenefitDisplay').textContent = `${data.deathBenefit}萬`;
            document.getElementById('accidentDeathDisplay').textContent = `${data.accidentDeath}萬`;
            document.getElementById('medicalLimitDisplay').textContent = `${data.medicalLimit}萬`;
            document.getElementById('criticalIllnessDisplay').textContent = `${data.criticalIllness}萬`;
            
            // 更新客戶姓名顯示
            document.getElementById('deathClientDisplay').textContent = data.clientName;
            document.getElementById('accidentClientDisplay').textContent = data.clientName;
            document.getElementById('medicalClientDisplay').textContent = data.clientName;
            document.getElementById('criticalClientDisplay').textContent = `${data.clientName}、陳蘇彥、陳虹霖`;
            
            // 更新醫療案例賠付數據
            updateMedicalCaseData(data);
        }
        
        // 更新醫療案例賠付數據
        function updateMedicalCaseData(data) {
            // 癌症治療
            const cancerPayout = Math.min(data.medicalLimit, 20) + Math.min(data.cancerBenefit, 24);
            const cancerSelfPay = 100 - 10 - cancerPayout;
            document.getElementById('cancerPayout').textContent = `${cancerPayout}萬`;
            document.getElementById('cancerMedicalPayout').textContent = Math.min(data.medicalLimit, 20);
            document.getElementById('cancerCancerPayout').textContent = Math.min(data.cancerBenefit, 24);
            document.getElementById('cancerSelfPay').textContent = `${cancerSelfPay}萬`;
            
            // 骨盆骨折
            const pelvisPayout = Math.min(data.medicalLimit, 20) + Math.min(data.surgeryBenefit, 16);
            const pelvisSelfPay = 80 - 15 - pelvisPayout;
            document.getElementById('pelvisPayout').textContent = `${pelvisPayout}萬`;
            document.getElementById('pelvisMedicalPayout').textContent = Math.min(data.medicalLimit, 20);
            document.getElementById('pelvisSurgeryPayout').textContent = Math.min(data.surgeryBenefit, 16);
            document.getElementById('pelvisSelfPay').textContent = `${pelvisSelfPay}萬`;
            
            // 腦中風
            const strokePayout = Math.min(data.medicalLimit, 20) + Math.min(data.criticalIllness * 0.3, 30);
            const strokeSelfPay = 120 - 20 - strokePayout;
            document.getElementById('strokePayout').textContent = `${strokePayout}萬`;
            document.getElementById('strokeMedicalPayout').textContent = Math.min(data.medicalLimit, 20);
            document.getElementById('strokeCriticalPayout').textContent = Math.min(data.criticalIllness * 0.3, 30);
            document.getElementById('strokeSelfPay').textContent = `${strokeSelfPay}萬`;
            
            // 心臟手術
            const heartPayout = Math.min(data.medicalLimit, 20) + Math.min(data.surgeryBenefit, 16);
            const heartSelfPay = 90 - 12 - heartPayout;
            document.getElementById('heartPayout').textContent = `${heartPayout}萬`;
            document.getElementById('heartMedicalPayout').textContent = Math.min(data.medicalLimit, 20);
            document.getElementById('heartSurgeryPayout').textContent = Math.min(data.surgeryBenefit, 16);
            document.getElementById('heartSelfPay').textContent = `${heartSelfPay}萬`;
        }
        
        // 計算雷達圖數據
        function calculateRadarData(data) {
            // 根據輸入數據計算各項保障的強度（0-100）
            return [
                Math.min((data.deathBenefit / 700) * 100, 100), // 身故给付
                Math.min((data.medicalLimit / 50) * 100, 100),  // 实支实付
                Math.min((data.accidentHospital / 10000) * 100, 100), // 意外住院
                Math.min((data.cancerBenefit / 50) * 100, 100), // 癌症险
                Math.min((data.disabilityBenefit / 20000) * 100, 100), // 失能险
                Math.min((data.diseaseHospital / 10000) * 100, 100), // 疾病住院
                Math.min((data.criticalIllness / 200) * 100, 100), // 重大疾病
                Math.min((data.surgeryBenefit / 30) * 100, 100), // 手术险
                data.longTermCare // 长照险
            ];
        }
        
        // 生成所有圖表
        function generateCharts(formData, radarData) {
            // 清除舊圖表
            if (radarChart) radarChart.destroy();
            if (cancerChart) cancerChart.destroy();
            if (pelvisChart) pelvisChart.destroy();
            if (strokeChart) strokeChart.destroy();
            if (heartChart) heartChart.destroy();
            if (futureChart) futureChart.destroy();
            
            // 保障强度雷达图
            const radarCtx = document.getElementById('radarChart').getContext('2d');
            radarChart = new Chart(radarCtx, {
                type: 'radar',
                data: {
                    labels: ['身故给付', '实支实付', '意外住院', '癌症险', '失能险', '疾病住院', '重大疾病', '手术险', '长照险'],
                    datasets: [{
                        label: '保障强度',
                        data: radarData,
                        backgroundColor: 'rgba(52, 152, 219, 0.2)',
                        borderColor: '#3498db',
                        pointBackgroundColor: '#3498db',
                        pointBorderColor: '#fff',
                        pointHoverBackgroundColor: '#fff',
                        pointHoverBorderColor: '#3498db'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        r: {
                            angleLines: {
                                display: true
                            },
                            suggestedMin: 0,
                            suggestedMax: 100,
                            ticks: {
                                stepSize: 20,
                                callback: function(value) {
                                    return value + '%';
                                }
                            }
                        }
                    },
                    plugins: {
                        legend: {
                            display: false
                        }
                    }
                }
            });
            
            // 癌症治疗费用对比图
            const cancerCtx = document.getElementById('cancerCostChart').getContext('2d');
            const cancerPayout = Math.min(formData.medicalLimit, 20) + Math.min(formData.cancerBenefit, 24);
            const cancerSelfPay = 100 - 10 - cancerPayout;
            
            cancerChart = new Chart(cancerCtx, {
                type: 'bar',
                data: {
                    labels: ['总治疗费用', '健保覆盖', '保单赔付', '客户自付'],
                    datasets: [{
                        label: '金额(万元)',
                        data: [100, 10, cancerPayout, cancerSelfPay],
                        backgroundColor: [
                            'rgba(52, 152, 219, 0.7)',
                            'rgba(46, 204, 113, 0.7)',
                            'rgba(155, 89, 182, 0.7)',
                            'rgba(231, 76, 60, 0.7)'
                        ],
                        borderColor: [
                            '#3498db',
                            '#2ecc71',
                            '#9b59b6',
                            '#e74c3c'
                        ],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            title: {
                                display: true,
                                text: '金额 (万元)'
                            }
                        }
                    },
                    plugins: {
                        legend: {
                            display: false
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return context.parsed.y + ' 万元';
                                }
                            }
                        }
                    }
                }
            });
            
            // 骨盆粉碎性骨折费用对比图
            const pelvisCtx = document.getElementById('pelvisCostChart').getContext('2d');
            const pelvisPayout = Math.min(formData.medicalLimit, 20) + Math.min(formData.surgeryBenefit, 16);
            const pelvisSelfPay = 80 - 15 - pelvisPayout;
            
            pelvisChart = new Chart(pelvisCtx, {
                type: 'bar',
                data: {
                    labels: ['总治疗费用', '健保覆盖', '保单赔付', '客户自付'],
                    datasets: [{
                        label: '金额(万元)',
                        data: [80, 15, pelvisPayout, pelvisSelfPay],
                        backgroundColor: [
                            'rgba(52, 152, 219, 0.7)',
                            'rgba(46, 204, 113, 0.7)',
                            'rgba(155, 89, 182, 0.7)',
                            'rgba(231, 76, 60, 0.7)'
                        ],
                        borderColor: [
                            '#3498db',
                            '#2ecc71',
                            '#9b59b6',
                            '#e74c3c'
                        ],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            title: {
                                display: true,
                                text: '金额 (万元)'
                            }
                        }
                    },
                    plugins: {
                        legend: {
                            display: false
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return context.parsed.y + ' 万元';
                                }
                            }
                        }
                    }
                }
            });
            
            // 急性腦中風費用对比图
            const strokeCtx = document.getElementById('strokeCostChart').getContext('2d');
            const strokePayout = Math.min(formData.medicalLimit, 20) + Math.min(formData.criticalIllness * 0.3, 30);
            const strokeSelfPay = 120 - 20 - strokePayout;
            
            strokeChart = new Chart(strokeCtx, {
                type: 'bar',
                data: {
                    labels: ['总治疗费用', '健保覆盖', '保单赔付', '客户自付'],
                    datasets: [{
                        label: '金额(万元)',
                        data: [120, 20, strokePayout, strokeSelfPay],
                        backgroundColor: [
                            'rgba(52, 152, 219, 0.7)',
                            'rgba(46, 204, 113, 0.7)',
                            'rgba(155, 89, 182, 0.7)',
                            'rgba(231, 76, 60, 0.7)'
                        ],
                        borderColor: [
                            '#3498db',
                            '#2ecc71',
                            '#9b59b6',
                            '#e74c3c'
                        ],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            title: {
                                display: true,
                                text: '金额 (万元)'
                            }
                        }
                    },
                    plugins: {
                        legend: {
                            display: false
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return context.parsed.y + ' 万元';
                                }
                            }
                        }
                    }
                }
            });
            
            // 冠狀動脈繞道手術費用对比图
            const heartCtx = document.getElementById('heartCostChart').getContext('2d');
            const heartPayout = Math.min(formData.medicalLimit, 20) + Math.min(formData.surgeryBenefit, 16);
            const heartSelfPay = 90 - 12 - heartPayout;
            
            heartChart = new Chart(heartCtx, {
                type: 'bar',
                data: {
                    labels: ['总治疗费用', '健保覆盖', '保单赔付', '客户自付'],
                    datasets: [{
                        label: '金额(万元)',
                        data: [90, 12, heartPayout, heartSelfPay],
                        backgroundColor: [
                            'rgba(52, 152, 219, 0.7)',
                            'rgba(46, 204, 113, 0.7)',
                            'rgba(155, 89, 182, 0.7)',
                            'rgba(231, 76, 60, 0.7)'
                        ],
                        borderColor: [
                            '#3498db',
                            '#2ecc71',
                            '#9b59b6',
                            '#e74c3c'
                        ],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            title: {
                                display: true,
                                text: '金额 (万元)'
                            }
                        }
                    },
                    plugins: {
                        legend: {
                            display: false
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return context.parsed.y + ' 万元';
                                }
                            }
                        }
                    }
                }
            });
            
            // 未来医疗趋势图
            const futureCtx = document.getElementById('futureTrendChart').getContext('2d');
            futureChart = new Chart(futureCtx, {
                type: 'line',
                data: {
                    labels: ['2025', '2028', '2030', '2032', '2035'],
                    datasets: [{
                        label: '先进医疗平均费用',
                        data: [30, 45, 60, 80, 120],
                        borderColor: '#e74c3c',
                        backgroundColor: 'rgba(231, 76, 60, 0.1)',
                        fill: true,
                        tension: 0.4
                    },
                    {
                        label: '当前实支实付额度',
                        data: [formData.medicalLimit, formData.medicalLimit, formData.medicalLimit, formData.medicalLimit, formData.medicalLimit],
                        borderColor: '#3498db',
                        backgroundColor: 'rgba(52, 152, 219, 0.1)',
                        borderDash: [5, 5],
                        fill: true,
                        tension: 0
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            title: {
                                display: true,
                                text: '金额 (万元)'
                            }
                        }
                    },
                    plugins: {
                        legend: {
                            position: 'top',
                        }
                    }
                }
            });
        }
        
        // 標籤頁切換功能
        document.addEventListener('DOMContentLoaded', function() {
            const tabButtons = document.querySelectorAll('.tab-button');
            const tabContents = document.querySelectorAll('.tab-content');
            
            tabButtons.forEach(button => {
                button.addEventListener('click', function() {
                    const tabId = this.getAttribute('data-tab');
                    
                    // 移除所有按鈕和內容的active類
                    tabButtons.forEach(btn => btn.classList.remove('active'));
                    tabContents.forEach(content => content.classList.remove('active'));
                    
                    // 添加active類到當前按鈕和內容
                    this.classList.add('active');
                    document.getElementById(`${tabId}-tab`).classList.add('active');
                });
            });
            
            // 初始化時生成一次分析報告
            generateAnalysis();
        });
    </script>
</body>
</html>
