# HealthyMe
HealthyMe - BMI Calculator 📱✨

Welcome to HealthyMe, your all-in-one BMI Calculator app that not only calculates your Body Mass Index (BMI) but also provides personalized food and exercise suggestions to help you stay healthy! 🌟

🌟 Features at a Glance

BMI Calculation: Input your height and weight to instantly calculate your BMI. 📊

Food Suggestions: Get tailored food recommendations based on your BMI category. 🍎

Exercise Tips: Discover workout routines to achieve or maintain a healthy BMI. 🏋️‍♀️

Motivational Quotes: Stay inspired with random quotes after each BMI calculation. 🌈

Dynamic UI: An interactive, user-friendly interface with a clean and responsive design. 🖼️

🚀 How It Works

Enter Details: Provide your gender, height, weight, and preferred units.

Calculate BMI: Click on the "Calculate BMI" button to get your results instantly.

Explore Suggestions: Choose between food or exercise suggestions tailored for your BMI range.

Stay Motivated: Read a random motivational quote after every calculation.

Recalculate: Use the "Calculate Again" button to analyze new inputs.

🛠️ Technologies Used

HTML: The backbone of the app, creating the structure and form inputs. 🧱

Provides a user-friendly BMI calculation form.

Displays BMI results and suggestions dynamically.

CSS: Enhances the visual appeal and responsiveness of the app. 🎨

Implements gradients, shadows, and a modern card design.

Ensures consistency across devices with responsive styling.

JavaScript: Brings the app to life with interactivity and logic. ⚡

Calculates BMI based on user inputs.

Dynamically updates suggestions and motivational quotes.

Handles UI transitions like showing/hiding sections.

🌐 How I Built This

CodePen: Developed and tested the app using CodePen. 🛠️

Flaticon: Downloaded icons from Flaticon. 🎨

Tiiny Host: Deployed the web app online using Tiiny Host. 🌍

Web Into App: Converted the web app into a mobile app APK using Web Into App. 📱

CODE FOR THIS APP :
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>HealthyMe - BMI Calculator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(to right, #a8edea, #fed6e3);
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    .container {
      background-color: white;
      padding: 30px;
      border-radius: 10px;
      width: 100%;
      max-width: 600px;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
    }

    h1, h2 {
      text-align: center;
      margin-bottom: 20px;
      color: #333;
    }

    label {
      font-size: 1.1em;
      margin-bottom: 8px;
      display: block;
    }

    input, select, button {
      width: 100%;
      padding: 10px;
      margin-bottom: 15px;
      border-radius: 5px;
      border: 1px solid #ccc;
      font-size: 1em;
    }

    button {
      background-color: #4CAF50;
      color: white;
      cursor: pointer;
    }

    button:hover {
      background-color: #45a049;
    }

    #suggestionButtons {
      margin-bottom: 20px;
    }

    #foodContent, #exerciseContent {
      display: none;
      margin-top: 20px;
    }

    ul {
      list-style-type: none;
      padding-left: 0;
    }

    ul li {
      margin: 8px 0;
    }

    #calculateAgainButton {
      display: none;
      width: auto;
      margin-top: 20px;
      background-color: #2196F3;
    }

    /* Popup for Thank You Message */
    #thankYouPopup {
      display: none;
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background-color: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
      text-align: center;
    }

    #thankYouPopup button {
      background-color: #4CAF50;
      color: white;
      padding: 10px 20px;
      border-radius: 5px;
      cursor: pointer;
      border: none;
    }

    #thankYouPopup button:hover {
      background-color: #45a049;
    }
  </style>
</head>
<body>

  <div class="container">
    <!-- BMI Form -->
    <div id="bmiForm">
      <h1>HealthyMe - BMI Calculator</h1>
      <h2>Enter your details to calculate BMI</h2>
      <form>
        <!-- Gender -->
        <label for="gender">Gender:</label>
        <select id="gender">
          <option value="male">Male</option>
          <option value="female">Female</option>
          <option value="other">Other</option>
        </select>

        <!-- Height Unit -->
        <label for="heightUnit">Height Unit:</label>
        <select id="heightUnit">
          <option value="cm">Centimeters (cm)</option>
          <option value="inches">Inches (in)</option>
        </select>

        <!-- Weight Unit -->
        <label for="weightUnit">Weight Unit:</label>
        <select id="weightUnit">
          <option value="kg">Kilograms (kg)</option>
          <option value="pounds">Pounds (lbs)</option>
        </select>

        <!-- Height -->
        <label for="height">Height:</label>
        <input type="number" id="height" placeholder="Enter height" required>

        <!-- Weight -->
        <label for="weight">Weight:</label>
        <input type="number" id="weight" placeholder="Enter weight" required>

        <!-- Calculate Button -->
        <button type="button" onclick="calculateBMI()">Calculate BMI</button>
      </form>
    </div>

    <!-- BMI Result and Suggestions -->
    <div id="bmiResultContent" style="display: none;">
      <p id="bmiResult"></p>
      <p id="suggestionMessage"></p>
      
      <div id="suggestionButtons">
        <button onclick="showFoodSuggestions()">Food Suggestions</button>
        <button onclick="showExerciseSuggestions()">Exercise Suggestions</button>
      </div>

      <div id="foodContent">
        <h3>Food Suggestions 🍽️</h3>
        <ul id="foodList"></ul>
      </div>

      <div id="exerciseContent">
        <h3>Exercise Suggestions 🏋️</h3>
        <ul id="exerciseList"></ul>
      </div>

      <!-- Calculate Again Button -->
      <button id="calculateAgainButton" onclick="showBMIForm()">Calculate BMI Again</button>
    </div>
  </div>

  <!-- Thank You Popup -->
  <div id="thankYouPopup">
    <h2>Thank you! 🙌</h2>
    <p id="quote"></p>
    <button onclick="closePopup()">Close</button>
  </div>

  <script>
    // Array of motivational quotes
    const quotes = [
      "Strength does not come from what you can do. It comes from overcoming the things you once thought you couldn’t! 🏆",
      "Success is not final, failure is not fatal: It is the courage to continue that counts. 💪",
      "The only limit to our realization of tomorrow is our doubts of today. 🌟",
      "Your only limit is you! Believe in yourself. 🚀",
      "Hardships often prepare ordinary people for an extraordinary destiny. ✨",
      "Don’t stop when you’re tired, stop when you’re done! 🔥",
      "The harder you work for something, the greater you’ll feel when you achieve it. 🎯",
      "Believe in yourself and all that you are. Know that there is something inside you that is greater than any obstacle. 💥",
      "Your future is created by what you do today, not tomorrow. 🌞",
      "It always seems impossible until it’s done. 🏅"
    ];

    // Function to calculate BMI
    function calculateBMI() {
      let height = parseFloat(document.getElementById("height").value);
      let weight = parseFloat(document.getElementById("weight").value);
      let heightUnit = document.getElementById("heightUnit").value;
      let weightUnit = document.getElementById("weightUnit").value;

      // Convert height to meters if in centimeters or inches
      if (heightUnit === "inches") {
        height = height * 0.0254; // Convert inches to meters
      } else {
        height = height / 100; // Convert cm to meters
      }

      // Convert weight to kilograms if in pounds
      if (weightUnit === "pounds") {
        weight = weight * 0.453592; // Convert pounds to kilograms
      }

      // BMI Calculation
      let bmi = weight / (height * height);
      bmi = bmi.toFixed(2); // Round to 2 decimal places

      // Display BMI Result
      document.getElementById("bmiResult").innerHTML = "Your BMI: " + bmi;

      // Display Suggestions based on BMI
      let suggestionMessage = "";
      let foodSuggestions = [];
      let exerciseSuggestions = [];

      if (bmi < 18.5) {
        suggestionMessage = "You are underweight. Let's focus on gaining healthy weight!";
        foodSuggestions = [
          "Whole Grain Oats 🍚 – Rich in fiber and carbs, helping you gain healthy weight.",
          "Avocados 🥑 – Packed with healthy fats and calories.",
          "Nuts and Nut Butters 🥜 – High-calorie, healthy fats for weight gain.",
          "Full-fat Dairy 🧀 – Milk, cheese, and yogurt are calorie-dense.",
          "Lean Meats 🍗 – Chicken, turkey, and lean beef to increase protein intake.",
          "Quinoa 🍚 – A high-protein whole grain, great for building muscle.",
          "Bananas 🍌 – High in carbohydrates, offering a quick energy boost.",
          "Sweet Potatoes 🍠 – Full of healthy carbs, vitamins, and minerals.",
          "Smoothies 🍹 – Homemade smoothies with protein powder, nut butters, and fruits.",
          "Dark Chocolate 🍫 – Provides healthy fats and antioxidants."
        ];
        exerciseSuggestions = [
          "Deadlifts 🏋️", "Squats 🏋️", "Bench Press 💪", "Pull-ups 🚶‍♂️", "Push-ups 🤸‍♀️", 
          "Lunges 🚶‍♀️", "Bicep Curls 💪", "Shoulder Press 💪", "Leg Raises 🦵", "Planks 🏖️"
        ];
      } else if (bmi >= 18.5 && bmi < 24.9) {
        suggestionMessage = "You have a healthy weight. Keep up the good work!";
        foodSuggestions = [
          "Quinoa 🍚 – A balanced source of protein and carbs, maintaining energy levels.",
          "Chicken Breast 🍗 – A lean source of protein to maintain muscle mass.",
          "Oats 🍚 – Full of fiber and slow-digesting carbs, ideal for sustained energy.",
          "Broccoli 🥦 – High in vitamins and fiber, helping maintain overall health.",
          "Sweet Potatoes 🍠 – A nutrient-dense carb option that provides steady energy.",
          "Eggs 🍳 – A versatile protein source to balance meals.",
          "Nuts and Seeds 🥜 – Healthy fats for balanced energy and maintaining a healthy weight.",
          "Cottage Cheese 🧀 – Protein-rich dairy that supports muscle and bone health.",
          "Apples 🍏 – A fiber-rich fruit to keep you full without adding too many calories.",
          "Whole Grains (Brown Rice, Whole Wheat Pasta) 🌾 – Essential for sustained energy without spiking blood sugar."
        ];
        exerciseSuggestions = [
          "Push-ups 🤸‍♂️", "Squats 🏋️", "Lunges 🚶‍♂️", "Deadlifts 🏋️", "Pull-ups 🚶‍♀️", 
          "Running 🏃‍♂️", "Cycling 🚴", "Planks 🏖️", "Leg Raises 🦵", "Russian Twists 🔄"
        ];
      } else {
        suggestionMessage = "You are overweight. Let's work on losing weight in a healthy way!";
        foodSuggestions = [
          "Leafy Greens 🥗 – Spinach, kale, and lettuce are low in calories but high in nutrients.",
          "Grilled Chicken 🍗 – A lean source of protein, perfect for satiety without excess calories.",
          "Greek Yogurt 🥣 – High in protein and calcium, with fewer calories than regular yogurt.",
          "Salmon 🐟 – Rich in omega-3 fatty acids, which help reduce inflammation and support fat loss.",
          "Cucumbers 🥒 – Low in calories, hydrating, and great for snacks.",
          "Cauliflower 🥦 – Low-calorie vegetable rich in fiber, great for replacing high-calorie foods.",
          "Berries 🍓 – Low in sugar and high in fiber, good for satisfying sweet cravings.",
          "Eggs 🍳 – High in protein and healthy fats, helping to feel fuller for longer.",
          "Zucchini 🥒 – A low-calorie, versatile vegetable that can be used in various dishes.",
          "Chia Seeds 🌱 – High in fiber and omega-3s, they help with digestion and can keep you full."
        ];
        exerciseSuggestions = [
          "Running 🏃‍♀️", "Cycling 🚴", "Jump Rope 🪢", "HIIT (High-Intensity Interval Training) 💪", 
          "Squats 🏋️", "Lunges 🚶‍♀️", "Push-ups 🤸‍♂️", "Burpees 🔥", "Mountain Climbers 🧗‍♀️", "Planks 🏖️"
        ];
      }

      document.getElementById("suggestionMessage").innerHTML = suggestionMessage;

      // Update Food Suggestions
      let foodList = document.getElementById("foodList");
      foodList.innerHTML = "";
      foodSuggestions.forEach(function(food) {
        let li = document.createElement("li");
        li.textContent = food;
        foodList.appendChild(li);
      });

      // Update Exercise Suggestions
      let exerciseList = document.getElementById("exerciseList");
      exerciseList.innerHTML = "";
      exerciseSuggestions.forEach(function(exercise) {
        let li = document.createElement("li");
        li.textContent = exercise;
        exerciseList.appendChild(li);
      });

      // Show the BMI result and suggestions
      document.getElementById("bmiResultContent").style.display = "block";
      document.getElementById("calculateAgainButton").style.display = "block";

      // Show a random motivational quote in the popup
      const randomQuote = quotes[Math.floor(Math.random() * quotes.length)];
      document.getElementById("quote").innerText = randomQuote;

      // Show the Thank You popup after suggestions
      setTimeout(() => {
        document.getElementById("thankYouPopup").style.display = "block";
      }, 2000);

      // Hide the initial form
      document.getElementById("bmiForm").style.display = "none";
    }

    // Function to show the BMI Form again
    function showBMIForm() {
      document.getElementById("bmiForm").style.display = "block";
      document.getElementById("bmiResultContent").style.display = "none";
      document.getElementById("thankYouPopup").style.display = "none";
      document.getElementById("calculateAgainButton").style.display = "none";
    }

    // Function to close the Thank You popup
    function closePopup() {
      document.getElementById("thankYouPopup").style.display = "none";
    }

    // Function to show Food Suggestions
    function showFoodSuggestions() {
      document.getElementById("foodContent").style.display = "block";
      document.getElementById("exerciseContent").style.display = "none";
    }

    // Function to show Exercise Suggestions
    function showExerciseSuggestions() {
      document.getElementById("exerciseContent").style.display = "block";
      document.getElementById("foodContent").style.display = "none";
    }
  </script>

</body>
</html> 

📥 How to Use the Mobile App

Locate the APK File: Navigate to the android folder inside the HealthyMe directory.

Upload to Drive: Upload the APK file to your Google Drive. ☁️

Download: Access the file on your mobile and install it. 📲

Enjoy: Launch the app and start your journey to better health! 🎉

WEB APP LINK :https://healthyme.tiiny.site/

📝 Code Explanation

HTML:

Defines the structure of the app, including form inputs, buttons, and result sections.

Includes the BMI calculation form and suggestion containers.

CSS:

Styles the app with a gradient background, responsive design, and modern UI elements.

Provides hover effects for buttons and a visually appealing layout.

JavaScript:

Performs BMI calculations and determines suggestions based on the result.

Updates the UI dynamically, showing/hiding sections as needed.

Displays random motivational quotes from a predefined list.

🎯 Future Enhancements

Add user authentication for personalized tracking.

Include a feature to log and track BMI over time.

Expand suggestions to include sleep and hydration tips. 💡

🙌 Acknowledgments

CodePen for providing an interactive development environment.

Flaticon for high-quality icons.

Tiiny Host for easy web hosting.

Web Into App for converting the web app into a mobile app.

❤️ Connect

Have feedback or suggestions? Feel free to share them! Together, let's make HealthyMe even better. 🚀
