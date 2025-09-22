# 🛡️ Threat Intelligence Dashboard (Power BI)
A Power BI dashboard that combines real phishing and real malware datasets to visualize Indicators of Compromise (IOCs). It provides SOC analysts with quick insights into IOC counts and threat distribution.

## ✨ Features
- KPI Cards: Total IOCs, Phishing IOCs, Malware IOCs
- Bar Chart: IOC counts by source (Phishing vs Malware)
- Pie Chart: Distribution of Phishing vs Malware
- Built from real-world open feeds (PhishTank + URLhaus)

## 📂 Repository Structure
data/
  datasets.zip              # contains phishing_dataset.csv + malware_dataset.csv
dashboard/
  ThreatIntelDashboard.pbix # Power BI dashboard file
  screenshots/
    dashboard_overview.png  # main preview image
README.md

## 📊 Datasets
- Phishing IOCs → phishing_dataset.csv (from PhishTank, verified phishing URLs)
- Malware IOCs → malware_dataset.csv (from URLhaus, malware distribution feed)
👉 Both are packaged inside data/datasets.zip to avoid GitHub secret-scanning false positives.

## 🚀 How to Reproduce
1. Clone the Repository
git clone https://github.com/YourUsername/Threat-Intel-Dashboard.git
cd Threat-Intel-Dashboard

2. Unzip Datasets
Extract the contents of data/datasets.zip → phishing_dataset.csv + malware_dataset.csv

3. Open in Power BI
- If PBIX exists → open dashboard/ThreatIntelDashboard.pbix
- Else, build from scratch:
  - Get Data → Text/CSV
  - Load phishing_dataset.csv → name table csv_phishing
  - Load malware_dataset.csv → name table csv_malware

## ⚙️ Building the Dashboard
KPI Cards
- Phishing IOCs → Card → csv_phishing[url] (Count)
- Malware IOCs → Card → csv_malware[URL] (Count)
- Total IOCs (measure):
Total_IOCs = COUNTROWS(csv_phishing) + COUNTROWS(csv_malware)

Comparison Visuals
1. Create helper table (Home → Enter Data):
Source
Phishing IOCs
Malware IOCs
Name it IOC_Source_Table
2. Measures:
Phishing_IOCs = COUNTROWS(csv_phishing)
Malware_IOCs  = COUNTROWS(csv_malware)
IOC_Count =
SWITCH(
  SELECTEDVALUE(IOC_Source_Table[Source]),
  "Phishing IOCs", [Phishing_IOCs],
  "Malware IOCs", [Malware_IOCs]
)
3. Bar Chart → Axis = IOC_Source_Table[Source], Values = IOC_Count
4. Pie Chart → Legend = IOC_Source_Table[Source], Values = IOC_Count

Styling
- Cards → Format → Effects → Background ON (10–20% transparency)
- Titles → clear names (“Phishing IOCs”, “Malware IOCs”, “Total IOCs”)
- Colors → consistent scheme (Phishing = Red/Orange, Malware = Blue)

## 🖼️ Preview
![Dashboard Overview](dashboard/screenshots/Screenshot 2025-09-21 234928.png)

## 📈 Roadmap
- Add time-series IOC trends by First_Seen
- Add slicers (date ranges, targets)
- Publish to Power BI Service with auto-refresh
- Integrate live feeds (OpenPhish, AbuseIPDB, VirusTotal)

## 👤 Author
**Thristha Gurajala**  
🔗 https://www.linkedin.com/in/thristha20024
rsecurity portfolio.  
**Author:** [Thristha Gurajala](https://www.linkedin.com/in/thristha20024)
