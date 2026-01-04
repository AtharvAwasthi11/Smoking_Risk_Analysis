# 🫁 Smoking Health Risk Analysis Dashboard

## 📌 Project Overview
This repository features a cutting-edge **Healthcare Intelligence Dashboard** designed to visualize the physiological impact of smoking. By correlating smoking duration and daily intake with vital health markers like **BMI**, **Cholesterol**, and **Hypertension**, this tool identifies high-risk demographics and health trends across different age groups.

---

## 🚀 Key Clinical Insights
* **Demographic Benchmarking:** Real-time comparison of patient **Age (Avg 54.9)** and **BMI (Avg 29.8)** against overall population averages.
* **Intake Correlation:** A detailed time-series analysis showing the relationship between Years of Smoking (YOS) and Cigarettes Per Day (CPD).
* **Risk Stratification:** Visual tracking of Cholesterol and Hypertension risk levels (High, Low, Normal) across aging populations.
* **Organ-Specific Navigation:** Interactive sidebar allowing users to toggle focus between Heart, Kidney, Liver, and Lungs.

---

## 🧪 Technical Deep Dive: DAX & Logic
The dashboard utilizes advanced DAX (Data Analysis Expressions) to provide dynamic, context-aware reporting.

### 🔹 Variance Indicators (Dynamic KPIs)
These measures compare the filtered patient group against the global average, using `UNICHAR` for visual trend icons.

**VS Avg Age Formula:**
```dax
vs Avg Age = 
VAR _CurrentAge = AVERAGE(health_dataset[Age]) 
VAR _OverallAge = CALCULATE(AVERAGE(health_dataset[Age]), ALL(health_dataset)) 
VAR _Diff = _CurrentAge - _OverallAge
RETURN 
SWITCH( TRUE(), 
    _Diff > 0, UNICHAR(9650) & " " & FORMAT(_CurrentAge, "0.0"), 
    _Diff < 0, UNICHAR(9660) & " " & FORMAT(_CurrentAge, "0.0"), 
    FORMAT(_CurrentAge, "0.0") 
)



**VS Avg BMI Formula:**
vs Avg BMI = 
VAR _CurrentBMI = AVERAGE(health_dataset[BMI]) 
VAR _OverallBMI = CALCULATE(AVERAGE(health_dataset[BMI]), ALL(health_dataset)) 
VAR _Diff = _CurrentBMI - _OverallBMI
RETURN 
SWITCH( TRUE(), 
    _Diff > 0, UNICHAR(9650) & " " & FORMAT(_CurrentBMI, "0.0"), 
    _Diff < 0, UNICHAR(9660) & " " & FORMAT(_CurrentBMI, "0.0"), 
    FORMAT(_CurrentBMI, "0.0") 
)
----

**🔹 Demographic Binning**
Age Group = SWITCH( TRUE(), 
    health_dataset[Age] <= 28, "18–28", 
    health_dataset[Age] <= 38, "29–38", 
    health_dataset[Age] <= 48, "39–48", 
    health_dataset[Age] <= 58, "49–58", 
    health_dataset[Age] <= 68, "59–68", 
    "69+" 
)
----
🎨 Design Palette & UI/UX
The dashboard follows a sophisticated "Medical-Clean" aesthetic:

Primary Background: #D4DDE3 (Soft Steel Blue)

Active State/Selection: #C3CFD8

Organ Highlight Color: #E2EAFA

Heading Typography: #666666

Data Visual Colors: * Donut Chart: Never (#98ABB3), Current (#A9BBC7), Former (#C3CFD8)

Hypertension Risk: High (#808080), Low (#98ABB3), Normal (#C3CFD8)****
