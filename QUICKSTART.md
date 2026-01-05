# 🚀 Quick Start Guide - AI Diet Generator

Get your personalized diet plan in **5 minutes**!

---

## 📋 Prerequisites Checklist

Before starting, ensure you have:

- [ ] **Docker Desktop** installed ([Download](https://docs.docker.com/get-docker/))
- [ ] **8GB RAM** minimum (16GB recommended)
- [ ] **5GB disk space** free
- [ ] **Internet connection** (for first setup)

---

## ⚡ Installation (3 Steps)

### Step 1: Install Ollama

**Windows:**
```bash
# Download from: https://ollama.ai/download/windows
# Run: ollama-setup.exe
```

**macOS:**
```bash
brew install ollama
```

**Linux:**
```bash
curl -fsSL https://ollama.ai/install.sh | sh
```

**Verify installation:**
```bash
ollama --version
# Should output: ollama version 0.x.x
```

---

### Step 2: Download Mistral 7B Model

```bash
# This will download ~4GB (takes 5-10 minutes)
ollama pull mistral:7b

# Verify model is installed
ollama list
# Should show: mistral:7b
```

---

### Step 3: Start Ollama Server

**Windows/macOS:**
```bash
# Open new terminal and run:
ollama serve
```

**Linux:**
```bash
# Ollama starts automatically as service
# Check status:
systemctl status ollama
```

**Keep this terminal open!** Ollama must be running.

---

## 🐳 Run AI Diet Generator

### Option A: Docker Compose (Recommended)

```bash
# 1. Download docker-compose.yml
curl -O https://raw.githubusercontent.com/yourusername/ai-diet-generator-public/main/docker-compose.yml

# 2. Start application
docker-compose up -d

# 3. Check status
docker-compose ps

# Should show:
# NAME                  STATUS    PORTS
# ai-diet-generator     Up        0.0.0.0:5000->5000/tcp
```

### Option B: Docker Run

```bash
docker run -d \
  --name ai-diet-generator \
  -p 5000:5000 \
  --add-host host.docker.internal:host-gateway \
  -e OLLAMA_HOST=http://host.docker.internal:11434 \
  chriwork/ai-diet-generator:latest
```

---

## 🌐 Access Application

1. **Open browser**
2. **Navigate to:** `http://localhost:5000`
3. **You should see:** AI Diet Generator interface

✅ **Success!** The application is running.

---

## 📝 Generate Your First Diet Plan

### 1. Fill in Your Data

```yaml
Personal Info:
  Weight: 68 kg          # Your current weight
  Height: 173 cm         # Your height
  Age: 25 years          # Your age
  Gender: Male/Female    # Select your gender

Activity Level:
  Sedentary:    Office work, minimal movement
  Light:        Standing jobs, light walking
  Moderate:     Physical labor, active job

Workout Frequency:
  0:            No workouts
  1-2:          1-2 workouts per week
  3-4:          3-4 workouts per week
  5+:           5 or more workouts per week

Nutritional Goal:
  Mass Gain:       Build muscle (+10% calories)
  Maintenance:     Maintain current weight
  Weight Loss:     Lose fat (-15% calories)

Days:
  1-14:         Number of days to generate
```

### 2. Click "Genera Piano"

⏳ **Wait 10-30 seconds** (depends on number of days)

### 3. View Results

You'll see:
- ✅ **Target calories** vs actual calories
- ✅ **Daily meal plans** with portions
- ✅ **Nutritional breakdown** per meal
- ✅ **Quality rating** (0-10)

### 4. Download PDFs

Click buttons to download:
- 📄 **Diet PDF**: Full meal plan with portions
- 🛒 **Shopping List PDF**: Aggregated grocery list

---

## 💡 Example Scenarios

### Scenario 1: Build Muscle (Man, 25y, 68kg, 173cm)

```yaml
Weight: 68 kg
Height: 173 cm
Age: 25
Gender: Male
Activity: Sedentary
Workouts: 3-4 per week
Goal: Mass Gain
Days: 7

Expected Result:
Target: ~2500 kcal/day
Protein: ~150g/day
Rating: 8.5-9.5/10
```

### Scenario 2: Lose Weight (Woman, 30y, 65kg, 165cm)

```yaml
Weight: 65 kg
Height: 165 cm
Age: 30
Gender: Female
Activity: Light
Workouts: 1-2 per week
Goal: Weight Loss
Days: 14

Expected Result:
Target: ~1500 kcal/day
High vegetables: ~850g/day
Rating: 9.0-9.7/10
```

### Scenario 3: Maintenance (Woman, 25y, 55kg, 165cm)

```yaml
Weight: 55 kg
Height: 165 cm
Age: 25
Gender: Female
Activity: Sedentary
Workouts: 3-4 per week
Goal: Maintenance
Days: 7

Expected Result:
Target: ~1800 kcal/day
Balanced macros
Rating: 9.0/10
```

---

## 🎯 Tips for Best Results

### ✅ Do's

1. **Accurate data**: Enter exact weight and height
2. **Honest activity**: Don't overestimate activity level
3. **Realistic goals**: Start with 7 days to test
4. **Check Ollama**: Ensure `ollama serve` is running
5. **Wait patiently**: Generation takes 10-30 seconds

### ❌ Don'ts

1. **Don't refresh** during generation (wait for results)
2. **Don't use extreme values** (weight 30kg or 300kg)
3. **Don't close Ollama** while using the app
4. **Don't expect instant results** (AI needs time)

---

## 🔄 Stopping the Application

### Docker Compose

```bash
# Stop application
docker-compose down

# Stop and remove data
docker-compose down -v
```

### Docker Run

```bash
# Stop container
docker stop ai-diet-generator

# Remove container
docker rm ai-diet-generator
```

### Stop Ollama

```bash
# Windows/macOS: Close terminal running "ollama serve"
# Linux:
sudo systemctl stop ollama
```

---

## 📊 Understanding the Rating

The system rates your diet on 4 dimensions:

| Metric | What it measures | Good score |
|--------|------------------|------------|
| 🔥 **Calories** | Accuracy vs target | 9.0+ |
| 🥗 **Variety** | Food diversity | 9.0+ |
| 🍗 **Proteins** | Protein frequency & variety | 8.5+ |
| 🌱 **Vegetables** | Vegetable volume & types | 8.0+ |


---

## 🎓 Next Steps

After your first successful generation:

1. **Try different goals**: Test all 3 (Mass/Maintenance/Weight Loss)
2. **Extend duration**: Generate 14-day plans
3. **Download PDFs**: Use them for meal prep
4. **Adjust parameters**: Fine-tune for best results
5. **Check FAQ**: See [FAQ.md](FAQ.md) for more tips

---

## 🆘 Having Issues?

If something doesn't work:

1. **Check [TROUBLESHOOTING.md](TROUBLESHOOTING.md)** - Common solutions
2. **Verify Ollama** is running: `ollama list`
3. **Check Docker** logs: `docker-compose logs -f`
4. **Read [FAQ.md](FAQ.md)** - Frequently asked questions



---

## ⏱️ Time Estimates

| Task | Time |
|------|------|
| Install Docker | 5 min |
| Install Ollama | 2 min |
| Download Mistral 7B | 5-10 min |
| Start application | 1 min |
| Generate 7-day diet | 15-30 sec |
| Generate 14-day diet | 30-60 sec |

**Total setup time:** ~15-20 minutes (first time only)

---

## ✅ Success Indicators

You'll know everything works when:

- ✅ Browser shows "✅ Ollama attivo - Mistral disponibile"
- ✅ Diet generates in 10-30 seconds
- ✅ Results show target vs actual calories
- ✅ Rating is 8.0+ / 10
- ✅ PDFs download successfully

---

**🎉 Congratulations!** You're ready to use AI Diet Generator!

For advanced topics, see:
- [TROUBLESHOOTING.md](TROUBLESHOOTING.md) - Problem solving
- [FAQ.md](FAQ.md) - Common questions

---

**Last updated:** January 5, 2026