# Nutrition_Calculator
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Nutrition & Intake Tracker with Personal Info</title>
<style>
  body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: #fafafa;
    margin: 0;
    padding: 0;
    color: #222;
  }
  header {
    background: #007acc;
    color: white;
    padding: 16px;
    text-align: center;
    font-size: 1.5rem;
    font-weight: bold;
  }
  .tabs {
    display: flex;
    justify-content: center;
    background: #005fa3;
  }
  .tab {
    padding: 14px 28px;
    cursor: pointer;
    color: white;
    font-weight: 600;
    user-select: none;
    transition: background 0.3s;
  }
  .tab:hover {
    background: #00467a;
  }
  .tab.active {
    background: white;
    color: #007acc;
    border-bottom: 3px solid #007acc;
  }
  .tab-content {
    max-width: 700px;
    margin: 20px auto 40px;
    background: white;
    padding: 20px;
    box-shadow: 0 0 12px rgba(0,0,0,0.1);
    border-radius: 8px;
  }
  .hidden {
    display: none;
  }
  label {
    display: block;
    margin: 12px 0 6px;
    font-weight: 600;
  }
  input[type=text], input[type=number], select {
    width: 100%;
    padding: 10px 12px;
    font-size: 1rem;
    border: 1px solid #ccc;
    border-radius: 6px;
    box-sizing: border-box;
  }
  button {
    margin-top: 12px;
    padding: 10px 20px;
    font-size: 1rem;
    background: #007acc;
    color: white;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    transition: background 0.3s;
  }
  button:hover {
    background: #005fa3;
  }
  #searchResults {
    margin-top: 20px;
  }
  .food-item {
    border-bottom: 1px solid #ddd;
    padding: 10px 0;
    cursor: pointer;
  }
  .food-item:hover {
    background: #e6f2ff;
  }
  .nutrition-info {
    margin-top: 6px;
    font-size: 0.9rem;
    color: #555;
  }
  .tracker-section {
    margin-top: 20px;
  }
  .progress-bar {
    height: 25px;
    background: #ddd;
    border-radius: 12px;
    overflow: hidden;
    margin: 6px 0 12px;
  }
  .progress-fill {
    height: 100%;
    border-radius: 12px;
    background: #007acc;
    width: 0%;
    transition: width 0.5s ease-in-out;
  }
  .history-list {
    margin-top: 12px;
    max-height: 150px;
    overflow-y: auto;
    border: 1px solid #ccc;
    border-radius: 6px;
    padding: 8px;
    background: #f9f9f9;
  }
  .history-list li {
    font-size: 0.9rem;
    padding: 6px 4px;
    border-bottom: 1px solid #eee;
  }
  .history-list li:last-child {
    border-bottom: none;
  }
  .clear-btn {
    background: #d9534f;
    margin-left: 10px;
  }
  .clear-btn:hover {
    background: #b52b27;
  }
  .form-row {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
  }
  .form-row > div {
    flex: 1 1 150px;
  }
  @media (max-width: 720px) {
    .tabs {
      flex-wrap: wrap;
    }
    .tab {
      flex: 1 1 50%;
      text-align: center;
      padding: 12px 0;
    }
    .tab-content {
      margin: 10px 10px 30px;
    }
    .form-row {
      flex-direction: column;
    }
  }
</style>
</head>
<body>

<header>Nutrition Tracker & Food Search</header>

<div class="tabs">
  <div id="tab-intake" class="tab active" role="tab" aria-selected="true" tabindex="0" aria-controls="intakeContent">Intake Tracker</div>
  <div id="tab-search" class="tab" role="tab" aria-selected="false" tabindex="-1" aria-controls="searchContent">Food Search</div>
</div>

<div id="intakeContent" class="tab-content" role="tabpanel" aria-labelledby="tab-intake">
  <h2>Your Info & Daily Goals</h2>
  <form id="userInfoForm" aria-label="User information form">
    <div class="form-row">
      <div>
        <label for="weightInput">Weight</label>
        <input type="number" id="weightInput" min="1" max="635" step="0.1" placeholder="Enter your weight" aria-describedby="weightHelp" required />
        <small id="weightHelp">Pounds (lbs) or Kilograms (kg)</small>
      </div>
      <div>
        <label for="weightUnit">Unit</label>
        <select id="weightUnit" aria-label="Select weight unit">
          <option value="lbs" selected>Pounds (lbs)</option>
          <option value="kg">Kilograms (kg)</option>
        </select>
      </div>
      <div>
        <label for="heightInput">Height (optional)</label>
        <input type="number" id="heightInput" min="30" max="250" step="1" placeholder="Height in cm" aria-describedby="heightHelp" />
        <small id="heightHelp">Useful for more accurate calculations</small>
      </div>
    </div>
    <button type="submit" aria-label="Calculate daily goals">Calculate Goals</button>
  </form>

  <div id="goalsOutput" style="margin-top:20px; display:none;">
    <p><strong>Recommended Daily Calorie Intake:</strong> <span id="calorieGoalText"></span> kcal</p>
    <p><strong>Recommended Daily Water Intake:</strong> <span id="waterGoalText"></span> liters</p>
  </div>

  <h2>Track Your Daily Intake</h2>
  
  <div class="tracker-section">
    <label>Calories</label>
    <div class="progress-bar" aria-label="Calories progress">
      <div id="calorieBar" class="progress-fill"></div>
    </div>
    <span id="calorieText">0 / 2000 kcal</span>
  </div>
  
  <div class="tracker-section">
    <label>Protein</label>
    <div class="progress-bar" aria-label="Protein progress">
      <div id="proteinBar" class="progress-fill"></div>
    </div>
    <span id="proteinText">0 / 150 g</span>
  </div>
  
  <div class="tracker-section">
    <label>Carbohydrates</label>
    <div class="progress-bar" aria-label="Carbohydrates progress">
      <div id="carbBar" class="progress-fill"></div>
    </div>
    <span id="carbText">0 / 300 g</span>
  </div>

  <div class="tracker-section">
    <label>Water Intake</label>
    <div class="progress-bar" aria-label="Water intake progress">
      <div id="waterBar" class="progress-fill" style="background:#17a2b8;"></div>
    </div>
    <span id="waterText">0 / 3 liters</span>
  </div>
  
  <button id="clearIntakeBtn" class="clear-btn" aria-label="Clear intake tracker data">Clear Intake</button>
  
  <h3>History</h3>
  <ul id="historyList" class="history-list" aria-live="polite" aria-relevant="additions"></ul>
</div>

<div id="searchContent" class="tab-content hidden" role="tabpanel" aria-labelledby="tab-search">
  <h2>Search Food Nutrition Info</h2>
  <label for="foodSearchInput">Enter food name or description:</label>
  <input id="foodSearchInput" type="text" placeholder="e.g., apple, grilled chicken" autocomplete="off" aria-autocomplete="list" aria-controls="searchResults" aria-expanded="false"/>
  <button id="searchBtn" aria-label="Search food">Search</button>
  
  <div id="searchResults" role="listbox" aria-live="polite" aria-relevant="additions"></div>
</div>

<script>
  // Tab switching
  const tabIntake = document.getElementById('tab-intake');
  const tabSearch = document.getElementById('tab-search');
  const intakeContent = document.getElementById('intakeContent');
  const searchContent = document.getElementById('searchContent');

  function activateTab(tabToActivate, contentToShow) {
    [tabIntake, tabSearch].forEach(tab => {
      tab.classList.remove('active');
      tab.setAttribute('aria-selected', 'false');
      tab.tabIndex = -1;
    });
    [intakeContent, searchContent].forEach(content => content.classList.add('hidden'));

    tabToActivate.classList.add('active');
    tabToActivate.setAttribute('aria-selected', 'true');
    tabToActivate.tabIndex = 0;
    contentToShow.classList.remove('hidden');
  }

  tabIntake.onclick = () => activateTab(tabIntake, intakeContent);
  tabSearch.onclick = () => activateTab(tabSearch, searchContent);

  tabIntake.addEventListener('keydown', e => {
    if(e.key === 'Enter' || e.key === ' ') {
      activateTab(tabIntake, intakeContent);
      e.preventDefault();
    }
  });
  tabSearch.addEventListener('keydown', e => {
    if(e.key === 'Enter' || e.key === ' ') {
      activateTab(tabSearch, searchContent);
      e.preventDefault();
    }
  });

  // Intake tracking variables & limits (default goals)
  let dailyGoals = {
    calories: 2000,
    protein: 150,
    carbs: 300,
    waterLiters: 3
  };

  let intake = {
    calories: 0,
    protein: 0,
    carbs: 0,
    waterLiters: 0
  };

  // Elements for bars & text
  const calorieBar = document.getElementById('calorieBar');
  const proteinBar = document.getElementById('proteinBar');
  const carbBar = document.getElementById('carbBar');
  const waterBar = document.getElementById('waterBar');
  const calorieText = document.getElementById('calorieText');
  const proteinText = document.getElementById('proteinText');
  const carbText = document.getElementById('carbText');
  const waterText = document.getElementById('waterText');
  const historyList = document.getElementById('historyList');
  const clearBtn = document.getElementById('clearIntakeBtn');

  // Update progress bars and texts
  function updateIntakeUI() {
    const calPercent = Math.min(100, (intake.calories / dailyGoals.calories) * 100);
    const proteinPercent = Math.min(100, (intake.protein / dailyGoals.protein) * 100);
    const carbPercent = Math.min(100, (intake.carbs / dailyGoals.carbs) * 100);
    const waterPercent = Math.min(100, (intake.waterLiters / dailyGoals.waterLiters) * 100);

    calorieBar.style.width = calPercent + '%';
    proteinBar.style.width = proteinPercent + '%';
    carbBar.style.width = carbPercent + '%';
    waterBar.style.width = waterPercent + '%';

    calorieText.textContent = `${intake.calories.toFixed(0)} / ${dailyGoals.calories} kcal`;
    proteinText.textContent = `${intake.protein.toFixed(1)} / ${dailyGoals.protein} g`;
    carbText.textContent = `${intake.carbs.toFixed(1)} / ${dailyGoals.carbs} g`;
    waterText.textContent = `${intake.waterLiters.toFixed(2)} / ${dailyGoals.waterLiters} liters`;
  }

  // Add item to history
  function addHistoryItem(name, cal, protein, carbs) {
    const li = document.createElement('li');
    li.textContent = `${name} — Calories: ${cal.toFixed(0)} kcal, Protein: ${protein.toFixed(1)} g, Carbs: ${carbs.toFixed(1)} g`;
    historyList.prepend(li);
  }

  // Clear intake & history
  clearBtn.onclick = () => {
    intake = { calories: 0, protein: 0, carbs: 0, waterLiters: 0 };
    updateIntakeUI();
    historyList.innerHTML = '';
  };

  updateIntakeUI();

  // User info form and daily goal calculation
  const userInfoForm = document.getElementById('userInfoForm');
  const weightInput = document.getElementById('weightInput');
  const weightUnit = document.getElementById('weightUnit');
  const heightInput = document.getElementById('heightInput');
  const calorieGoalText = document.getElementById('calorieGoalText');
  const waterGoalText = document.getElementById('waterGoalText');
  const goalsOutput = document.getElementById('goalsOutput');

  userInfoForm.addEventListener('submit', (e) => {
    e.preventDefault();

    let weight = parseFloat(weightInput.value);
    if (isNaN(weight) || weight <= 0) {
      alert('Please enter a valid weight.');
      return;
    }
    const unit = weightUnit.value;
    if (unit === 'kg') {
      weight = weight * 2.20462; // convert to pounds for calculation
    }

    if (weight > 1400) {
      alert('Weight must be less than or equal to 1400 lbs.');
      return;
    }

    // Optional: height ignored in this simple formula but you can expand it later

    // Calculate calorie goal:
    // Rough estimate: 15 calories per pound body weight per day
    const calorieGoal = Math.round(weight * 15);

    // Water intake recommendation: roughly 0.033 liters per lb (~30-35 ml)
    // Or about 1 oz per 2 lbs = 0.015 liters per lb but using 0.033 for better hydration
    const waterGoalLiters = +(weight * 0.033).toFixed(2);

    // Update daily goals
    dailyGoals.calories = calorieGoal;
    dailyGoals.waterLiters = waterGoalLiters;

    // Protein and carbs keep defaults (or can add formulas here too)
    // protein = 0.8g per lb approx: protein = weight * 0.8 (optional)
    dailyGoals.protein = Math.round(weight * 0.8);

    // carbs keep at 300g default or can be customized here

    // Show results
    calorieGoalText.textContent = calorieGoal;
    waterGoalText.textContent = waterGoalLiters;

    goalsOutput.style.display = 'block';

    // Reset intake tracker with new goals
    intake = { calories: 0, protein: 0, carbs: 0, waterLiters: 0 };
    updateIntakeUI();

    alert('Daily goals updated! Now you can track your intake.');
  });

  // --- Food Search and API integration ---

  const foodSearchInput = document.getElementById('foodSearchInput');
  const searchBtn = document.getElementById('searchBtn');
  const searchResults = document.getElementById('searchResults');

  // Edamam Nutrition API demo endpoint & app id/key (demo keys)
  // Docs: https://developer.edamam.com/edamam-docs-nutrition-api
  const EDAMAM_APP_ID = 'demo';
  const EDAMAM_APP_KEY = 'demo';

  async function searchFood(query) {
    searchResults.innerHTML = '<p>Loading...</p>';
    try {
      const res = await fetch(`https://api.edamam.com/api/nutrition-data?app_id=${EDAMAM_APP_ID}&app_key=${EDAMAM_APP_KEY}&ingr=${encodeURIComponent(query)}`);
      if (!res.ok) throw new Error('API error');
      const data = await res.json();
      if (data.calories === 0) {
        searchResults.innerHTML = `<p>No nutrition data found for "${query}". Try a different food.</p>`;
        return;
      }
      // Display data as a single result since this API returns nutrition info for whole query
      displayFoodResult(query, data);
    } catch (err) {
      searchResults.innerHTML = `<p style="color:red;">Error fetching data. Try again later.</p>`;
      console.error(err);
    }
  }

  function displayFoodResult(name, data) {
    searchResults.innerHTML = '';
    // Create food item div with nutrition details and click to add to intake
    const div = document.createElement('div');
    div.classList.add('food-item');
    div.setAttribute('role', 'option');
    div.tabIndex = 0;

    div.innerHTML = `
      <strong>${name}</strong>
      <div class="nutrition-info">
        Calories: ${data.calories.toFixed(0)} kcal<br/>
        Protein: ${((data.totalNutrients?.PROCNT?.quantity) || 0).toFixed(1)} g<br/>
        Carbs: ${((data.totalNutrients?.CHOCDF?.quantity) || 0).toFixed(1)} g
      </div>
      <small>Click to add to intake</small>
    `;

    div.onclick = () => {
      // Add to intake tracker
      intake.calories += data.calories || 0;
      intake.protein += (data.totalNutrients?.PROCNT?.quantity) || 0;
      intake.carbs += (data.totalNutrients?.CHOCDF?.quantity) || 0;
      updateIntakeUI();
      addHistoryItem(name, data.calories, intake.protein, intake.carbs);
    };

    div.onkeypress = (e) => {
      if (e.key === 'Enter' || e.key === ' ') {
        div.click();
      }
    };

    searchResults.appendChild(div);
  }

  searchBtn.onclick = () => {
    const query = foodSearchInput.value.trim();
    if (query.length < 2) {
      alert('Please enter at least 2 characters to search.');
      return;
    }
    searchFood(query);
  };

  foodSearchInput.addEventListener('keydown', (e) => {
    if (e.key === 'Enter') {
      searchBtn.click();
    }
  });
</script>

</body>
</html>



