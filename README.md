<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Creative Portfolio</title>

    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&family=Poppins:wght@400;600&display=swap" rel="stylesheet">

    <!-- Font Awesome for Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    
    <!-- EmailJS Library -->
    <script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>

    <style>
        :root {
            --primary-color: #333;
            --secondary-color: #007BFF;
            --accent-color: #0056b3;
            --background-gradient-light: linear-gradient(135deg, #ff9a9e, #fad0c4, #fbc2eb, #a18cd1);
            --background-gradient-dark: linear-gradient(135deg, #2b5876, #4e4376, #2b5876, #4e4376);
            --text-color-light: #333;
            --text-color-dark: #f0f0f0;
            --card-bg-light: white;
            --card-bg-dark: #2d2d2d;
        }
        
        body {
            margin: 0;
            font-family: 'Poppins', sans-serif;
            background: var(--background-gradient-light);
            background-size: 400% 400%;
            animation: gradientBG 10s ease infinite;
            color: var(--text-color-light);
            transition: all 0.5s ease;
        }

        body.dark-mode {
            background: var(--background-gradient-dark);
            color: var(--text-color-dark);
        }

        body.dark-mode .card,
        body.dark-mode .certificate-card,
        body.dark-mode .about-card,
        body.dark-mode .testimonial-card {
            background-color: var(--card-bg-dark);
            color: var(--text-color-dark);
        }

        body.dark-mode h1,
        body.dark-mode .project-title,
        body.dark-mode .certificate-title,
        body.dark-mode .about-card h3 {
            color: #f0f0f0;
        }

        body.dark-mode .project-description,
        body.dark-mode .testimonial-text {
            color: #ccc;
        }

        @keyframes gradientBG {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px;
            background-color: rgba(0, 0, 0, 0.5);
            color: white;
            position: sticky;
            top: 0;
            z-index: 1000;
        }
        @keyframes slideInLeft {
            from {
                transform: translateX(-100%);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }

        header h2 {
            animation: slideInLeft 1s ease-out;
        }

        @keyframes typing {
            from {
                width: 0;
            }
            to {
                width: 100%;
            }
        }

        @keyframes blink {
            50% {
                border-color: transparent;
            }
        }

        .about-text {
            font-family: 'Poppins', sans-serif;
            font-size: 1.2em;
            color: #5c5c5c;
            width: 80ch; /* Increased width to accommodate more text */
            overflow: hidden;
            line-height: 1.6;
            margin-bottom: 20px;
        }

        body.dark-mode .about-text {
            color: #d0d0d0;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .skills .card {
            animation: fadeIn 1s ease-in-out both;
        }

        html {
            scroll-behavior: smooth;
        }

        .menu {
            display: flex;
            gap: 15px;
        }

        .menu a {
            text-decoration: none;
            color: white;
            font-weight: bold;
            padding: 8px 12px;
            border-radius: 20px;
            transition: all 0.3s;
        }

        .menu a:hover {
            background-color: white;
            color: black;
        }

        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
            100% { transform: translateY(0px); }
        }

        .profile-photo {
            animation: float 3s ease-in-out infinite;
        }

        .chat-btn {
            position: fixed;
            bottom: 30px;
            right: 30px;
            background: #2196F3;
            padding: 15px 25px;
            border-radius: 30px;
            cursor: pointer;
            box-shadow: 0 4px 6px rgba(0,0,0,0.2);
            animation: pulse 2s infinite;
            z-index: 999;
            color: white;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        .chat-modal {
            position: fixed;
            bottom: 100px;
            right: 30px;
            width: 300px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            display: none;
            z-index: 1000;
            transform: translateY(100%);
            transition: transform 0.3s ease-out;
        }
        
        .chat-modal.active {
            display: block;
            transform: translateY(0);
        }
        
        .chat-header {
            padding: 10px 15px;
            background: #2196F3;
            color: white;
            border-radius: 10px 10px 0 0;
            display: flex;
            justify-content: space-between;
        }
        
        .close-chat {
            cursor: pointer;
            font-size: 20px;
        }
        
        .chat-messages {
            height: 250px;
            padding: 15px;
            overflow-y: auto;
        }
        
        .user-msg, .bot-msg {
            padding: 8px 12px;
            margin-bottom: 10px;
            border-radius: 15px;
            max-width: 80%;
        }
        
        .user-msg {
            background: #e1ffc7;
            margin-left: auto;
        }
        
        .bot-msg {
            background: #f0f0f0;
        }
        
        .chat-input {
            display: flex;
            padding: 10px;
            border-top: 1px solid #eee;
        }
        
        .chat-input input {
            flex: 1;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 20px;
            margin-right: 10px;
        }
        
        .chat-input button {
            background: #2196F3;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 20px;
            cursor: pointer;
        }

        @keyframes slideUp {
            from { opacity: 0; transform: translateY(50px); }
            to { opacity: 1; transform: translateY(0); }
        }

        section {
            opacity: 0;
            transition: opacity 0.5s, transform 0.5s;
        }

        section.visible {
            opacity: 1;
            animation: slideUp 0.8s ease-out;
        }

        .toggle-bar {
            font-size: 1.5em;
            color: white;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .toggle-bar:hover {
            transform: rotate(30deg);
        }

        section {
            padding: 50px 20px;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            text-align: center;
        }

        section h1 {
            margin-bottom: 30px;
            font-size: 2.5em;
            color: #4e4e4e;
            text-transform: uppercase;
            letter-spacing: 2px;
            position: relative;
            padding-bottom: 15px;
        }

        section h1::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 60px;
            height: 4px;
            background-color: var(--secondary-color);
            border-radius: 2px;
        }

        section p {
            max-width: 800px;
            font-size: 1.2em;
            line-height: 1.8;
            color: #5c5c5c;
        }

        body.dark-mode section p {
            color: #d0d0d0;
        }

        .profile-photo {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            overflow: hidden;
            margin: 20px 0;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
        }

        .profile-photo img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        /* Updated Skills Section */
        .skills-container {
            width: 100%;
            max-width: 900px;
            margin: 0 auto;
        }

        .skills {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 40px;
            width: 100%;
        }

        .skills .card {
            height: 120px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: white;
            border-radius: 15px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            font-size: 1.2em;
            font-weight: bold;
            transition: transform 0.3s, box-shadow 0.3s;
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }

        .skills .card:hover {
            transform: translateY(-10px);
            box-shadow: 0 8px 12px rgba(0, 0, 0, 0.2);
        }

        .skills .card::before {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 4px;
            background: var(--secondary-color);
        }

        .progress-bars {
            width: 100%;
        }

        .progress-bar-container {
            width: 100%;
            background: #e0e0e0;
            border-radius: 10px;
            margin: 15px 0;
            overflow: hidden;
            position: relative;
            height: 25px;
        }

        .progress-bar {
            height: 100%;
            border-radius: 10px;
            text-align: left;
            padding-left: 15px;
            line-height: 25px;
            color: white;
            font-weight: bold;
            position: relative;
            transition: width 1.5s ease-in-out;
        }

        .progress-bar span {
            position: absolute;
            right: 15px;
        }

        .certificates, .projects {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 25px;
            width: 100%;
            max-width: 900px;
            margin: 30px auto;
        }

        .card {
            width: 100%;
            height: 150px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: white;
            border-radius: 15px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            font-size: 1em;
            font-weight: bold;
            transition: transform 0.3s, box-shadow 0.3s;
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }

        .card:hover {
            transform: translateY(-10px);
            box-shadow: 0 8px 12px rgba(0, 0, 0, 0.2);
        }

        footer {
            text-align: center;
            padding: 20px;
            background-color: rgba(0, 0, 0, 0.5);
            color: white;
            margin-top: 50px;
        }

        .contact-link {
            color: #007BFF;
            text-decoration: none;
            font-weight: bold;
            transition: color 0.3s;
        }

        .contact-link:hover {
            color: #0056b3;
        }

        .contact-links a {
            display: inline-block;
            margin: 10px;
            padding: 10px 20px;
            background: var(--secondary-color);
            color: white;
            text-decoration: none;
            border-radius: 5px;
            transition: background 0.3s ease;
        }

        .contact-links a:hover {
            background: var(--accent-color);
        }
        
        /* Contact Form Styles */
        #contact-form {
            max-width: 500px;
            width: 100%;
            margin: 0 auto 30px;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        #contact-form input,
        #contact-form textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-family: 'Poppins', sans-serif;
            transition: border-color 0.3s;
        }

        #contact-form input:focus,
        #contact-form textarea:focus {
            border-color: var(--secondary-color);
            outline: none;
        }
        
        #contact-form textarea {
            min-height: 150px;
            resize: vertical;
        }
        
        #contact-form button {
            background: var(--secondary-color);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 5px;
            cursor: pointer;
            font-family: 'Poppins', sans-serif;
            transition: background 0.3s;
            font-weight: bold;
        }
        
        #contact-form button:hover {
            background: var(--accent-color);
        }
        
        #form-status {
            margin-top: 15px;
            font-weight: bold;
            padding: 10px;
            border-radius: 5px;
            display: none;
        }

        #form-status.success {
            background-color: rgba(76, 175, 80, 0.2);
            color: #2e7d32;
            border: 1px solid #2e7d32;
            display: block;
        }

        #form-status.error {
            background-color: rgba(244, 67, 54, 0.2);
            color: #c62828;
            border: 1px solid #c62828;
            display: block;
        }

        /* Updated styles for projects */
        .project-card {
            width: 100%;
            height: 300px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .project-card .project-title {
            font-size: 1.2em;
            font-weight: bold;
            margin-bottom: 10px;
        }

        .project-card .project-content {
            padding: 15px;
            display: flex;
            flex-direction: column;
            height: 100%;
            justify-content: space-between;
        }

        .project-year {
            background: var(--secondary-color);
            color: white;
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 0.8em;
            display: inline-block;
            margin-top: 10px;
        }

        .project-description {
            font-size: 0.9em;
            line-height: 1.5;
            margin: 15px 0;
            color: #555;
            flex-grow: 1;
            overflow-y: auto;
            max-height: 150px;
            text-align: left;
        }

        /* Certificate card styles */
        .certificate-card {
            width: 100%;
            height: 180px;
            background: white;
            border-radius: 15px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            padding: 20px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            align-items: center;
            transition: transform 0.3s, box-shadow 0.3s;
        }

        .certificate-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 8px 12px rgba(0, 0, 0, 0.2);
        }

        .certificate-title {
            font-weight: bold;
            font-size: 1.1em;
            margin-bottom: 10px;
        }

        .certificate-buttons {
            display: flex;
            gap: 10px;
            margin-top: 15px;
        }

        .certificate-buttons button {
            padding: 8px 15px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.9em;
            transition: all 0.3s ease;
        }

        .view-btn {
            background: #4CAF50;
            color: white;
        }

        .upload-btn {
            background: #2196F3;
            color: white;
        }

        .view-btn:hover, .upload-btn:hover {
            opacity: 0.9;
            transform: scale(1.05);
        }

        /* Modal styles */
        .modal {
            display: none;
            position: fixed;
            z-index: 2000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0, 0, 0, 0.7);
        }

        .modal-content {
            background-color: #fefefe;
            margin: 10% auto;
            padding: 20px;
            border: 1px solid #888;
            border-radius: 10px;
            width: 80%;
            max-width: 700px;
            animation: modalFadeIn 0.3s;
        }

        @keyframes modalFadeIn {
            from {opacity: 0; transform: translateY(-50px);}
            to {opacity: 1; transform: translateY(0);}
        }

        .close-modal {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
        }

        .close-modal:hover {
            color: #000;
        }

        .certificate-preview {
            max-width: 100%;
            max-height: 400px;
            display: block;
            margin: 20px auto;
            border: 1px solid #ddd;
        }

        .file-upload-container {
            margin: 20px 0;
            text-align: center;
        }

        .motivational-quote-btn {
            position: fixed;
            top: 100px;
            right: 20px;
            background: #FF9800;
            color: white;
            padding: 15px 25px;
            border-radius: 5px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            cursor: pointer;
            font-weight: bold;
            z-index: 100;
            transition: all 0.3s ease;
        }

        .motivational-quote-btn:hover {
            background: #F57C00;
            transform: translateY(-5px);
            box-shadow: 0 6px 10px rgba(0,0,0,0.2);
        }

        /* Quote modal styling */
        #quote-modal .modal-content {
            text-align: center;
            padding: 40px;
        }

        .quote-text {
            font-size: 24px;
            line-height: 1.5;
            font-style: italic;
            margin-bottom: 20px;
            color: #333;
        }

        .quote-author {
            font-weight: bold;
            color: #666;
            font-size: 18px;
        }

        .next-quote-btn {
            margin-top: 30px;
            background: #FF9800;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            transition: all 0.3s ease;
        }

        .next-quote-btn:hover {
            background: #F57C00;
        }

        /* About me extended styling */
        .about-section {
            display: flex;
            flex-direction: column;
            align-items: center;
            max-width: 900px;
            margin: 0 auto;
        }

        .about-details {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 20px;
            margin-top: 30px;
        }

        .about-card {
            background: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            width: 250px;
            text-align: left;
            transition: all 0.3s;
        }

        .about-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 8px 15px rgba(0,0,0,0.2);
        }

        .about-card h3 {
            color: var(--secondary-color);
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .about-card p {
            font-size: 0.95em;
            line-height: 1.6;
        }

        .about-card i {
            font-size: 2em;
            color: var(--secondary-color);
            margin-bottom: 15px;
        }

        /* Testimonials Section */
        .testimonials-container {
            max-width: 900px;
            width: 100%;
            margin: 0 auto;
        }

        .testimonials {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 25px;
            width: 100%;
        }

        .testimonial-card {
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            position: relative;
            transition: all 0.3s ease;
            text-align: left;
        }

        .testimonial-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 8px 16px rgba(0,0,0,0.1);
        }

        .testimonial-card::before {
            content: '❝';
            position: absolute;
            top: 15px;
            left: 15px;
            font-size: 2.5em;
            color: rgba(0, 123, 255, 0.2);
            line-height: 1;
        }

        .testimonial-text {
            font-size: 0.95em;
            line-height: 1.6;
            margin-bottom: 20px;
            color: #555;
            padding-top: 20px;
        }

        .testimonial-author {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .testimonial-author-img {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            object-fit: cover;
        }

        .testimonial-author-info {
            display: flex;
            flex-direction: column;
        }

        .testimonial-author-name {
            font-weight: bold;
            font-size: 1em;
        }

        .testimonial-author-title {
            font-size: 0.8em;
            color: #666;
        }

        .testimonial-stars {
            color: #FFD700;
            font-size: 1.2em;
            margin-top: 5px;
        }
    </style>
</head>
<body>
    <header>
        <h2>My Portfolio</h2>
        <nav class="menu">
            <a href="#about">About Me</a>
            <a href="#skills">Skills</a>
            <a href="#certificates">Certificates</a>
            <a href="#projects">Projects</a>
            <a href="#testimonials">Testimonials</a>
            <a href="#contact">Contact</a>
        </nav>
        <i class="fas fa-adjust toggle-bar" id="toggle-theme"></i>
    </header>
    
    <!-- Chat button and modal -->
    <div class="chat-btn" onclick="toggleChat()">💬 Let's Talk</div>

    <!-- Motivational Quote Button (Renamed from Free Quote) -->
    <div class="motivational-quote-btn" onclick="openQuoteModal()">🚀 Motivational Quotes</div>

    <div id="chat-modal" class="chat-modal">
        <div class="chat-header">
            <h3>Chat with Me</h3>
            <span class="close-chat" onclick="toggleChat()">×</span>
        </div>
        <div class="chat-messages" id="chat-messages"></div>
        <div class="chat-input">
            <input type="text" id="chat-input" placeholder="Type your message...">
            <button onclick="sendMessage()">Send</button>
        </div>
    </div>

    <!-- Quote Modal (Changed to display motivational quotes) -->
    <div id="quote-modal" class="modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeQuoteModal()">&times;</span>
            <h2>Business Motivational Quote</h2>
            <div class="quote-text" id="quote-text">
                "The best way to predict the future is to create it."
            </div>
            <div class="quote-author" id="quote-author">
                - Peter Drucker
            </div>
            <button class="next-quote-btn" onclick="showNextQuote()">Next Quote</button>
        </div>
    </div>

    <!-- Certificate View Modal -->
    <div id="certificate-modal" class="modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeCertificateModal()">&times;</span>
            <h2 id="certificate-modal-title">Certificate</h2>
            <img id="certificate-preview" class="certificate-preview" src="" alt="Certificate Preview">
        </div>
    </div>

    <!-- Certificate Upload Modal -->
    <div id="upload-modal" class="modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeUploadModal()">&times;</span>
            <h2 id="upload-modal-title">Upload Certificate</h2>
            <div class="file-upload-container">
                <input type="file" id="certificate-file" accept="image/*,.pdf">
                <p>Supported formats: JPG, PNG, PDF</p>
            </div>
            <button onclick="uploadCertificate()">Upload</button>
            <p id="upload-status"></p>
        </div>
    </div>

    <!-- Project Details Modal -->
    <div id="project-modal" class="modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeProjectModal()">&times;</span>
            <h2 id="project-modal-title"></h2>
            <p id="project-modal-year"></p>
            <div id="project-modal-description"></div>
        </div>
    </div>

    <section id="about">
        <h1>About Me</h1>
        <div class="profile-photo">
            <img src="C:\Users\lenovo\Desktop\khathija.jpeg" alt="Your Photo">
        </div>
        <div class="about-section" id="heroText">
            <h2>About Me</h2>
            <p id="heroTextt" >
        I am a curious and driven individual with a deep interest in software development, artificial intelligence, and problem-solving. 
        At VIT Chennai, I have honed my skills in programming, teamwork, and leadership. My goal is to contribute to impactful projects 
        that push the boundaries of technology while empowering communities. I also enjoy exploring creative pursuits like writing blogs 
        and mentoring peers.
            </p>
    <!-- Language Selection -->

            <div style="margin-top: 20px;">
                <label for="languageSelect" style="font-size: 1rem; font-weight: bold;">Translate to:</label>
                <select id="languageSelect" style="padding: 10px; font-size: 1rem; border-radius: 5px;">
                    <option value="en">English</option>
                    <option value="es">Spanish</option>
                    <option value="fr">French</option>
                    <option value="de">German</option>
                    <option value="hi">Hindi</option>
                </select>
                <button id="translateButton" style="padding: 10px 20px; font-size: 1rem; background-color: var(--accent-color); color: white; border: none; border-radius: 5px; cursor: pointer;">
                    Translate
                </button>
                <label for="languageAboutSelect" style="font-size: 1rem; font-weight: bold;">Translate to:</label>
                <select id="languageAboutSelect" style="padding: 10px; font-size: 1rem; border-radius: 5px;">
                    <option value="en">English</option>
                    <option value="es">Spanish</option>
                    <option value="fr">French</option>
                    <option value="de">German</option>
                    <option value="hi">Hindi</option>
                </select>
                <button id="translateAboutButton" style="padding: 10px 20px; font-size: 1rem; background-color: var(--accent-color); color: white; border: none; border-radius: 5px; cursor: pointer;">
                    Translate
                </button>

            </div>
            <div class="about-details">
                <div class="about-card">
                    <i class="fas fa-graduation-cap"></i>
                    <h3>Education</h3>
                    <p>2nd Year student in Computer Science Engineering in Artificial Intelligence</p>
                </div>
                <div class="about-card">
                    <i class="fas fa-briefcase"></i>
                    <h3>Experience</h3>
                    <p>1+ years in AI & Machine Learning projects</p>
                </div>
                <div class="about-card">
                    <i class="fas fa-map-marker-alt"></i>
                    <h3>Location</h3>
                    <p>Based in India ,Tamil Nadu Chennai</p>
                </div>
                <div class="about-card">
                    <i class="fas fa-heart"></i>
                    <h3>Interests</h3>
                    <p>Travel, Photography, Swimming, Hiking, Reading tech blogs</p>
                </div>
            </div>
        </div>
    </section>

    <section id="skills" class="skills-section">
        <h1>My Skills</h1>
        <div class="skills-container">
            <h2>Technical Skills</h2>
            <div class="skills">
                <div class="card">HTML5 & CSS3</div>
                <div class="card">JavaScript & TypeScript</div>
                <div class="card">React & Vue.js</div>
                <div class="card">Python</div>
            </div>
            
            <h2>Proficiency Levels</h2>
            <div class="progress-bars">
                <div class="progress-bar-container">
                    <div class="progress-bar" style="width: 95%; background-color: #4CAF50;">
                        Front-End Development <span>95%</span>
                    </div>
                </div>
                <div class="progress-bar-container">
                    <div class="progress-bar" style="width: 90%; background-color: #2196F3;">
                        Back-End Development <span>90%</span>
                    </div>
                </div>
                <div class="progress-bar-container">
                    <div class="progress-bar" style="width: 85%; background-color: #FF9800;">
                        Mobile App Development <span>85%</span>
                    </div>
                </div>
                <div class="progress-bar-container">
                    <div class="progress-bar" style="width: 80%; background-color: #9C27B0;">
                        AI & Machine Learning <span>80%</span>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section id="certificates">
        <h1>Certificates</h1>
        <div class="certificates">
            <div class="certificate-card">
                <div class="certificate-title">AWS Certified Solutions</div>
                <p>Amazon Web Services - 2023</p>
                <div class="certificate-buttons">
                    <button class="view-btn" onclick="viewCertificate('AWS Certified Solutions Architect')">View</button>
                </div>
            </div>
            <div class="certificate-card">
                <div class="certificate-title">Full Stack Web Development</div>
                <p>Udemy - 2022</p>
                <div class="certificate-buttons">
                    <button class="view-btn" onclick="viewCertificate('Full Stack Web Development')">View</button>
                </div>
            </div>
            <div class="certificate-card">
                <div class="certificate-title">Artificial Intelligence Specialization</div>
                <p>Coursera - 2023</p>
                <div class="certificate-buttons">
                    <button class="view-btn" onclick="viewCertificate('Machine Learning Specialization')">View</button>
                </div>
            </div>
        </div>
    </section>

    <section id="projects">
        <h1>Projects</h1>
        <div class="projects">
            <div class="card project-card" onclick="openProjectModal('AI-Powered Customer Service Bot', '2023', 'Developed a natural language processing chatbot that handles customer inquiries with 92% accuracy. Integrated with multiple CRM systems and reduced customer service wait times by 45%. Used Python, TensorFlow, and deployed on AWS.')">
                <div class="project-content">
                    <div class="project-title">AI-Powered Customer Service Bot</div>
                    <div class="project-description">Developed a natural language processing chatbot that handles customer inquiries with 92% accuracy...</div>
                    <div class="project-year">2023</div>
                </div>
            </div>
            <div class="card project-card" onclick="openProjectModal('E-commerce Platform Redesign', '2022', 'Led the complete redesign of an e-commerce platform serving 50,000+ monthly users. Implemented responsive design principles and optimized for performance, resulting in 30% faster page loads and 25% increase in conversion rates. Tech stack: React, Node.js, MongoDB, AWS.')">
                <div class="project-content">
                    <div class="project-title">E-commerce Platform Redesign</div>
                    <div class="project-description">Led the complete redesign of an e-commerce platform serving 50,000+ monthly users...</div>
                    <div class="project-year">2022</div>
                </div>
            </div>
            <div class="card project-card" onclick="openProjectModal('Financial Data Analytics Dashboard', '2022', 'Created a real-time financial data visualization dashboard for investment analysts. Implemented complex data filtering and custom visualizations that process over 1M data points daily. Used React, D3.js, Node.js, and time-series databases.')">
                <div class="project-content">
                    <div class="project-title">Financial Data Analytics Dashboard</div>
                    <div class="project-description">Created a real-time financial data visualization dashboard for investment analysts...</div>
                    <div class="project-year">2022</div>
                </div>
            </div>
        </div>
    </section>

    <section id="testimonials">
        <h1>Testimonials</h1>
        <div class="testimonials-container">
            <div class="testimonials">
                <div class="testimonial-card">
                    <div class="testimonial-text">
                        "Khathija is an exceptional developer who consistently delivered beyond our expectations. Her technical skills are matched by her problem-solving abilities and attention to detail."
                    </div>
                    <div class="testimonial-author">
                        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQTWEiBurJ9JnOykCtPZ9Fo0QSaAFbeS15tVg&s" alt="client" class="testimonial-author-img">
                        <div class="testimonial-author-info">
                            <div class="testimonial-author-name">Krishna arya</div>
                            <div class="testimonial-author-title">Professor,VIT Chennai</div>
                            <div class="testimonial-stars">★★★★★</div>
                        </div>
                    </div>
                </div>
                <div class="testimonial-card">
                    <div class="testimonial-text">
                        "Working with Khathija was a game-changer for our startup. She quickly understood our vision and translated it into a beautiful, functional product that our users love."
                    </div>
                    <div class="testimonial-author">
                        <img src="https://img.freepik.com/premium-vector/businesswoman-avatar-cartoon-character-profile_18591-50143.jpg" alt="client" class="testimonial-author-img">
                        <div class="testimonial-author-info">
                            <div class="testimonial-author-name">Sarah Johnson</div>
                            <div class="testimonial-author-title">3rd Year Student, VIT Chennai</div>
                            <div class="testimonial-stars">★★★★</div>
                        </div>
                    </div>
                </div>
                <div class="testimonial-card">
                    <div class="testimonial-text">
                        "Khathija's expertise in AI and machine learning helped us implement features we didn't think were possible within our timeline and budget. Highly recommended for complex technical projects."
                    </div>
                    <div class="testimonial-author">
                        <img src="https://cdn3.vectorstock.com/i/1000x1000/62/87/young-woman-profile-cartoon-vector-19116287.jpg" alt="client" class="testimonial-author-img">
                        <div class="testimonial-author-info">
                            <div class="testimonial-author-name">Rishika Cilji</div>
                            <div class="testimonial-author-title">2nd Year Student, VIT Chennai</div>
                            <div class="testimonial-stars">★★★★★</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section id="contact">
        <h1>Contact Me</h1>
        <p>Interested in working together? Feel free to reach out using the form below or through any of my social channels.</p>
        
        <form id="contact-form">
            <div class="form-group">
                <input type="text" id="name" name="name" placeholder="Your Name" required>
            </div>
            <div class="form-group">
                <input type="email" id="email" name="email" placeholder="Your Email" required>
            </div>
            <div class="form-group">
                <input type="text" id="subject" name="subject" placeholder="Subject">
            </div>
            <div class="form-group">
                <textarea id="message" name="message" placeholder="Your Message" required></textarea>
            </div>
            <button type="submit">Send Message</button>
        </form>
        
        <div id="form-status"></div>
        
        <div class="contact-links">
            <a href="https://linkedin.com/" target="_blank"><i class="fab fa-linkedin"></i> LinkedIn</a>
            <a href="https://github.com/" target="_blank"><i class="fab fa-github"></i> GitHub</a>
            <a href="mailto:khathija@example.com"><i class="fas fa-envelope"></i> Email</a>
            <a href="tel:+1234567890"><i class="fas fa-phone"></i> Call</a>
        </div>
    </section>

    <footer>
        <p>&copy; 2025 Khathija Idris. All rights reserved.</p>
    </footer>

    <script>
        // Toggle theme between light and dark
        document.getElementById('toggle-theme').addEventListener('click', function() {
            document.body.classList.toggle('dark-mode');
        });

        // Intersection Observer for scroll animations
        const sections = document.querySelectorAll('section');
        const observer = new IntersectionObserver(entries => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('visible');
                }
            });
        }, { threshold: 0.1 });

        sections.forEach(section => {
            observer.observe(section);
        });

        // Chat functionality
        function toggleChat() {
            const chatModal = document.getElementById('chat-modal');
            chatModal.classList.toggle('active');
            
            if (chatModal.classList.contains('active') && document.getElementById('chat-messages').children.length === 0) {
                // Add welcome message
                const botMsg = document.createElement('div');
                botMsg.className = 'bot-msg';
                botMsg.textContent = "Hi there! I'm Khathija's virtual assistant. How can I help you today?";
                document.getElementById('chat-messages').appendChild(botMsg);
            }
        }

        function sendMessage() {
            const input = document.getElementById('chat-input');
            const message = input.value.trim();
            
            if (message) {
                // Add user message
                const userMsg = document.createElement('div');
                userMsg.className = 'user-msg';
                userMsg.textContent = message;
                document.getElementById('chat-messages').appendChild(userMsg);
                
                // Clear input
                input.value = '';
                
                // Auto reply (in real implementation, this would be more sophisticated)
                setTimeout(() => {
                    const botMsg = document.createElement('div');
                    botMsg.className = 'bot-msg';
                    
                    // Simple pattern matching for responses
                    if (message.toLowerCase().includes('hello') || message.toLowerCase().includes('hi')) {
                        botMsg.textContent = "Hello! How can I assist you today?";
                    } else if (message.toLowerCase().includes('contact') || message.toLowerCase().includes('hire')) {
                        botMsg.textContent = "You can contact Khathija via the contact form below or directly at khathija@example.com";
                    } else if (message.toLowerCase().includes('project') || message.toLowerCase().includes('work')) {
                        botMsg.textContent = "Khathija has worked on various projects including AI chatbots, e-commerce platforms, and mobile apps. Would you like specific details about any of these?";
                    } else {
                        botMsg.textContent = "Thanks for your message! Khathija will get back to you soon. If you need immediate assistance, please email directly.";
                    }
                    
                    document.getElementById('chat-messages').appendChild(botMsg);
                    
                    // Scroll to bottom
                    const chatMessages = document.getElementById('chat-messages');
                    chatMessages.scrollTop = chatMessages.scrollHeight;
                }, 800);
            }
        }

        // Enter key in chat input
        document.getElementById('chat-input').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                sendMessage();
            }
        });

        // Certificate modal functions
        function viewCertificate(title) {
            document.getElementById('certificate-modal-title').textContent = title;
            // In a real implementation, this would fetch the actual certificate image
            document.getElementById('certificate-preview').src = "C:\\Users\\lenovo\\Desktop\\ChatGPT Image Apr 3, 2025, 01_44_01 PM.png";
            document.getElementById('certificate-modal').style.display = 'block';
        }
        
        function closeCertificateModal() {
            document.getElementById('certificate-modal').style.display = 'none';
        }
        
        function openUploadModal(title) {
            document.getElementById('upload-modal-title').textContent = `Upload ${title}`;
            document.getElementById('upload-modal').style.display = 'block';
        }
        
        function closeUploadModal() {
            document.getElementById('upload-modal').style.display = 'none';
        }
        
        function uploadCertificate() {
            const fileInput = document.getElementById('certificate-file');
            if (fileInput.files.length > 0) {
                // In a real implementation, this would handle the file upload
                document.getElementById('upload-status').textContent = 'Upload successful!';
                document.getElementById('upload-status').style.color = 'green';
                
                // Reset after a delay
                setTimeout(() => {
                    document.getElementById('upload-status').textContent = '';
                    closeUploadModal();
                }, 2000);
            } else {
                document.getElementById('upload-status').textContent = 'Please select a file first.';
                document.getElementById('upload-status').style.color = 'red';
            }
        }

        // Project modal functions
        function openProjectModal(title, year, description) {
            document.getElementById('project-modal-title').textContent = title;
            document.getElementById('project-modal-year').textContent = `Year: ${year}`;
            document.getElementById('project-modal-description').textContent = description;
            document.getElementById('project-modal').style.display = 'block';
        }
        
        function closeProjectModal() {
            document.getElementById('project-modal').style.display = 'none';
        }

        // Quote modal functions
        const quotes = [
            { text: "The best way to predict the future is to create it.", author: "Peter Drucker" },
            { text: "Your work is going to fill a large part of your life, and the only way to be truly satisfied is to do what you believe is great work.", author: "Steve Jobs" },
            { text: "Don't watch the clock; do what it does. Keep going.", author: "Sam Levenson" },
            { text: "Success is not the key to happiness. Happiness is the key to success. If you love what you are doing, you will be successful.", author: "Albert Schweitzer" },
            { text: "The only place where success comes before work is in the dictionary.", author: "Vidal Sassoon" }
        ];
        
        let currentQuoteIndex = 0;
        
        function openQuoteModal() {
            document.getElementById('quote-modal').style.display = 'block';
            showQuote(currentQuoteIndex);
        }
        
        function closeQuoteModal() {
            document.getElementById('quote-modal').style.display = 'none';
        }
        
        function showNextQuote() {
            currentQuoteIndex = (currentQuoteIndex + 1) % quotes.length;
            showQuote(currentQuoteIndex);
        }
        
        function showQuote(index) {
            document.getElementById('quote-text').textContent = quotes[index].text;
            document.getElementById('quote-author').textContent = "- " + quotes[index].author;
        }

        // Close modals with ESC key or clicking outside
        window.addEventListener('click', function(event) {
            if (event.target.classList.contains('modal')) {
                event.target.style.display = 'none';
            }
        });
        
        window.addEventListener('keydown', function(event) {
            if (event.key === 'Escape') {
                document.querySelectorAll('.modal').forEach(modal => {
                    modal.style.display = 'none';
                });
            }
        });

        // Contact form handling
        document.getElementById('contact-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const name = document.getElementById('name').value;
            const email = document.getElementById('email').value;
            const subject = document.getElementById('subject').value;
            const message = document.getElementById('message').value;
            
            // In a real implementation, this would use EmailJS or another service to send the email
            // For demonstration, we'll just show a success message
            
            const formStatus = document.getElementById('form-status');
            formStatus.textContent = `Thank you, ${name}! Your message has been sent successfully.`;
            formStatus.className = 'success';
            
            // Clear form
            document.getElementById('contact-form').reset();
            
            // Hide status after 5 seconds
            setTimeout(() => {
                formStatus.style.display = 'none';
                formStatus.className = '';
            }, 5000);
        });
       
    const aboutMeTranslations = {
        en: "I am a curious and driven individual with a deep interest in software development, artificial intelligence, and problem-solving. At VIT Chennai, I have honed my skills in programming, teamwork, and leadership. My goal is to contribute to impactful projects that push the boundaries of technology while empowering communities. I also enjoy exploring creative pursuits like writing blogs and mentoring peers.",
        es: "Soy una persona curiosa y motivada con un profundo interés en el desarrollo de software, la inteligencia artificial y la resolución de problemas. En VIT Chennai, he perfeccionado mis habilidades en programación, trabajo en equipo y liderazgo. Mi objetivo es contribuir a proyectos impactantes que amplíen los límites de la tecnología mientras empoderan a las comunidades. También disfruto explorar actividades creativas como escribir blogs y asesorar a compañeros.",
        fr: "Je suis une personne curieuse et motivée avec un profond intérêt pour le développement de logiciels, l'intelligence artificielle et la résolution de problèmes. À VIT Chennai, j'ai perfectionné mes compétences en programmation, travail d'équipe et leadership. Mon objectif est de contribuer à des projets percutants qui repoussent les limites de la technologie tout en autonomisant les communautés. J'aime également explorer des activités créatives comme écrire des blogs et encadrer mes pairs.",
        de: "Ich bin eine neugierige und zielstrebige Person mit großem Interesse an Softwareentwicklung, künstlicher Intelligenz und Problemlösung. An der VIT Chennai habe ich meine Fähigkeiten in Programmierung, Teamarbeit und Führung weiterentwickelt. Mein Ziel ist es, zu wirkungsvollen Projekten beizutragen, die die Grenzen der Technologie erweitern und gleichzeitig Gemeinschaften stärken. Außerdem erkunde ich gerne kreative Tätigkeiten wie das Schreiben von Blogs und das Mentoring von Kollegen.",
        hi: "मैं एक जिज्ञासु और प्रेरित व्यक्ति हूं जिसे सॉफ़्टवेयर विकास, कृत्रिम बुद्धिमत्ता और समस्या-समाधान में गहरी रुचि है। वीआईटी चेन्नई में, मैंने प्रोग्रामिंग, टीमवर्क और नेतृत्व में अपनी क्षमताओं को निखारा है। मेरा लक्ष्य प्रभावशाली परियोजनाओं में योगदान देना है जो प्रौद्योगिकी की सीमाओं को आगे बढ़ाते हुए समुदायों को सशक्त बनाती हैं। मुझे ब्लॉग लिखने और सहकर्मियों का मार्गदर्शन करने जैसे रचनात्मक कार्यों का भी आनंद मिलता है।"
    };

    document.getElementById("translateButton").addEventListener("click", function () {
        const selectedLanguage = document.getElementById("languageSelect").value;
        const heroTextt = document.getElementById("heroTextt");
        
        // Update text based on selected language
        if (aboutMeTranslations[selectedLanguage]) {
            heroTextt.innerText = aboutMeTranslations[selectedLanguage];
        } else {
            heroTextt.innerText = aboutMeTranslations["en"]; // Default to English if no translation is found
        }
    });
    const translationss = {
        en: {
            heroTitle: "Welcome to My Portfolio",
            heroText: "Hi, I'm Aiyisha Idris, a CSE student at VIT Chennai passionate about technology and innovation.",
            aboutMeTitle: "About Me",
            aboutMeText:
                "I am a curious and driven individual with a deep interest in software development, artificial intelligence, and problem-solving. At VIT Chennai, I have honed my skills in programming, teamwork, and leadership. My goal is to contribute to impactful projects that push the boundaries of technology while empowering communities. I also enjoy exploring creative pursuits like writing blogs and mentoring peers.",
            certificatesTitle: "Certificates",
        },
        es: {
            heroTitle: "Bienvenido a Mi Portafolio",
            heroText: "Hola, soy Aiyisha Idris, una estudiante de CSE en VIT Chennai apasionada por la tecnología y la innovación.",
            aboutMeTitle: "Sobre Mí",
            aboutMeText:
                "Soy una persona curiosa y motivada con un profundo interés en el desarrollo de software, la inteligencia artificial y la resolución de problemas. En VIT Chennai, he perfeccionado mis habilidades en programación, trabajo en equipo y liderazgo. Mi objetivo es contribuir a proyectos impactantes que amplíen los límites de la tecnología mientras empoderan a las comunidades. También disfruto explorar actividades creativas como escribir blogs y asesorar a compañeros.",
            certificatesTitle: "Certificados",
        },
        fr: {
            heroTitle: "Bienvenue dans Mon Portfolio",
            heroText: "Bonjour, je suis Aiyisha Idris, une étudiante en CSE à VIT Chennai passionnée par la technologie et l'innovation.",
            aboutMeTitle: "À Propos de Moi",
            aboutMeText:
                "Je suis une personne curieuse et motivée avec un profond intérêt pour le développement de logiciels, l'intelligence artificielle et la résolution de problèmes. À VIT Chennai, j'ai perfectionné mes compétences en programmation, travail d'équipe et leadership. Mon objectif est de contribuer à des projets percutants qui repoussent les limites de la technologie tout en autonomisant les communautés. J'aime également explorer des activités créatives comme écrire des blogs et encadrer mes pairs.",
            certificatesTitle: "Certificats",
        },
        de: {
            heroTitle: "Willkommen in Meinem Portfolio",
            heroText:
                "Hallo, ich bin Aiyisha Idris, eine CSE-Studentin an der VIT Chennai, die sich für Technologie und Innovation begeistert.",
            aboutMeTitle: "Über Mich",
            aboutMeText:
                "Ich bin eine neugierige und zielstrebige Person mit großem Interesse an Softwareentwicklung, künstlicher Intelligenz und Problemlösung. An der VIT Chennai habe ich meine Fähigkeiten in Programmierung, Teamarbeit und Führung weiterentwickelt. Mein Ziel ist es, zu wirkungsvollen Projekten beizutragen, die die Grenzen der Technologie erweitern und gleichzeitig Gemeinschaften stärken. Außerdem erkunde ich gerne kreative Tätigkeiten wie das Schreiben von Blogs und das Mentoring von Kollegen.",
            certificatesTitle: "Zertifikate",
        },
        hi: {
            heroTitle: "मेरे पोर्टफोलियो में आपका स्वागत है",
            heroText:
                "नमस्ते, मैं अयिशा इदरीस हूं, वीआईटी चेन्नई में सीएसई की छात्रा हूं जो प्रौद्योगिकी और नवाचार के प्रति उत्साही है।",
            aboutMeTitle: "मेरे बारे में",
            aboutMeText:
                "मैं एक जिज्ञासु और प्रेरित व्यक्ति हूं जिसे सॉफ़्टवेयर विकास, कृत्रिम बुद्धिमत्ता और समस्या-समाधान में गहरी रुचि है। वीआईटी चेन्नई में, मैंने प्रोग्रामिंग, टीमवर्क और नेतृत्व में अपनी क्षमताओं को निखारा है। मेरा लक्ष्य प्रभावशाली परियोजनाओं में योगदान देना है जो प्रौद्योगिकी की सीमाओं को आगे बढ़ाते हुए समुदायों को सशक्त बनाती हैं। मुझे ब्लॉग लिखने और सहकर्मियों का मार्गदर्शन करने जैसे रचनात्मक कार्यों का भी आनंद मिलता है।",
            certificatesTitle: "प्रमाण पत्र",
        },
    };

    document.getElementById("translateAboutButton").addEventListener("click", function () {
        const selectedLanguagee = document.getElementById("languageAboutSelect").value;

        // Update Hero Section
        document.querySelector(".hero h1").innerText = translationss[selectedLanguagee].heroTitle;
        document.querySelector(".hero p").innerText = translationss[selectedLanguagee].heroText;

        // Update About Me Section
        document.querySelector("#aboutMeSection h2").innerText = translationss[selectedLanguagee].aboutMeTitle;
        document.querySelector("#aboutMeSection p").innerText = translationss[selectedLanguagee].aboutMeText;

        // Update Certificates Section
        document.querySelector(".certificates-section h2").innerText = translationss[selectedLanguagee].certificatesTitle;
    });
        


        // Initialize EmailJS in a real implementation
        // (function() {
        //     emailjs.init("YOUR_USER_ID");
        // })();
    </script>
</body>
</html>
