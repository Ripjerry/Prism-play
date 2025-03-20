
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prism Play</title>
    <script src="https://unpkg.com/@tailwindcss/browser@4"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        /* Custom CSS for the color picker */
        #colorPicker {
            -webkit-appearance: none;
            -moz-appearance: none;
            appearance: none;
            width: 40px;
            height: 40px;
            border: none;
            cursor: pointer;
            border-radius: 50%;
            padding: 0;
        }
        #colorPicker::-webkit-color-swatch-wrapper {
            padding: 0;
        }
        #colorPicker::-webkit-color-swatch {
            border: none;
            border-radius: 50%;
        }
        #colorPicker::-moz-color-swatch-wrapper {
            padding: 0;
        }
        #colorPicker::-moz-color-swatch {
            border: none;
            border-radius: 50%;
        }
        #colorPicker:focus {
            outline: none;
            box-shadow: 0 0 0 2px rgba(0, 123, 255, 0.5); /* Add a subtle focus outline */
        }
        /* Style for the button */
        #gameButton {
            padding: 12px 24px;
            font-size: 18px;
            font-weight: 600;
            color: white;
            background-color: #007bff; /* Blue */
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: background-color 0.3s ease;
            margin-top: 20px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
        }
        #gameButton:hover {
            background-color: #0056b3; /* Darker blue */
        }
        #gameButton:active {
            background-color: #004080; /* Even darker blue */
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3); /* Smaller shadow */
            transform: translateY(2px);
        }
        .auth-button {
            padding: 10px 20px;
            font-size: 16px;
            font-weight: 600;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: background-color 0.3s ease;
            margin: 5px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        }
        .login-button {
            background-color: #28a745; /* Green */
        }
        .login-button:hover {
            background-color: #218838; /* Darker green */
        }
        .signup-button {
            background-color: #dc3545; /* Red */
        }
        .signup-button:hover {
            background-color: #c82333; /* Darker red */
        }
        /* Modal Styles */
        .modal {
            display: none; /* Hidden by default */
            position: fixed; /* Stay in place */
            z-index: 1000; /* Sit on top */
            left: 0;
            top: 0;
            width: 100%; /* Full width */
            height: 100%; /* Full height */
            overflow: auto; /* Enable scroll if needed */
            background-color: rgba(0,0,0,0.5); /* Black with opacity */
        }

        .modal-content {
            background-color: #fefefe;
            margin: 10% auto; /* 15% from the top and centered */
            padding: 20px;
            border: 1px solid #888;
            width: 90%; /* Could be more or less, depending on screen size */
            max-width: 500px; /* Maximum width */
            border-radius: 10px;
            position: relative; /* To position the close button */
            box-shadow: 0 4px 8px rgba(0,0,0,0.3);
            animation: fadeIn 0.3s; /* Add fade in animation */
        }

        /* Fade in Animation */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-50px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            position: absolute;
            top: 10px;
            right: 15px;
            cursor: pointer;
        }

        .close:hover,
        .close:focus {
            color: #000;
            text-decoration: none;
        }

        .modal-header {
            padding: 10px 20px;
            border-bottom: 1px solid #ddd;
        }

        .modal-header h2 {
            margin: 0;
            font-size: 24px;
        }

        .modal-body {
            padding: 20px;
        }

        .modal-body form {
            display: flex;
            flex-direction: column;
        }

        .modal-body form label {
            margin-bottom: 5px;
            font-weight: 600;
        }

        .modal-body form input {
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            transition: border-color 0.3s ease;
        }

        .modal-body form input:focus {
            outline: none;
            border-color: #007bff;
            box-shadow: 0 0 0 2px rgba(0, 123, 255, 0.25);
        }

        .modal-body form button {
            padding: 10px 20px;
            font-size: 16px;
            font-weight: 600;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: background-color 0.3s ease;
            margin-top: 10px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        }

        .modal-body form button.login {
            background-color: #28a745; /* Green */
        }

        .modal-body form button.login:hover {
            background-color: #218838; /* Darker green */
        }

        .modal-body form button.signup {
            background-color: #dc3545; /* Red */
        }

        .modal-body form button.signup:hover {
            background-color: #c82333; /* Darker red */
        }

        .modal-footer {
            padding: 10px 20px;
            border-top: 1px solid #ddd;
            text-align: right;
        }

        #headerImage {
            width: 50px; /* Adjust size as needed */
            height: 50px;
            border-radius: 50%; /* Make it a circle */
            object-fit: cover; /* Ensure image fills the circle */
            margin-right: 10px; /* Add some space to the right of the image */
        }
    </style>
</head>
<body class="bg-gradient-to-r from-blue-200 to-green-200 min-h-screen flex flex-col">
    <header class="bg-gradient-to-br from-purple-500 to-pink-500 text-white p-6 text-center shadow-md rounded-b-lg flex justify-between items-center">
        <div class="flex items-center">
            <img id="headerImage" src="image_628f81.png" alt="Profile Image">
            <h1 class="text-3xl font-semibold mb-2">Welcome to My Website</h1>
        </div>
        <input type="color" id="colorPicker" value="#007bff" title="Change the website color">
        <div>
            <button id="loginButton" class="auth-button login-button">Log In</button>
            <button id="signupButton" class="auth-button signup-button">Sign Up</button>
        </div>
    </header>

    <main class="container mx-auto py-10 flex-grow flex justify-center items-center flex-col">
        <div class="bg-white rounded-lg shadow-xl p-8 max-w-2xl text-center transition-transform hover:scale-105">
            <h2 class="text-2xl font-bold text-blue-700 mb-4">About Site</h2>
            <p class="text-gray-700 text-lg mb-6">
                Welcome to my website!  This site is a place where you can have fun experimenting with colors and interactivity. I'm learning web development and having fun creating things. I hope you enjoy it!
            </p>
            <a href="#contact" class="bg-gradient-to-r from-green-400 to-blue-500 hover:from-green-500 hover:to-blue-600 text-white font-semibold py-3 px-6 rounded-full transition-colors duration-300">
                Contact Me
            </a>
            <button id="gameButton">Click the button</button>
        </div>
    </main>

    <section id="contact" class="bg-gradient-to-tl from-yellow-400 to-orange-400 p-8 rounded-t-lg shadow-md text-center">
        <div class="container mx-auto">
            <h2 class="text-2xl font-semibold text-gray-800 mb-4">Contact Me</h2>
            <p class="text-gray-700 mb-6">
                Feel free to reach out to me through the following channels:
            </p>
            <ul class="list-none space-y-3">
                <li>
                    <a href="mailto:chikaimaezeoha@gmail.com" class="text-blue-600 hover:text-blue-800 transition-colors">
                        Email: chikaimaezeoha@gmail.com
                    </a>
                </li>
                <li>
                    <a href="https://github.com/Ripjerry" target="_blank" rel="noopener noreferrer" class="text-blue-600 hover:text-blue-800 transition-colors">
                        GitHub: Ripjerry
                    </a>
                </li>
                <li>
                    <a href="https://x.com/Jerry_YT234" target="_blank" rel="noopener noreferrer" class="text-blue-600 hover:text-blue-800 transition-colors flex items-center justify-center">
                        <img src="image_628f81.png" alt="X Logo" style="width: 20px; height: 20px; margin-right: 5px;">
                        Twitter: Jerry_YT234
                    </a>
                </li>
                 <li>
                    <a href="https://www.youtube.com/@rip_jerry13" target="_blank" rel="noopener noreferrer" class="text-blue-600 hover:text-blue-800 transition-colors">
                        YouTube: My Channel
                    </a>
                </li>
            </ul>
        </div>
    </section>

    <footer class="bg-gray-800 text-white text-center p-4 rounded-t-lg shadow-md">
        <p>© 2024 My Colorful Website. All rights reserved.</p>
    </footer>

    <div id="loginModal" class="modal">
        <div class="modal-content">
            <span class="close">×</span>
            <div class="modal-header">
                <h2>Log In</h2>
            </div>
            <div class="modal-body">
                <form id="loginForm">
                    <label for="loginEmail">Email:</label>
                    <input type="email" id="loginEmail" name="loginEmail" required>
                    <label for="loginPassword">Password:</label>
                    <input type="password" id="loginPassword" name="loginPassword" required>
                    <button type="submit" class="login">Log In</button>
                </form>
            </div>
            <div class="modal-footer">
                <p>Don't have an account? <a href="#" id="goToSignup">Sign Up</a></p>
            </div>
        </div>
    </div>

    <div id="signupModal" class="modal">
        <div class="modal-content">
            <span class="close">×</span>
            <div class="modal-header">
                <h2>Sign Up</h2>
            </div>
            <div class="modal-body">
                <form id="signupForm">
                    <label for="signupName">Name:</label>
                    <input type="text" id="signupName" name="signupName" required>
                    <label for="signupEmail">Email:</label>
                    <input type="email" id="signupEmail" name="signupEmail" required>
                    <label for="signupPassword">Password:</label>
                    <input type="password" id="signupPassword" name="signupPassword" required>
                    <button type="submit" class="signup">Sign Up</button>
                </form>
            </div>
            <div class="modal-footer">
                <p>Already have an account? <a href="#" id="goToLogin">Log In</a></p>
            </div>
        </div>
    </div>

    <script>
        const colorPicker = document.getElementById('colorPicker');
        const body = document.body;
        const header = document.querySelector('header');
        const main = document.querySelector('main');
        const contactSection = document.getElementById('contact');
        const footer = document.querySelector('footer');
        const gameButton = document.getElementById('gameButton');
        const loginButton = document.getElementById('loginButton');
        const signupButton = document.getElementById('signupButton');
        const loginModal = document.getElementById('loginModal');
        const signupModal = document.getElementById('signupModal');
        const closeBtns = document.querySelectorAll('.close');
        const goToLoginLink = document.getElementById('goToLogin');
        const goToSignupLink = document.getElementById('goToSignup');
        const loginForm = document.getElementById('loginForm');
        const signupForm = document.getElementById('signupForm');

        const colors = ['#ff0000', '#ff7f00', '#ffff00', '#00ff00', '#0000ff', '#4b0082', '#9400d3']; // Rainbow colors
        let colorIndex = 0;

        colorPicker.addEventListener('change', function() {
            const newColor = this.value;
            body.style.backgroundImage = `linear-gradient(to right, ${newColor}, ${getComplementaryColor(newColor)})`;
            header.style.backgroundImage = `linear-gradient(to bottom right, ${getLighterColor(newColor)}, ${getDarkerColor(newColor)})`;
            contactSection.style.backgroundImage = `linear-gradient(to top left, ${getLighterColor(newColor)}, ${getDarkerColor(newColor)})`;
            footer.style.backgroundColor = getDarkerColor(newColor);
             header.style.color = isDark(newColor) ? 'white' : 'black';
             main.style.color = isDark(newColor) ? 'white' : 'black';
             contactSection.style.color = isDark(newColor) ? 'white' : 'black';
             footer.style.color = isDark(newColor) ? 'white' : 'black';
        });

        function getComplementaryColor(hexcolor){
            hexcolor = hexcolor.replace("#","");
            let r = parseInt(hexcolor.substr(0,2),16);
            let g = parseInt(hexcolor.substr(2,2),16);
            let b = parseInt(hexcolor.substr(4,2),16);
            r = 255 - r;
            g = 255 - g;
            b = 255 - b;
            return "#" + componentToHex(r) + componentToHex(g) + componentToHex(b);
        }

        function componentToHex(c) {
            var hex = c.toString(16);
            return hex.length == 1 ? "0" + hex : hex;
        }

        function getLighterColor(hexcolor) {
            hexcolor = hexcolor.replace("#","");
            let r = parseInt(hexcolor.substr(0,2),16);
            let g = parseInt(hexcolor.substr(2,2),16);
            let b = parseInt(hexcolor.substr(4,2),16);

            r = Math.min(255, r + 50); //Lighten
            g = Math.min(255, g + 50);
            b = Math.min(255, b + 50);

            return "#" + componentToHex(r) + componentToHex(g) + componentToHex(b);
        }

        function getDarkerColor(hexcolor) {
            hexcolor = hexcolor.replace("#","");
            let r = parseInt(hexcolor.substr(0,2),16);
            let g = parseInt(hexcolor.substr(2,2),16);
            let b = parseInt(hexcolor.substr(4,2),16);

            r = Math.max(0, r - 50); //Darken
            g = Math.max(0, g - 50);
            b = Math.max(0, b - 50);

            return "#" + componentToHex(r) + componentToHex(g) + componentToHex(b);
        }

         function isDark(hexcolor) {
            hexcolor = hexcolor.replace("#","");
            const r = parseInt(hexcolor.substr(0,2),16);
            const g = parseInt(hexcolor.substr(2,2),16);
            const b = parseInt(hexcolor.substr(4,2),16);
            const luminance = 0.299 * r + 0.587 * g + 0.114 * b;
            return luminance < 128;
        }

        gameButton.addEventListener('click', function() {
            // Change the button's background color
            this.style.backgroundColor = colors[colorIndex];
            // Change the text color.  Make it black or white based on the background color.
            this.style.color = isDark(colors[colorIndex]) ? '#ffffff' : '#000000';
            // Increment the color index
            colorIndex = (colorIndex + 1) % colors.length;
            //Play a sound when the button is clicked.
            const audio = new Audio('https://www.soundjay.com/buttons/sounds/beep-01a.mp3');
            audio.play();
        });

        loginButton.addEventListener('click', () => {
            loginModal.style.display = "block";
        });

        signupButton.addEventListener('click', () => {
            signupModal.style.display = "block";
        });

        closeBtns.forEach(closeBtn => {
            closeBtn.addEventListener('click', () => {
                loginModal.style.display = "none";
                signupModal.style.display = "none";
            });
        });

        window.addEventListener('click', (event) => {
            if (event.target.classList.contains('modal')) {
                loginModal.style.display = "none";
                signupModal.style.display = "none";
            }
        });

        goToSignupLink.addEventListener('click', (event) => {
            event.preventDefault(); // Prevent default link behavior
            loginModal.style.display = "none"; // Hide login modal
            signupModal.style.display = "block"; // Show signup modal
        });

        goToLoginLink.addEventListener('click', (event) => {
            event.preventDefault(); // Prevent default link behavior
            signupModal.style.display = "none"; // Hide signup modal
            loginModal.style.display = "block"; // Show login modal
        });

        loginForm.addEventListener('submit', (event) => {
            event.preventDefault();
            const email = document.getElementById('loginEmail').value;
            const password = document.getElementById('loginPassword').value;
            // Here, you would typically send this data to a server for authentication
            if(email && password){
                alert(`Logging in with Email: ${email}, Password: ${password}`);
                loginModal.style.display = "none"; // Hide modal after submission
            }
            else{
                alert('Please enter your email and password');
            }

        });

        signupForm.addEventListener('submit', (event) => {
            event.preventDefault();
            const name = document.getElementById('signupName').value;
            const email = document.getElementById('signupEmail').value;
            const password = document.getElementById('signupPassword').value;
            // Here, you would typically send this data to a server for registration
            if (name && email && password) {
                 alert(`Signing up with Name: ${name}, Email: ${email}, Password: ${password}`);
                 signupModal.style.display = "none"; // Hide modal after submission
            }
            else{
                alert('Please enter your name, email and password');
            }

        });
    </script>
</body>
</html>
