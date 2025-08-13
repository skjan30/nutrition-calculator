# Nutrition_Calculator
# Nutrition & Intake Tracker with Food Search

A sleek, single-page web app that helps you calculate your personalized daily nutrition goals and effortlessly track your food and water intake—with real-time nutrition lookup using the Edamam Nutrition API.

---

##  Features

1. **Personalized Daily Goals**  
   Enter your weight (in lbs or kg), and the app instantly calculates:
   - Daily calorie target (approx. 15 kcal per pound)
   - Protein goal (~0.8 g per pound)
   - Daily water recommendation (approx. 0.033 L per pound)

2. **Visual Intake Tracker**  
   Track your:
   - Calories (kcal)  
   - Protein (g)  
   - Carbohydrates (g)  
   - Water intake (L)  
   Progress bars dynamically fill as you log entries.

3. **Food Search with Real Nutrition Data**  
   Use the **Food Search** tab to look up any food or meal description. The app fetches real nutritional info via the **Edamam Nutrition API (demo key)**. Click the result to instantly add its calories, protein, and carbs to your tracker.

4. **History & Clear Option**  
   Every logged item appears in a scrollable history list. Use the **"Clear Intake"** button to reset daily tracking—all stored in the current browser session.

5. **Responsive & Accessible UI**  
   Clean design that works on desktop and mobile. Keyboard navigable and ARIA-friendly for accessibility.

---

##  How to Use

1. **Open `index.html` in your browser**.  
2. In the **Intake Tracker** tab:  
   - Enter your weight and unit; click **Calculate Goals**.  
   - Your daily targets will display, and trackers will reset.  
3. Switch to **Food Search**:  
   - Type something like "apple", "2 eggs and toast", etc., and click **Search**.  
   - Click the result to log it—your tracker updates instantly.  
4. Review your daily totals and progress in the **Intake Tracker** tab.  
5. Use **Clear Intake** to start fresh at any time.

---

##  Tech Stack & Implementation

- **Front-end only**: Plain HTML, CSS, and JavaScript—no build tools needed.  
- **Edamam Nutrition API (demo)**: Provides calorie, protein, and carb data from food queries.  
- **Calculator Logic**: Uses user input to compute goals and dynamically update tracking UI.  
- **History Management**: Simple in-memory array for current session—no backend or database required.

---

##  Future Enhancements (Coming Soon)

- **Secure API usage**, via a backend or serverless function, to hide credentials.  
- **Persistent storage** using localStorage or backend DB so data survives page reloads.  
- **Expand nutrient tracking** to include fats, fiber, sugars, etc.  
- **Camera integration** for automated meal detection (object recognition / OCR).  
- **Weekly summaries** and progress charts.

---

##  Attribution & Contact

Built and maintained by **Srithik Kumar** — passionate about making coding and health tracking fun and accessible.

- Email: ksrithik30@gmail.com  
- GitHub: [skjan30](https://github.com/skjan30)  
- YouTube: [Srithik Kumar](https://www.youtube.com/@srithikkumar4170)

