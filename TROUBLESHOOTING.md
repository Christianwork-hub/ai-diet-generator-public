# 🔧 Troubleshooting Guide - AI Diet Generator

Common issues and solutions.

---

## 🚨 Quick Diagnostics

Run these checks first:

```bash
# 1. Check Docker is running
docker --version
docker ps

# 2. Check Ollama is running
ollama list

# 3. Check application is running
curl http://localhost:5000

# 4. Check logs
docker-compose logs -f
```

---

## ⚠️ Common Issues

### Issue #1: "Ollama non in esecuzione" Error

**Symptoms:**
- Red banner: "❌ Ollama non in esecuzione"
- Diet generation fails immediately

**Causes:**
- Ollama server not started
- Ollama on wrong port
- Docker can't reach host

**Solutions:**

#### Solution A: Start Ollama Server
```bash
# Open NEW terminal
ollama serve

# Keep this terminal open!
```

#### Solution B: Check Ollama is Running
```bash
# Should return list of models
ollama list

# Should show mistral:7b
```

#### Solution C: Verify Connection
```bash
# Should return JSON
curl http://localhost:11434/api/tags

# If this fails, Ollama is not accessible
```

#### Solution D: Docker on Windows/Mac
```bash
# Edit docker-compose.yml
# Change:
extra_hosts:
  - "host.docker.internal:host-gateway"

# To (if above doesn't work):
network_mode: "host"
environment:
  - OLLAMA_HOST=http://localhost:11434
```

#### Solution E: Docker on Linux
```bash
# Get host IP
ip addr show docker0 | grep inet

# Use that IP in docker-compose.yml:
environment:
  - OLLAMA_HOST=http://172.17.0.1:11434
```

---

### Issue #2: "Mistral non trovato" Warning

**Symptoms:**
- Yellow banner: "⚠️ Ollama attivo ma Mistral non trovato"
- Diet generation fails with timeout

**Causes:**
- Mistral 7B model not downloaded
- Wrong model name

**Solutions:**

```bash
# Download Mistral 7B (takes 5-10 min)
ollama pull mistral:7b

# Verify installation
ollama list

# Should show:
# NAME            ID              SIZE
# mistral:7b      xxx             4.1 GB
```

**Alternative models (if mistral fails):**
```bash
# Try smaller model (faster)
ollama pull mistral:7b-instruct

# Or larger model (better quality, slower)
ollama pull mixtral:8x7b
```

---

### Issue #3: Port 5000 Already in Use

**Symptoms:**
```
Error: bind: address already in use
```

**Solutions:**

#### Solution A: Stop Conflicting Service
```bash
# Find what's using port 5000
# Windows:
netstat -ano | findstr :5000

# Mac/Linux:
lsof -i :5000

# Kill the process (replace PID)
kill -9 <PID>
```

#### Solution B: Use Different Port
```yaml
# Edit docker-compose.yml
ports:
  - "5001:5000"  # Change host port to 5001

# Then access: http://localhost:5001
```

---

### Issue #4: Docker Container Won't Start

**Symptoms:**
```bash
docker-compose up -d
# Container exits immediately
```

**Solutions:**

```bash
# Check logs for errors
docker-compose logs

# Common issues:

# 1. Image not found
docker pull chriwork/ai-diet-generator:latest

# 2. Permission denied (Linux)
sudo usermod -aG docker $USER
newgrp docker

# 3. Out of memory
# Close other applications or increase Docker memory:
# Docker Desktop → Settings → Resources → Memory → 8GB+
```

---

### Issue #5: Slow Generation (>2 minutes)

**Symptoms:**
- Diet generation takes 2+ minutes
- Browser shows loading spinner forever

**Causes:**
- Insufficient RAM
- CPU throttling
- Too many days requested

**Solutions:**

#### Solution A: Reduce Days
```yaml
# Instead of 14 days, try:
Days: 7  # Faster generation
```

#### Solution B: Increase Docker Resources
```
Docker Desktop → Settings → Resources:
  Memory: 8GB → 12GB
  CPUs: 2 → 4
```

#### Solution C: Check System Resources
```bash
# Check memory usage
docker stats

# If memory >90%, close other apps
```

#### Solution D: Restart Everything
```bash
# Stop application
docker-compose down

# Restart Ollama
# Close terminal running "ollama serve"
# Open new terminal: ollama serve

# Start application
docker-compose up -d
```

---

### Issue #6: "Failed to Fetch" Error in Browser

**Symptoms:**
- Red error banner in web interface
- "Impossibile connettersi al server"

**Causes:**
- Flask app crashed
- Docker container not running
- Network issues

**Solutions:**

```bash
# Check container is running
docker ps

# Should show ai-diet-generator with status "Up"

# If not running:
docker-compose up -d

# Check logs for errors
docker-compose logs -f

# Look for:
# - Python errors
# - Missing dependencies
# - Port conflicts
```

---

### Issue #7: PDF Download Fails

**Symptoms:**
- "Download Dieta PDF" button doesn't work
- Error message: "Dieta non trovata"

**Causes:**
- Session expired
- Diet not generated yet
- Browser blocking download

**Solutions:**

#### Solution A: Regenerate Diet
```
1. Click "Genera Piano" again
2. Wait for results
3. Then click "Scarica Dieta PDF"
```

#### Solution B: Check Browser Console
```
1. Press F12
2. Check Console tab for errors
3. Look for CORS or network errors
```

#### Solution C: Allow Pop-ups
```
Browser Settings:
  - Allow pop-ups from localhost:5000
  - Allow automatic downloads
```

---

### Issue #8: Empty or Weird Results

**Symptoms:**
- Very low calories (<500 kcal)
- Missing meals
- Strange food combinations

**Causes:**
- Invalid input parameters
- Mistral model hallucinates
- Calculation error

**Solutions:**

#### Solution A: Validate Inputs
```yaml
Check your inputs:
  Weight: 40-150 kg (not 400 or 4)
  Height: 140-220 cm (not 1400 or 14)
  Age: 15-100 years (not 150)
  Days: 1-14 (not 100)
```

#### Solution B: Restart Generation
```
Sometimes AI generates edge cases.
Click "Genera Piano" again for new results.
```

#### Solution C: Check Ollama Model
```bash
# Verify Mistral is healthy
ollama run mistral:7b "Test response"

# Should get coherent response
# If gibberish, re-pull model:
ollama pull mistral:7b
```

---

### Issue #9: High Caloric Deviation (>10%)

**Symptoms:**
- Target: 2000 kcal
- Actual: 1700 kcal (-15%)
- Rating: <8.0

**Causes:**
- Conservative booster system
- Extreme parameters

**Solutions:**

#### Solution A: Acceptable Range
```
System targets <8% deviation.
Results of 8-10% are still usable.

If deviation >10%, regenerate:
Click "Genera Piano" again.
```

#### Solution B: Adjust Parameters
```yaml
Try slightly different inputs:
  Activity: Sedentary → Light
  Workouts: 3-4 → 5+
  
This increases target calories.
```

---

### Issue #10: Docker on Windows WSL Issues

**Symptoms:**
- Docker commands fail
- `host.docker.internal` not resolving

**Solutions:**

```bash
# Ensure WSL2 is used (not WSL1)
wsl -l -v

# Should show VERSION 2

# If not, convert:
wsl --set-version <distro> 2

# Restart Docker Desktop
# Settings → General → Use WSL2 based engine ✓
```

---

## 🐧 Platform-Specific Issues

### Windows

**Issue: Docker Desktop won't start**
```
1. Enable Hyper-V:
   Control Panel → Programs → Turn Windows features on/off
   ✓ Hyper-V
   ✓ Windows Subsystem for Linux

2. Update Windows to latest version

3. Restart computer
```

**Issue: Slow Docker performance**
```
1. Increase WSL2 memory:
   Create: %USERPROFILE%\.wslconfig

[wsl2]
memory=8GB
processors=4

2. Restart WSL: wsl --shutdown
```

### macOS

**Issue: Docker permission denied**
```bash
# Fix permissions
sudo chown -R $USER ~/Library/Containers/com.docker.docker

# Restart Docker Desktop
```

**Issue: M1/M2 ARM compatibility**
```bash
# Pull ARM-compatible image
docker pull --platform linux/arm64 chriwork/ai-diet-generator:latest

# Or build locally (if issues)
docker build --platform linux/arm64 .
```

### Linux

**Issue: Docker permission denied**
```bash
# Add user to docker group
sudo usermod -aG docker $USER

# Logout and login, or:
newgrp docker

# Verify
docker ps
```

**Issue: Ollama connection on Linux**
```bash
# Get Docker bridge IP
ip addr show docker0 | grep inet
# Example: 172.17.0.1

# Update docker-compose.yml:
environment:
  - OLLAMA_HOST=http://172.17.0.1:11434
```

---

## 🔍 Advanced Diagnostics

### Check Container Health

```bash
# Container status
docker inspect ai-diet-generator | grep Health

# Should show: "Status": "healthy"
```

### Test Ollama Connectivity from Container

```bash
# Enter container
docker exec -it ai-diet-generator sh

# Test Ollama
curl http://host.docker.internal:11434/api/tags

# Should return JSON with models
exit
```

### Monitor Resource Usage

```bash
# Real-time stats
docker stats ai-diet-generator

# Look for:
# - Memory: Should be <2GB
# - CPU: Spikes during generation (normal)
```

---

## 📝 Collecting Debug Info

If you need to report an issue:

```bash
# Collect all relevant info

# 1. System info
docker --version
ollama --version
uname -a  # Linux/Mac
systeminfo  # Windows

# 2. Container logs
docker-compose logs > debug-logs.txt

# 3. Ollama logs
ollama list > ollama-models.txt

# 4. Docker inspect
docker inspect ai-diet-generator > container-info.txt

# 5. Network test
curl -v http://localhost:5000 > network-test.txt
curl -v http://localhost:11434/api/tags > ollama-test.txt
```

**Then attach these files to your GitHub issue.**

---

## 🆘 Still Having Issues?

### Before Opening an Issue

1. ✅ Read this entire guide
2. ✅ Check [FAQ.md](FAQ.md)
3. ✅ Search [existing issues](https://github.com/yourusername/ai-diet-generator-public/issues)
4. ✅ Collect debug info (see above)

### Opening an Issue

Use the [Bug Report template](https://github.com/yourusername/ai-diet-generator-public/issues/new?template=bug_report.md)

Include:
- Detailed description
- Steps to reproduce
- Expected vs actual behavior
- System info
- Debug logs

---

## 💡 Quick Fixes Summary

| Problem | Quick Fix |
|---------|-----------|
| Ollama not found | `ollama serve` in new terminal |
| Mistral missing | `ollama pull mistral:7b` |
| Port conflict | Change to 5001 in docker-compose.yml |
| Container won't start | `docker-compose down && docker-compose up -d` |
| Slow generation | Reduce days to 7, increase Docker RAM |
| PDF download fails | Regenerate diet, check browser console |
| High deviation | Regenerate or adjust parameters |

---

**Most issues are solved by restarting Ollama or Docker!** 🔄

---

**Need more help?**
- [FAQ.md](FAQ.md) - Common questions
- [Contact](mailto:christiangri@live.it)

**Last updated:** January 4, 2026