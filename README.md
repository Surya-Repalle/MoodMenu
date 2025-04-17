# MoodMenu
 AI-Powered Emotional Dining Experiences
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MoodMenu - Emotional Dining Experiences</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f0f4f8;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            width: 100%;
            max-width: 500px;
            background-color: #ffffff;
            border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #6B46C1, #9F7AEA);
            color: white;
            padding: 20px;
            text-align: center;
            position: relative;
        }
        
        .logo {
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 10px;
        }
        
        .logo-text {
            font-size: 24px;
            font-weight: bold;
            margin-left: 10px;
        }
        
        .tagline {
            font-size: 14px;
            opacity: 0.9;
        }
        
        .chat-area {
            height: 400px;
            overflow-y: auto;
            padding: 20px;
            background-color: #f9fafc;
        }
        
        .message {
            padding: 12px 16px;
            margin-bottom: 12px;
            border-radius: 12px;
            max-width: 80%;
            animation: fadeIn 0.3s ease;
        }
        
        .bot {
            background-color: #EDF2F7;
            margin-right: auto;
            border-bottom-left-radius: 4px;
        }
        
        .user {
            background-color: #6B46C1;
            color: white;
            margin-left: auto;
            border-bottom-right-radius: 4px;
        }
        
        .input-area {
            display: flex;
            padding: 16px;
            background-color: white;
            border-top: 1px solid #E2E8F0;
        }
        
        .input-area input {
            flex: 1;
            padding: 12px 16px;
            border: 1px solid #E2E8F0;
            border-radius: 24px;
            outline: none;
            font-size: 14px;
        }
        
        .input-area input:focus {
            border-color: #9F7AEA;
        }
        
        .input-area button {
            background-color: #6B46C1;
            color: white;
            border: none;
            border-radius: 24px;
            padding: 12px 20px;
            margin-left: 10px;
            cursor: pointer;
            transition: background-color 0.2s;
        }
        
        .input-area button:hover {
            background-color: #553C9A;
        }
        
        .mood-indicators {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            padding: 10px;
            gap: 8px;
        }
        
        .mood-button {
            background-color: #EDF2F7;
            border: none;
            border-radius: 20px;
            padding: 8px 12px;
            font-size: 12px;
            cursor: pointer;
            transition: all 0.2s;
        }
        
        .mood-button:hover {
            background-color: #E9D8FD;
        }
        
        .typing-indicator {
            padding: 12px 16px;
            margin-bottom: 12px;
            border-radius: 12px;
            max-width: 80%;
            background-color: #EDF2F7;
            margin-right: auto;
            border-bottom-left-radius: 4px;
            display: none;
        }
        
        .typing-indicator span {
            display: inline-block;
            width: 8px;
            height: 8px;
            background-color: #9F7AEA;
            border-radius: 50%;
            animation: bounce 1s infinite;
            margin-right: 3px;
        }
        
        .typing-indicator span:nth-child(2) {
            animation-delay: 0.1s;
        }
        
        .typing-indicator span:nth-child(3) {
            animation-delay: 0.2s;
        }
        
        @keyframes bounce {
            0%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-8px); }
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .food-suggestion {
            background-color: #ffffff;
            border: 1px solid #E2E8F0;
            border-radius: 12px;
            padding: 15px;
            margin-top: 12px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }

        .food-title {
            font-weight: bold;
            color: #4A5568;
            margin-bottom: 5px;
        }

        .food-description {
            font-size: 14px;
            color: #718096;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <div class="logo">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M12 2L15.09 8.26L22 9.27L17 14.14L18.18 21.02L12 17.77L5.82 21.02L7 14.14L2 9.27L8.91 8.26L12 2Z" fill="white"/>
                </svg>
                <span class="logo-text">MoodMenu</span>
            </div>
            <div class="tagline">AI-Powered Emotional Dining Experiences</div>
        </div>
        <div class="mood-indicators">
            <button class="mood-button" onclick="sendMood('Happy')">😊 Happy</button>
            <button class="mood-button" onclick="sendMood('Stressed')">😰 Stressed</button>
            <button class="mood-button" onclick="sendMood('Sad')">😢 Sad</button>
            <button class="mood-button" onclick="sendMood('Energetic')">⚡ Energetic</button>
            <button class="mood-button" onclick="sendMood('Romantic')">❤️ Romantic</button>
            <button class="mood-button" onclick="sendMood('Need Focus')">🧠 Need Focus</button>
        </div>
        <div class="chat-area" id="chatArea">
            <div class="message bot">
                Hello! I'm MoodMenu, your emotional dining assistant. How are you feeling today? I can suggest foods that might complement or improve your mood.
            </div>
        </div>
        <div class="typing-indicator" id="typingIndicator">
            <span></span>
            <span></span>
            <span></span>
        </div>
        <div class="input-area">
            <input type="text" id="userInput" placeholder="Tell me how you're feeling or what you're craving..." onkeypress="handleKeyPress(event)">
            <button onclick="sendMessage()">Send</button>
        </div>
    </div>

    <script>
        // Food suggestions database organized by mood
        const foodSuggestions = {
            "happy": [
                {
                    title: "Mediterranean Platter",
                    description: "A vibrant spread of hummus, olives, fresh vegetables and pita bread. The healthy fats can help maintain your positive mood."
                },
                {
                    title: "Grilled Salmon with Mango Salsa",
                    description: "Omega-3 rich salmon topped with bright, tropical flavors to match your upbeat energy."
                },
                {
                    title: "Berry Parfait",
                    description: "Layers of antioxidant-rich berries, yogurt and granola to maintain your happy state with natural sweetness."
                }
            ],
            "sad": [
                {
                    title: "Dark Chocolate Avocado Mousse",
                    description: "Creamy, rich dessert that provides mood-boosting compounds from dark chocolate and healthy fats from avocado."
                },
                {
                    title: "Warm Chicken and Vegetable Soup",
                    description: "A comforting, nurturing bowl that provides protein and nutrients while soothing with familiar flavors."
                },
                {
                    title: "Turmeric Golden Milk",
                    description: "A warming drink with anti-inflammatory properties that can help ease both physical and emotional discomfort."
                }
            ],
            "stressed": [
                {
                    title: "Herbal Tea with Honey",
                    description: "Chamomile or lavender tea with a touch of honey can help activate calming neurotransmitters."
                },
                {
                    title: "Dark Leafy Green Salad with Walnuts",
                    description: "Magnesium-rich greens and omega-3 fatty acids from walnuts help regulate cortisol levels."
                },
                {
                    title: "Whole Grain Bowl with Roasted Vegetables",
                    description: "Complex carbohydrates can boost serotonin production, while the variety of vegetables provides stress-fighting nutrients."
                }
            ],
            "energetic": [
                {
                    title: "Protein-Packed Buddha Bowl",
                    description: "A balanced mix of quinoa, roasted chickpeas, fresh vegetables and tahini dressing to sustain your energy levels."
                },
                {
                    title: "Spicy Tacos with Guacamole",
                    description: "The combination of protein, healthy fats and metabolism-boosting spices complements your high energy state."
                },
                {
                    title: "Fruit and Nut Energy Balls",
                    description: "Natural sugars paired with protein and fiber for steady energy release, perfect for your active mood."
                }
            ],
            "romantic": [
                {
                    title: "Red Wine Poached Pears",
                    description: "Elegant, sensual dessert infused with cinnamon and vanilla. The red wine contains resveratrol which may enhance mood and blood flow."
                },
                {
                    title: "Oysters with Champagne Mignonette",
                    description: "Classic aphrodisiac rich in zinc and amino acids that boost dopamine, paired with effervescent champagne sauce."
                },
                {
                    title: "Dark Chocolate Covered Strawberries",
                    description: "The perfect romantic treat combining antioxidants from dark chocolate with vitamin C from fresh strawberries."
                },
                {
                    title: "Saffron Risotto",
                    description: "Luxurious, creamy rice dish with saffron that has mood-enhancing properties and creates a golden, romantic glow."
                }
            ],
            "need focus": [
                {
                    title: "Blueberry and Walnut Oatmeal",
                    description: "Slow-release carbohydrates from oats paired with antioxidant-rich blueberries and brain-boosting omega-3s from walnuts."
                },
                {
                    title: "Matcha Green Tea Latte",
                    description: "L-theanine in matcha provides calm alertness without the jitters of coffee, perfect for sustained focus."
                },
                {
                    title: "Salmon and Avocado Power Bowl",
                    description: "Omega-3 fatty acids from salmon paired with healthy fats from avocado support brain function and cognitive performance."
                },
                {
                    title: "Dark Chocolate with 85% Cacao",
                    description: "Small amounts of high-quality dark chocolate can improve blood flow to the brain and enhance focus with natural stimulants."
                }
            ],
            "default": [
                {
                    title: "Balanced Plate",
                    description: "A mix of lean protein, whole grains, and colorful vegetables to support overall wellbeing."
                },
                {
                    title: "Fresh Fruit Smoothie",
                    description: "A refreshing blend of seasonal fruits, yogurt and a touch of honey for natural energy."
                }
            ]
        };

        const chatArea = document.getElementById('chatArea');
        const userInput = document.getElementById('userInput');
        const typingIndicator = document.getElementById('typingIndicator');

        // Add message to chat
        function addMessage(text, isUser = false) {
            const messageDiv = document.createElement('div');
            messageDiv.className = `message ${isUser ? 'user' : 'bot'}`;
            messageDiv.textContent = text;
            chatArea.appendChild(messageDiv);
            chatArea.scrollTop = chatArea.scrollHeight;
        }

        // Add food suggestion to chat
        function addFoodSuggestion(suggestion) {
            const suggestionDiv = document.createElement('div');
            suggestionDiv.className = 'message bot';
            
            const foodSuggestionContent = document.createElement('div');
            foodSuggestionContent.className = 'food-suggestion';
            
            const titleElement = document.createElement('div');
            titleElement.className = 'food-title';
            titleElement.textContent = suggestion.title;
            
            const descElement = document.createElement('div');
            descElement.className = 'food-description';
            descElement.textContent = suggestion.description;
            
            foodSuggestionContent.appendChild(titleElement);
            foodSuggestionContent.appendChild(descElement);
            suggestionDiv.appendChild(foodSuggestionContent);
            
            chatArea.appendChild(suggestionDiv);
            chatArea.scrollTop = chatArea.scrollHeight;
        }

        // Show typing indicator
        function showTypingIndicator() {
            typingIndicator.style.display = 'block';
            chatArea.scrollTop = chatArea.scrollHeight;
        }

        // Hide typing indicator
        function hideTypingIndicator() {
            typingIndicator.style.display = 'none';
        }

        // Process user message
        function processMessage(text) {
            const lowerText = text.toLowerCase();
            
            // Enhanced mood detection
            let detectedMood = "default";
            
            if (lowerText.includes("happy") || lowerText.includes("joy") || lowerText.includes("excited") || lowerText.includes("great")) {
                detectedMood = "happy";
            } else if (lowerText.includes("sad") || lowerText.includes("down") || lowerText.includes("blue") || lowerText.includes("depressed")) {
                detectedMood = "sad";
            } else if (lowerText.includes("stress") || lowerText.includes("anxious") || lowerText.includes("overwhelmed") || lowerText.includes("nervous")) {
                detectedMood = "stressed";
            } else if (lowerText.includes("energetic") || lowerText.includes("active") || lowerText.includes("energized") || lowerText.includes("full of energy")) {
                detectedMood = "energetic";
            } else if (lowerText.includes("romantic") || lowerText.includes("date") || lowerText.includes("love") || lowerText.includes("passion")) {
                detectedMood = "romantic";
            } else if (lowerText.includes("focus") || lowerText.includes("concentrate") || lowerText.includes("productivity") || lowerText.includes("study") || lowerText.includes("work")) {
                detectedMood = "need focus";
            }
            
            showTypingIndicator();
            
            // Simulate AI thinking time
            setTimeout(() => {
                hideTypingIndicator();
                
                if (detectedMood !== "default") {
                    addMessage(`Based on what you've shared, I sense you're in a ${detectedMood} mood. Here are some food suggestions that might complement how you're feeling:`);
                } else if (lowerText.includes("recommend") || lowerText.includes("suggest") || lowerText.includes("what should")) {
                    addMessage("I'd be happy to recommend something! Here are a few options that promote general wellbeing:");
                } else if (lowerText.includes("hello") || lowerText.includes("hi ") || lowerText === "hi") {
                    addMessage("Hello! How are you feeling today? I can suggest foods based on your mood to enhance your dining experience.");
                    return;
                } else if (lowerText.includes("how are you")) {
                    addMessage("I'm here and ready to help you find the perfect food for your emotional state! How are you feeling today?");
                    return;
                } else if (lowerText.includes("thank")) {
                    addMessage("You're welcome! Would you like more personalized suggestions? Just let me know how you're feeling.");
                    return;
                } else {
                    addMessage("I'm trying to understand how you're feeling. Could you tell me more about your mood? Are you feeling happy, sad, stressed, energetic, romantic, or do you need focus?");
                    return;
                }
                
                // Get appropriate food suggestions
                const suggestions = foodSuggestions[detectedMood];
                
                // Display 1-2 random suggestions
                const numSuggestions = Math.min(2, suggestions.length);
                const selectedIndices = new Set();
                
                while (selectedIndices.size < numSuggestions) {
                    selectedIndices.add(Math.floor(Math.random() * suggestions.length));
                }
                
                selectedIndices.forEach(index => {
                    addFoodSuggestion(suggestions[index]);
                });
                
                // Follow-up question
                setTimeout(() => {
                    addMessage("Would you like more suggestions or have a specific dietary preference to consider?");
                }, 1000);
                
            }, 1500);
        }

        // Send message from input field
        function sendMessage() {
            const text = userInput.value.trim();
            if (text) {
                addMessage(text, true);
                userInput.value = '';
                processMessage(text);
            }
        }

        // Send mood from button
        function sendMood(mood) {
            addMessage(`I'm feeling ${mood}`, true);
            processMessage(`I'm feeling ${mood}`);
        }

        // Handle Enter key
        function handleKeyPress(event) {
            if (event.key === 'Enter') {
                sendMessage();
            }
        }
    </script>
</body>
</html>
