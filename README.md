# Assignment: Creating Interactive Elements and Form Validation

## Objective:
Build a functional webpage that incorporates event handling, interactive elements, and form validation using JavaScript.

## Requirements:

Interactive Button with onclick:

Add a button that toggles the background color of the webpage between two colors.
Slider with Real-Time Feedback (oninput):

Add a slider that adjusts the size of a paragraph text dynamically.
Modal with Event Listeners:

Create a modal that displays when a button is clicked and hides when the user clicks a close button.

## Form with Validation:

Include a form with the following fields:
Name (required, minimum 3 characters).
Email (valid email format).
Password (minimum 8 characters, at least one uppercase letter and one number).
Display error messages if validation fails.
Prevent form submission if there are errors.
Bonus (Optional):

Add a dropdown menu that displays a custom message when the selected option changes (onchange).

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Interactive Webpage</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      transition: background-color 0.5s;
    }
    #text-paragraph {
      font-size: 16px;
      transition: font-size 0.3s;
    }
    #modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.7);
      justify-content: center;
      align-items: center;
    }
    #modal-content {
      background: white;
      padding: 20px;
      border-radius: 5px;
      text-align: center;
    }
    .error {
      color: red;
      font-size: 14px;
    }
  </style>
</head>
<body>

  <!-- Interactive Button to Toggle Background Color -->
  <button onclick="toggleBackgroundColor()">Toggle Background Color</button>
  <br><br>

  <!-- Slider for Real-Time Text Size Adjustment -->
  <label for="fontSizeSlider">Adjust Text Size: </label>
  <input type="range" id="fontSizeSlider" min="10" max="50" value="16" oninput="adjustTextSize(this.value)">
  <span id="sliderValue">16px</span>
  <p id="text-paragraph">This text size can be adjusted using the slider.</p>
  <br><br>

  <!-- Modal Trigger Button -->
  <button onclick="openModal()">Open Modal</button>
  <div id="modal" onclick="closeModal()">
    <div id="modal-content" onclick="event.stopPropagation()">
      <p>This is a modal. Click the close button or outside the modal to close it.</p>
      <button onclick="closeModal()">Close Modal</button>
    </div>
  </div>
  <br><br>

  <!-- Form with Validation -->
  <form id="userForm" onsubmit="return validateForm()">
    <label for="name">Name (min 3 characters):</label>
    <input type="text" id="name" name="name" required>
    <span class="error" id="nameError"></span>
    <br><br>

    <label for="email">Email (valid format):</label>
    <input type="email" id="email" name="email" required>
    <span class="error" id="emailError"></span>
    <br><br>

    <label for="password">Password (min 8 characters, 1 uppercase, 1 number):</label>
    <input type="password" id="password" name="password" required>
    <span class="error" id="passwordError"></span>
    <br><br>

    <button type="submit">Submit Form</button>
  </form>
  <br><br>

  <!-- Bonus Dropdown Menu -->
  <label for="dropdown">Select an option:</label>
  <select id="dropdown" onchange="showDropdownMessage()">
    <option value="">Select...</option>
    <option value="Option 1">Option 1</option>
    <option value="Option 2">Option 2</option>
    <option value="Option 3">Option 3</option>
  </select>
  <p id="dropdownMessage"></p>

  <script>
    // Toggle background color between two colors
    let backgroundToggle = false;
    function toggleBackgroundColor() {
      document.body.style.backgroundColor = backgroundToggle ? 'white' : 'lightblue';
      backgroundToggle = !backgroundToggle;
    }

    // Adjust text size dynamically using the slider
    function adjustTextSize(value) {
      document.getElementById('text-paragraph').style.fontSize = value + 'px';
      document.getElementById('sliderValue').innerText = value + 'px';
    }

    // Open Modal
    function openModal() {
      document.getElementById('modal').style.display = 'flex';
    }

    // Close Modal
    function closeModal() {
      document.getElementById('modal').style.display = 'none';
    }

    // Form validation function
    function validateForm() {
      let valid = true;
      // Name validation
      let name = document.getElementById('name').value;
      let nameError = document.getElementById('nameError');
      if (name.length < 3) {
        nameError.innerText = 'Name must be at least 3 characters long.';
        valid = false;
      } else {
        nameError.innerText = '';
      }

      // Email validation
      let email = document.getElementById('email').value;
      let emailError = document.getElementById('emailError');
      let emailRegex = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}$/;
      if (!emailRegex.test(email)) {
        emailError.innerText = 'Please enter a valid email address.';
        valid = false;
      } else {
        emailError.innerText = '';
      }

      // Password validation
      let password = document.getElementById('password').value;
      let passwordError = document.getElementById('passwordError');
      let passwordRegex = /^(?=.*[A-Z])(?=.*\d).{8,}$/;
      if (!passwordRegex.test(password)) {
        passwordError.innerText = 'Password must be at least 8 characters, including 1 uppercase letter and 1 number.';
        valid = false;
      } else {
        passwordError.innerText = '';
      }

      return valid;
    }

    // Show message based on dropdown selection
    function showDropdownMessage() {
      let dropdownValue = document.getElementById('dropdown').value;
      let message = dropdownValue ? `You selected: ${dropdownValue}` : '';
      document.getElementById('dropdownMessage').innerText = message;
    }
  </script>

</body>
</html>
