# 🍽️ AI Diet Generator - Smart Meal Planning System

> ⚠️ IMPORTANT  
> This application requires a **local LLM (Ollama + Mistral 7B)**.  
> It is intended for **developers and technical users**.  
> A minimum of **8 GB RAM (16 GB recommended)** is required.


AI-powered meal planning system that generates personalized diet plans using caloric density scoring algorithms and LLM integration (Mistral 7B). Achieves **-4.4% average caloric deviation** with **77% food variety** over 14 days.

---

## 🌟 Key Features

### ✅ Core Functionality
- **3 Nutritional Goals**: Mass Gain, Maintenance, Weight Loss
- **Guaranteed Precision**: <8% caloric deviation (avg: **-4.4%**)
- **High Variety**: 77% unique foods over 14 days
- **Smart Selection**: Dynamic scoring based on caloric density
- **Auto-Compensation**: Intelligent booster system
- **Full Customization**: Age, weight, height, activity, workouts

### 🤖 AI-Powered Intelligence
- **Caloric Density Scoring**: Prioritizes optimal foods per goal
- **Mistral 7B Integration**: Via Ollama (100% local, zero cloud)
- **Variety Tracking**: Progressive penalties for food reuse
- **Adaptive Algorithms**: Goal-specific strategies

### 📊 Validated Performance (84 days tested)

| Scenario | Target | Actual | Deviation | Rating |
|----------|--------|--------|-----------|--------|
| Uomo Mantenimento | 2297 | 2220 | **-3.4%** | 9.0/10 |
| Uomo Dimagrimento | 1953 | 1819 | **-6.8%** | 8.8/10 |
| Uomo Massa | 2527 | 2372 | **-6.1%** | 9.0/10 |
| Donna Mantenimento | 1813 | 1791 | **-1.2%** | 9.0/10 |
| Donna Dimagrimento | 1541 | 1528 | **-0.9%** | 9.7/10 |
| Donna Massa | 1994 | 1877 | **-5.9%** | 8.9/10 |
| **MEDIA** | - | - | **-4.4%** | **9.0/10** |

---

## 🚀 Quick Start (Docker)

### Prerequisites

```bash
# Required
Docker Desktop (https://docs.docker.com/get-docker/)
Ollama (https://ollama.ai/)

# System Requirements
- RAM: 8GB minimum (16GB recommended)
- Disk: 5GB free space
- OS: Windows 10+, macOS 10.14+, Linux
```

### Installation (3 Steps)

```bash
# Step 1: Install Ollama
# Download from: https://ollama.ai/
# Windows: ollama-setup.exe
# Mac: brew install ollama
# Linux: curl -fsSL https://ollama.ai/install.sh | sh

# Step 2: Pull Mistral 7B model
ollama pull mistral:7b

# Step 3: Start Ollama server
ollama serve
```

### Run Application (1 Command)

```bash
# Start AI Diet Generator
docker-compose up -d

# Access application
# Open browser: http://localhost:5000
```

### Usage

1. **Open browser:** `http://localhost:5000`
2. **Fill parameters:**
   - Weight: 68 kg
   - Height: 173 cm
   - Age: 25 years
   - Activity: Sedentary / Light / Moderate
   - Workouts: 0-6 per week
   - Goal: Mass / Maintenance / Weight Loss
   - Days: 1-14
3. **Click "Genera Piano"**
4. **Download PDF** (diet + shopping list)

---

## 📊 How It Works

### 1. Caloric Density Scoring

```python
score = density_score + goal_bonus + variety_penalty

# Example: Salmon (208 kcal/100g) vs Cod (71 kcal/100g)

# MASS GAIN → High-density foods
salmon_score = 85 + 10 - 0 = 95 : Selected
cod_score = 30 + 10 - 0 = 40

# WEIGHT LOSS → Low-density foods
salmon_score = 20 + 10 - 0 = 30
cod_score = 80 + 10 - 0 = 90 : Selected
```

### 2. Adaptive Strategies

| Goal | Caloric Target | Food Selection | Volume |
|------|----------------|----------------|--------|
| **Mass** | +10% TDEE | High-density (salmon, nuts) | Moderate (775g veg) |
| **Maintenance** | TDEE | Balanced variety | Medium (800g veg) |
| **Weight Loss** | -15% TDEE | Low-density (white fish) | High (850g veg) |

### 3. Intelligent Features

- **Legume Integration:** 64-71% days for mass, 21-43% for other goals
- **Smart Bread System:** Contextual pairing (never with solo fruit)
- **Booster System:** Automatic gap compensation
- **Variety Tracker:** 77% unique foods (60-79 different items/14 days)

---

## 📈 Performance Metrics

### Precision

```
Deviazione media: -4.4%
Target sistema: <8%
Performance: 45% migliore del target 
```


---

## 🎯 System Architecture

```
User Input → TDEE Calculator → Density Scoring →
Food Selection → Portion Calculation → Booster System →
Validation → JSON Output → PDF Export
```

**Key Components:**
- **150+ foods database** with nutritional data
- **Mistral 7B** for intelligent suggestions
- **ReportLab** for PDF generation
- **Flask + Tailwind CSS** for web interface

---

## 🐳 Docker Commands

```bash
# Start application
docker-compose up -d

# Stop application
docker-compose down

# View logs
docker-compose logs -f

# Update to latest version
docker-compose pull
docker-compose up -d

# Restart application
docker-compose restart
```

---

## 🖼️ Screenshots

### Home Interface
![UI Home](https://via.placeholder.com/800x400?text=AI+Diet+Generator+Home)

### Generated Diet Plan
![Results](https://via.placeholder.com/800x400?text=Generated+Diet+Plan+Example)

---

## ❓ Troubleshooting

### Ollama not detected

```bash
# Check Ollama is running
ollama list

# Start Ollama server
ollama serve

# Verify connection
curl http://localhost:11434/api/tags
```

### Port 5000 already in use

```yaml
# Edit docker-compose.yml
ports:
  - "5001:5000"  # Change host port
```

### Docker permission denied (Linux)

```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

## 📋 System Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| **RAM** | 8GB | 16GB |
| **CPU** | Dual-core 2.0GHz | Quad-core 2.5GHz+ |
| **Disk** | 5GB free | 10GB free |
| **Docker** | 20.10+ | Latest |
| **Ollama** | Latest | Latest |

---

## 🔒 License

This software is **proprietary and confidential**. 

### Permitted Use:
✅ Personal, non-commercial testing via Docker  
✅ Web interface access at localhost:5000

### Restrictions:
❌ No source code access  
❌ No redistribution or modification  
❌ No commercial use without license

See [LICENSE](LICENSE) for full terms.

---

## 💼 Commercial Licensing

For commercial use, enterprise licensing, or custom development:

📧 **Email:** christiangri@live.it
💼 **LinkedIn:** [(https://www.linkedin.com/in/christian-grieco-340bba194/)]

---

## 🤝 Support

- 📧 **Email:** christiangri@live.it
- 💬 **LinkedIn:** [(https://www.linkedin.com/in/christian-grieco-340bba194/)]

---

## 🙏 Acknowledgments

- [Ollama](https://ollama.ai/) - Local LLM infrastructure
- [Mistral AI](https://mistral.ai/) - Mistral 7B model
- [Flask](https://flask.palletsprojects.com/) - Web framework
- [Tailwind CSS](https://tailwindcss.com/) - UI styling
- Nutritional data: USDA FoodData Central, CREA

---

## 📊 Technical Highlights

```
╔════════════════════════════════════════════════════╗
║  🏆 AI DIET GENERATOR       ║
╠════════════════════════════════════════════════════╣
║                                                    ║
║  📊 7 scenarios × 14 days = 84 days tested         ║
║  🎯 100% success rate (7/7 PASS)                   ║
║  📉 -4.4% deviation (target <8%)                   ║
║  🥗 77% food variety (target >75%)                 ║
║  ⭐ 9.0/10 average rating                          ║
║                                                    ║
╚════════════════════════════════════════════════════╝
```

---

<div align="center">

### ⭐ If this project impressed you, star the repo!


**© 2026 Christian Grieco. All Rights Reserved.**

</div>