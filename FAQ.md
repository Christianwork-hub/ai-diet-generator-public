# ❓ FAQ - Frequently Asked Questions

Common questions about AI Diet Generator.

---

## 📊 General Questions

### Q: What is AI Diet Generator?

**A:** An AI-powered meal planning system that generates personalized diet plans using:
- Caloric density scoring algorithms
- Mistral 7B LLM (local, no cloud)
- 150+ food database
- Validated on 84 days of testing

**Key features:**
- 3 goals: Mass, Maintenance, Weight Loss
- -4.4% average caloric deviation
- 77% food variety
- PDF export (diet + shopping list)

---

### Q: Is it free?

**A:** Yes, the Docker version is **free for personal, non-commercial use**.

Commercial licensing available for:
- Businesses (gyms, nutrition centers)
- Apps/websites integrating the system
- White-label solutions

[Contact for pricing](mailto:christiangri@live.it)

---

### Q: Is my data private?

**A:** **100% private!**

- ✅ All processing happens **locally** on your computer
- ✅ Zero cloud connections
- ✅ No data stored on external servers
- ✅ Mistral 7B runs via Ollama (local LLM)
- ✅ No tracking, analytics, or telemetry

Your weight, health data, and diet plans **never leave your machine**.

---

### Q: What's the accuracy?

**A:** Very high! Validated on 84 days across 7 scenarios:

| Metric | Target | Result |
|--------|--------|--------|
| Caloric deviation | <8% | **-4.4%** ✅ |
| Food variety | >75% | **77%** ✅ |
| Quality rating | >8.0 | **9.0/10** ✅ |



---

### Q: How does it compare to MyFitnessPal or Lifesum?

**A:** Different approach:

| Feature | AI Diet Generator | MyFitnessPal | Lifesum |
|---------|-------------------|--------------|---------|
| **Caloric precision** | -4.4% | ~10% | ~8% |
| **Food variety** | 77% | 60% | 65% |
| **AI-powered** | Local LLM | No AI | Cloud AI |
| **Privacy** | 100% local | Cloud | Cloud |
| **Customization** | High | Medium | Medium |
| **Cost** | Free (personal) | Freemium | Paid |

**We focus on:** Precision + Variety + Privacy

**They focus on:** Tracking + Social + Cloud features

---

## 🔧 Technical Questions

### Q: What are the system requirements?

**Minimum:**
- 8GB RAM
- Dual-core CPU 2.0GHz
- 5GB disk space
- Docker Desktop
- Windows 10+, macOS 10.14+, or Linux

**Recommended:**
- 16GB RAM
- Quad-core CPU 2.5GHz+
- 10GB disk space
- Docker Desktop latest
- Fast SSD

---

### Q: Why do I need Ollama?

**A:** Ollama runs Mistral 7B locally for:
- Intelligent food suggestions
- Creative meal combinations
- Context-aware selections
- 100% privacy (no cloud)

**Without Ollama:**
- System still works
- Uses deterministic algorithms only
- Slightly less variety

---

### Q: Can I use it without Docker?

**A:** Not easily. The public version is **Docker-only** to:
- Simplify installation
- Ensure consistent environment
- Protect proprietary code
- Provide easy updates

**For source code access:** Commercial license required.

---

### Q: Which LLM model should I use?

**A:** **Recommended: Mistral 7B** (default)

```bash
ollama pull mistral:7b
```

**Alternatives:**

| Model | Size | RAM | Speed | Quality |
|-------|------|-----|-------|---------|
| mistral:7b | 4.1GB | 8GB | Fast | Excellent  |
| mixtral:8x7b | 26GB | 48GB | Slow | Best |
| llama3.1:8b | 4.7GB | 10GB | Fast | Very Good |
| phi3:14b | 7.9GB | 16GB | Medium | Excellent |

**For most users: Stick with Mistral 7B!**

---

### Q: How long does generation take?

**A:** Depends on days requested:

| Days | Time (Mistral 7B) |
|------|-------------------|
| 1 day | 5-10 seconds |
| 7 days | 15-30 seconds |
| 14 days | 30-60 seconds |

**Factors affecting speed:**
- CPU speed
- RAM available
- LLM model size
- Docker resources

---

### Q: Can I run it on Raspberry Pi?

**A:** **Not recommended.**

- Mistral 7B requires 8GB+ RAM
- Raspberry Pi 4 has max 8GB (not enough for OS + Docker + Ollama + Mistral)
- Generation would be very slow (5-10 minutes)

**Minimum hardware:** x86_64 desktop/laptop with 8GB RAM

---

## 🍽️ Usage Questions

### Q: How accurate are the calories?

**A:** Very accurate! Based on:
- USDA FoodData Central
- CREA (Italian nutrition database)
- Manual verification of 150+ foods

**Validation:**
- 7 scenarios × 14 days = 84 days tested
- Average deviation: **-4.4%**
- Range: -0.9% to -6.8%

**Note:** Results may vary ±5-10% based on:
- Food preparation method
- Portion measurement accuracy
- Individual metabolic differences

---

### Q: Can I customize the food database?

**A:** Not in the free Docker version.

**Commercial license includes:**
- Custom food database
- Allergen filters
- Dietary restrictions (vegan, keto, etc.)
- Regional cuisine preferences
- Source code access

[Contact for details](mailto:christiangri@live.it)

---

### Q: Why so many vegetables?

**A:** By design! Especially for weight loss.

**Vegetables provide:**
- High volume (satiety)
- Low calories
- Essential nutrients
- Fiber for digestion

**Typical amounts:**
- Weight loss: 850g/day
- Maintenance: 800g/day
- Mass gain: 775g/day

**Too much?** Select "Maintenance" goal for less volume.

---

### Q: Can I meal prep with these plans?

**A:** **Absolutely!** That's one of the main use cases.

**Tips:**
1. Generate 7-14 day plan
2. Download **Shopping List PDF**
3. Buy groceries once
4. Meal prep Sunday for the week
5. Follow portions as specified

**Portability:**
- Most meals work cold/reheated
- Protein + vegetables = meal prep friendly
- Fruits travel well for snacks

---

### Q: What if I don't like a food?

**A:** **Regenerate!**

Click "Genera Piano" again for a completely different plan.

**Why this works:**
- 150+ foods in database
- 77% variety guaranteed
- Random selection from top 30% scored foods
- Each generation is unique

**Probability of same food:**
- Same day: ~23% (variety penalty)
- Next generation: ~5%

---

### Q: Can I adjust portions?

**A:** In the Docker version: No automatic adjustment.

**What you can do:**
1. Download PDF
2. Manually adjust portions in PDF
3. Track actual intake

**Commercial version includes:**
- Interactive portion adjustment
- Real-time calorie recalculation
- Ingredient substitutions

---

### Q: How does it handle allergies?

**A:** Current version: **No allergen filter**.

**Workaround:**
- Generate multiple plans
- Manually exclude allergenic foods from PDF

**Coming in v1.1:**
- Allergen exclusion filters
- Dietary restrictions (vegan, vegetarian, etc.)

[Vote for this feature](https://github.com/yourusername/ai-diet-generator-public/discussions)

---

## 📈 Diet & Nutrition Questions

### Q: Will this help me lose weight?

**A:** Yes, if used correctly!

**How it works:**
1. System calculates TDEE (maintenance calories)
2. Weight Loss goal = TDEE - 15%
3. Creates balanced deficit diet
4. High protein + high volume = satiety

**Average results** (based on 1500 kcal deficit):
- Week 1: -0.5 to -1kg (water weight)
- Weeks 2-4: -0.5kg/week (fat loss)
- Months 2-3: -2kg/month (sustainable)

**Important:**
- Follow portions accurately
- Combine with exercise
- Track weight weekly
- Adjust if plateau

**Not a magic solution!** Requires consistency and effort.

---

### Q: Can I build muscle with this?

**A:** Yes! Mass Gain goal optimized for muscle building.

**What it does:**
- +10% calories above TDEE
- High protein frequency (80% meals)
- Legumes in 71% days (additional protein)
- Balanced macros for recovery

**For best results:**
- Progressive resistance training 3-4×/week
- 0.5-1g protein per lb body weight
- Adequate sleep (7-9h)
- Consistency over 3-6 months

**Expected gains:**
- Beginners: 0.5-1kg muscle/month
- Intermediate: 0.25-0.5kg/month
- Advanced: 0.1-0.25kg/month

---

### Q: Is 14 days enough?

**A:** Depends on your goal:

**14 days is great for:**
- Testing the system
- Variety evaluation
- Meal prep planning
- Short-term events

**For long-term:**
- Generate new plan every 2 weeks
- Rotate between plans
- Prevents boredom
- Adapts to progress

**Note:** System ensures 77% variety over 14 days = low repetition!

---

### Q: What about macros (protein/carbs/fats)?

**A:** System optimizes macros per goal:

**Mass Gain:**
- Protein: 30%
- Carbs: 50%
- Fats: 20%

**Maintenance:**
- Protein: 25%
- Carbs: 45%
- Fats: 30%

**Weight Loss:**
- Protein: 40%
- Carbs: 35%
- Fats: 25%

**Note:** These are approximations. Actual macros vary by food selection.

---

### Q: Can diabetics use this?

**A:** **Consult your doctor first!**

The system is designed for healthy individuals.

**Diabetic considerations:**
- Carb timing matters
- Glycemic index not tracked
- Insulin management crucial
- Medical supervision required

**We recommend:**
- Show generated plan to your doctor
- Adjust per medical advice
- Monitor blood glucose
- Use as reference, not prescription

---

## 🔒 Privacy & Security Questions

### Q: What data do you collect?

**A:** **Zero data collection!**

- ❌ No user accounts
- ❌ No login required
- ❌ No tracking cookies
- ❌ No analytics
- ❌ No telemetry
- ❌ No cloud sync

**Everything stays on your machine.**

---

### Q: Is the source code available?

**A:** **No**, it's proprietary.

**What's public:**
- Docker image (pre-built)
- User documentation
- docker-compose.yml

**What's private:**
- Source code
- Algorithms
- Food database structure
- Scoring formulas

**Commercial license includes:**
- Full source code
- White-label rights
- Custom development

[Contact for pricing](mailto:christiangri@live.it)

---

### Q: Can I use this commercially?

**A:** **No**, not with the free Docker version.

**Free license allows:**
- ✅ Personal use
- ✅ Testing & evaluation
- ✅ Educational purposes

**Prohibited:**
- ❌ Selling diet plans generated
- ❌ Integrating in paid apps/websites
- ❌ Using in nutrition business
- ❌ Reselling or redistributing

**Commercial license available** for business use.

---

## 🚀 Updates & Roadmap Questions

### Q: How often is it updated?

**A:** Actively maintained!

**Update schedule:**
- Major versions: Quarterly (v1.0, v2.0)
- Minor versions: Monthly (v3.1, v3.2)
- Bug fixes: As needed

**How to update:**
```bash
docker-compose pull
docker-compose up -d
```

**Follow updates:**
- [GitHub Releases](https://github.com/yourusername/ai-diet-generator-public/releases)
- [LinkedIn](https://www.linkedin.com/in/christian-grieco-340bba194/)

---

### Q: What's in the roadmap?

**v3.1 (Feb 2026):**
- ✅ Allergen filters
- ✅ Improved booster system for mass gain
- ✅ More vegetables variety

**v3.5 (Apr 2026):**
- 🔄 Dietary restrictions (vegan, vegetarian)
- 🔄 Recipe suggestions
- 🔄 Multi-language support

**v4.0 (Q3 2026):**
- 🔄 User accounts & history
- 🔄 Mobile app (iOS/Android)
- 🔄 Wearable integration

[Vote on features](https://github.com/yourusername/ai-diet-generator-public/discussions)

---

### Q: Can I request features?

**A:** Yes! Feature requests welcome.

**How to request:**
1. Search [existing discussions](https://github.com/yourusername/ai-diet-generator-public/discussions)
2. If not found, [create new discussion](https://github.com/yourusername/ai-diet-generator-public/discussions/new)
3. Describe use case and benefit
4. Community votes on features

**Most voted features get priority!**

---

## 💼 Licensing Questions

### Q: Can I see the algorithm?

**A:** Not in the free version.

**What we can share:**
- High-level approach (in README)
- Validation results
- Performance metrics
- Research methodology

**What's proprietary:**
- Exact scoring formulas
- Normalization methods
- Booster thresholds
- Variety tracking algorithm

**Commercial license includes:** Full algorithm documentation + source code.

---

### Q: Why is it proprietary?

**A:** Several reasons:

1. **Protect IP**: 3 months R&D investment
2. **Prevent misuse**: Ensure ethical use
3. **Quality control**: Maintain accuracy
4. **Sustainability**: Fund development
5. **Support**: Provide quality support

**We provide:**
- Free personal use via Docker
- Transparent validation (84 days)
- Open bug reports
- Feature requests

---

### Q: How much is commercial license?

**A:** Depends on use case:

**Pricing tiers:**
- **Small Business** (1-10 users): Contact for quote
- **Enterprise** (10+ users): Contact for quote
- **White-label**: Contact for quote
- **Source code**: Contact for quote

**What's included:**
- Source code access
- Custom food database
- Commercial use rights
- Priority support
- Custom features

[Request quote](mailto:christiangri@live.it)

---

## 🆘 Support Questions

### Q: Where can I get help?

**A:** Multiple channels:

1. **Documentation:**
   - [QUICKSTART.md](QUICKSTART.md)
   - [TROUBLESHOOTING.md](TROUBLESHOOTING.md)
   - [FAQ.md](FAQ.md) (this file)

2. **Community:**
   - [GitHub Discussions](https://github.com/yourusername/ai-diet-generator-public/discussions)
   - [GitHub Issues](https://github.com/yourusername/ai-diet-generator-public/issues)

3. **Direct:**
   - [Email](mailto:christiangri@live.it)
   - [LinkedIn](https://www.linkedin.com/in/christian-grieco-340bba194/)

**Response time:**
- Issues: 24-48h
- Discussions: 2-7 days
- Email: 3-5 days

---

### Q: Found a bug, what do I do?

**A:** Report it!

1. **Search** [existing issues](https://github.com/yourusername/ai-diet-generator-public/issues)
2. If not found, [open new issue](https://github.com/yourusername/ai-diet-generator-public/issues/new?template=bug_report.md)
3. Use **Bug Report template**
4. Include:
   - Steps to reproduce
   - Expected vs actual behavior
   - System info
   - Logs

**We fix bugs fast!** Critical bugs in 24-48h.

---

### Q: Can I contribute?

**A:** Currently: **No** (proprietary codebase).

**What you CAN do:**
- 🐛 Report bugs
- 💡 Suggest features
- 📚 Improve documentation
- 🌍 Help with translations (v3.5+)
- ⭐ Star the repo!

**Future:** May open-source parts of the system (TBD).

---

## 🎯 Best Practices

### Q: Tips for best results?

**A:** Follow these guidelines:

**1. Accurate Data:**
- Weigh yourself in morning, after bathroom
- Measure height without shoes
- Be honest about activity level

**2. Realistic Goals:**
- Start with 7 days to test
- Don't over-adjust parameters
- Trust the algorithm

**3. Consistency:**
- Follow portions as specified
- Use kitchen scale for accuracy
- Track daily for 2+ weeks

**4. Flexibility:**
- If you don't like a meal, regenerate
- Swap similar foods (fish for fish)
- Adjust timing to your schedule

**5. Patience:**
- Results take 2-4 weeks
- Weight fluctuates daily (normal!)
- Focus on weekly trends

---

### Q: Common mistakes to avoid?

**A:** Avoid these:

**❌ Overestimating Activity:**
- Most people are "Sedentary" or "Light"
- "Moderate" is physical labor (construction, etc.)

**❌ Ignoring Portions:**
- System is precise: 150g ≠ 200g
- Use kitchen scale

**❌ Skipping Meals:**
- All 5 meals designed for balance
- Skipping = nutrient gaps

**❌ Too Aggressive Goals:**
- Weight loss ≠ starvation
- Muscle gain ≠ dirty bulk
- Be patient!

**❌ Not Tracking:**
- No tracking = no accountability
- Use app or journal

---

## 📞 Still Have Questions?

**Not answered here?**

1. 💬 [Start a discussion](https://github.com/yourusername/ai-diet-generator-public/discussions/new)
2. 📧 [Email us](mailto:christiangri@live.it)
3. 💼 [LinkedIn message](https://www.linkedin.com/in/christian-grieco-340bba194/)

---

**Last updated:** January 4, 2026

**Found this helpful?** [⭐ Star the repo!](https://github.com/yourusername/ai-diet-generator-public)