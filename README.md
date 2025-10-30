<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Everyday & Digital Terms</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1100px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #43e97b, #38f9d7);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.3em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.1em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 20px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 15px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #43e97b, #38f9d7);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(67, 233, 123, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 25px;
            min-height: 450px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f0fff4, #e8fcf7);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
            border: 2px solid #43e97b;
            box-shadow: 0 4px 15px rgba(67, 233, 123, 0.2);
        }

        .word-bank h3 {
            color: #43e97b;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.3em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #43e97b, #38f9d7);
            color: white;
            padding: 8px 16px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 14px;
            box-shadow: 0 3px 10px rgba(67, 233, 123, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(67, 233, 123, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 15px;
            border-left: 5px solid #43e97b;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #43e97b;
            margin-bottom: 12px;
            font-size: 1.2em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 15px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 12px;
            margin-top: 12px;
        }

        .option {
            padding: 12px 18px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
            font-size: 14px;
        }

        .option:hover {
            border-color: #43e97b;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(67, 233, 123, 0.2);
        }

        .option.selected {
            background: #43e97b;
            color: white;
            border-color: #43e97b;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #43e97b;
            font-size: 1.1em;
        }

        .match-item {
            padding: 12px;
            margin: 6px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
            font-size: 14px;
        }

        .match-item:hover {
            border-color: #43e97b;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(67, 233, 123, 0.2);
        }

        .match-item.selected {
            background: #e8fcf7;
            border-color: #43e97b;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #43e97b, #38f9d7);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 15px;
            font-weight: bold;
            margin: 15px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(67, 233, 123, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(67, 233, 123, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #f44336, #ff7961);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 15px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(244, 67, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(244, 67, 54, 0.4);
        }

        .feedback {
            margin-top: 12px;
            padding: 12px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
            font-size: 14px;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #43e97b, #38f9d7);
            color: white;
            padding: 12px 18px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(67, 233, 123, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 22px;
            margin-right: 8px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 15px;
        }

        .vocabulary-item {
            margin-bottom: 20px;
            padding: 18px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #43e97b;
            margin-bottom: 8px;
            font-size: 1.3em;
            border-bottom: 2px solid #43e97b;
            padding-bottom: 6px;
        }

        .vocabulary-item p {
            margin-bottom: 6px;
            line-height: 1.5;
            font-size: 14px;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 12px;
            border-left: 3px solid #43e97b;
            margin-top: 8px;
            font-size: 13px;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 15px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 180px;
                font-size: 14px;
            }
            
            .score {
                position: static;
                margin: 15px auto;
                display: block;
                width: fit-content;
            }
            
            .header h1 {
                font-size: 1.8em;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/12</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: Everyday & Digital Terms</h1>
            <p>Test your knowledge of these English terms!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary')">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Definitions</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #43e97b;">Vocabulary Explanations</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3>postpone</h3>
                    <p><strong>Definition:</strong> To delay or put off to a later time.</p>
                    <p><strong>Usage:</strong> Used for events, meetings, or tasks that are rescheduled.</p>
                    <p class="example"><strong>Example:</strong> "We had to postpone the meeting until next week due to the storm."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>rush</h3>
                    <p><strong>Definition:</strong> To move or act with great haste; to hurry.</p>
                    <p><strong>Usage:</strong> Can describe physical movement or the need to complete something quickly.</p>
                    <p class="example"><strong>Example:</strong> "I had to rush to catch the last train home."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>inhabitants</h3>
                    <p><strong>Definition:</strong> People or animals that live in a particular place.</p>
                    <p><strong>Usage:</strong> Refers to residents of a city, country, or any dwelling place.</p>
                    <p class="example"><strong>Example:</strong> "The inhabitants of the small island rely on fishing for their livelihood."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>useful</h3>
                    <p><strong>Definition:</strong> Able to be used for a practical purpose or in several ways.</p>
                    <p><strong>Usage:</strong> Describes objects, information, or skills that provide benefit.</p>
                    <p class="example"><strong>Example:</strong> "This multitool is very useful for camping trips."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>inefficient</h3>
                    <p><strong>Definition:</strong> Not achieving maximum productivity; wasting time or resources.</p>
                    <p><strong>Usage:</strong> Describes processes, systems, or methods that don't work well.</p>
                    <p class="example"><strong>Example:</strong> "The old manufacturing process was inefficient and costly."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>laugh</h3>
                    <p><strong>Definition:</strong> To make the spontaneous sounds and movements of the face and body that are the instinctive expressions of lively amusement.</p>
                    <p><strong>Usage:</strong> A natural reaction to something funny or amusing.</p>
                    <p class="example"><strong>Example:</strong> "The children laugh happily while playing in the park."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>expire</h3>
                    <p><strong>Definition:</strong> To come to an end; to cease to be valid.</p>
                    <p><strong>Usage:</strong> Used for dates, contracts, licenses, or products that are no longer valid.</p>
                    <p class="example"><strong>Example:</strong> "My driver's license will expire next month."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>folder</h3>
                    <p><strong>Definition:</strong> A directory or container for organizing and storing files or documents.</p>
                    <p><strong>Usage:</strong> Can be physical (paper folder) or digital (computer folder).</p>
                    <p class="example"><strong>Example:</strong> "I keep all my important documents in a blue folder on my desk."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>users</h3>
                    <p><strong>Definition:</strong> People who use or operate something, especially computers or services.</p>
                    <p><strong>Usage:</strong> Common in technology contexts for people using software, websites, or devices.</p>
                    <p class="example"><strong>Example:</strong> "The new app already has over a million active users."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>appear</h3>
                    <p><strong>Definition:</strong> To become visible or present; to seem or look a certain way.</p>
                    <p><strong>Usage:</strong> Can refer to physical presence or giving a certain impression.</p>
                    <p class="example"><strong>Example:</strong> "The sun began to appear from behind the clouds."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>pain</h3>
                    <p><strong>Definition:</strong> Physical suffering or discomfort caused by illness or injury.</p>
                    <p><strong>Usage:</strong> Can also refer to emotional distress.</p>
                    <p class="example"><strong>Example:</strong> "She felt a sharp pain in her knee after falling."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>back</h3>
                    <p><strong>Definition:</strong> The rear surface of the human body from the shoulders to the hips.</p>
                    <p><strong>Usage:</strong> Refers to the posterior part of the torso.</p>
                    <p class="example"><strong>Example:</strong> "My back hurts from sitting at the desk all day."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>gathering</h3>
                    <p><strong>Definition:</strong> An assembly or meeting of people.</p>
                    <p><strong>Usage:</strong> Can be formal or informal social events.</p>
                    <p class="example"><strong>Example:</strong> "We're having a small gathering at our house this weekend."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>capable</h3>
                    <p><strong>Definition:</strong> Having the ability, fitness, or quality necessary to do or achieve something.</p>
                    <p><strong>Usage:</strong> Describes people who have the skills or capacity to accomplish tasks.</p>
                    <p class="example"><strong>Example:</strong> "She is a very capable manager who handles difficult situations well."</p>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">postpone</span>
                    <span class="word-option">rush</span>
                    <span class="word-option">inhabitants</span>
                    <span class="word-option">useful</span>
                    <span class="word-option">inefficient</span>
                    <span class="word-option">laugh</span>
                    <span class="word-option">expire</span>
                    <span class="word-option">folder</span>
                    <span class="word-option">users</span>
                    <span class="word-option">appear</span>
                    <span class="word-option">pain</span>
                    <span class="word-option">back</span>
                    <span class="word-option">gathering</span>
                    <span class="word-option">capable</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #43e97b;">Match the words with their definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Vocabulary Words</h4>
                    <div class="match-item" data-word="postpone" onclick="selectMatch(this)">postpone</div>
                    <div class="match-item" data-word="rush" onclick="selectMatch(this)">rush</div>
                    <div class="match-item" data-word="inhabitants" onclick="selectMatch(this)">inhabitants</div>
                    <div class="match-item" data-word="useful" onclick="selectMatch(this)">useful</div>
                    <div class="match-item" data-word="inefficient" onclick="selectMatch(this)">inefficient</div>
                    <div class="match-item" data-word="laugh" onclick="selectMatch(this)">laugh</div>
                    <div class="match-item" data-word="expire" onclick="selectMatch(this)">expire</div>
                    <div class="match-item" data-word="folder" onclick="selectMatch(this)">folder</div>
                    <div class="match-item" data-word="users" onclick="selectMatch(this)">users</div>
                    <div class="match-item" data-word="appear" onclick="selectMatch(this)">appear</div>
                    <div class="match-item" data-word="pain" onclick="selectMatch(this)">pain</div>
                    <div class="match-item" data-word="back" onclick="selectMatch(this)">back</div>
                    <div class="match-item" data-word="gathering" onclick="selectMatch(this)">gathering</div>
                    <div class="match-item" data-word="capable" onclick="selectMatch(this)">capable</div>
                </div>
                <div class="match-column">
                    <h4>Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What does "postpone" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To cancel completely</div>
                    <div class="option" onclick="selectOption(this, true)">To delay to a later time</div>
                    <div class="option" onclick="selectOption(this, false)">To start early</div>
                    <div class="option" onclick="selectOption(this, false)">To make longer</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: What does "rush" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To move slowly</div>
                    <div class="option" onclick="selectOption(this, true)">To move or act with great haste</div>
                    <div class="option" onclick="selectOption(this, false)">To stop completely</div>
                    <div class="option" onclick="selectOption(this, false)">To plan carefully</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: Who are "inhabitants"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Visitors to a place</div>
                    <div class="option" onclick="selectOption(this, true)">People who live in a particular place</div>
                    <div class="option" onclick="selectOption(this, false)">Government officials</div>
                    <div class="option" onclick="selectOption(this, false)">Tourists</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: What does "useful" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Broken or not working</div>
                    <div class="option" onclick="selectOption(this, true)">Able to be used for practical purposes</div>
                    <div class="option" onclick="selectOption(this, false)">Very expensive</div>
                    <div class="option" onclick="selectOption(this, false)">Beautiful to look at</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: What does "inefficient" describe?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Something that works perfectly</div>
                    <div class="option" onclick="selectOption(this, true)">Something that wastes time or resources</div>
                    <div class="option" onclick="selectOption(this, false)">Something very fast</div>
                    <div class="option" onclick="selectOption(this, false)">Something modern</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: What does "laugh" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To cry sadly</div>
                    <div class="option" onclick="selectOption(this, true)">To make sounds of amusement</div>
                    <div class="option" onclick="selectOption(this, false)">To speak quietly</div>
                    <div class="option" onclick="selectOption(this, false)">To sing loudly</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 7: What does "expire" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To begin</div>
                    <div class="option" onclick="selectOption(this, true)">To come to an end or cease to be valid</div>
                    <div class="option" onclick="selectOption(this, false)">To renew</div>
                    <div class="option" onclick="selectOption(this, false)">To extend</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 8: What is a "folder"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of furniture</div>
                    <div class="option" onclick="selectOption(this, true)">A container for organizing documents</div>
                    <div class="option" onclick="selectOption(this, false)">A kind of food</div>
                    <div class="option" onclick="selectOption(this, false)">A musical instrument</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 9: Who are "users"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">People who create products</div>
                    <div class="option" onclick="selectOption(this, true)">People who use services or products</div>
                    <div class="option" onclick="selectOption(this, false)">People who sell things</div>
                    <div class="option" onclick="selectOption(this, false)">People who repair things</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 10: What does "appear" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To disappear</div>
                    <div class="option" onclick="selectOption(this, true)">To become visible or present</div>
                    <div class="option" onclick="selectOption(this, false)">To hide</div>
                    <div class="option" onclick="selectOption(this, false)">To change color</div>
                </div>
                <div class="feedback" id="mc-feedback-10" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 11: What is "pain"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A feeling of happiness</div>
                    <div class="option" onclick="selectOption(this, true)">Physical suffering or discomfort</div>
                    <div class="option" onclick="selectOption(this, false)">A type of medicine</div>
                    <div class="option" onclick="selectOption(this, false)">A relaxing sensation</div>
                </div>
                <div class="feedback" id="mc-feedback-11" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 12: What does "back" refer to in this context?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">The front of the body</div>
                    <div class="option" onclick="selectOption(this, true)">The rear surface of the human body</div>
                    <div class="option" onclick="selectOption(this, false)">A direction</div>
                    <div class="option" onclick="selectOption(this, false)">A support</div>
                </div>
                <div class="feedback" id="mc-feedback-12" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 13: What is a "gathering"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A separation</div>
                    <div class="option" onclick="selectOption(this, true)">An assembly or meeting of people</div>
                    <div class="option" onclick="selectOption(this, false)">A single person</div>
                    <div class="option" onclick="selectOption(this, false)">A type of food</div>
                </div>
                <div class="feedback" id="mc-feedback-13" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 14: What does "capable" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Unable to do something</div>
                    <div class="option" onclick="selectOption(this, true)">Having the ability to do something</div>
                    <div class="option" onclick="selectOption(this, false)">Not interested in learning</div>
                    <div class="option" onclick="selectOption(this, false)">Too young to understand</div>
                </div>
                <div class="feedback" id="mc-feedback-14" style="display: none;"></div>
            </div>
            
            <button class="reset-btn" onclick="resetMultipleChoice()">Reset Answers</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        let multipleChoiceCorrect = 0;
        
        // Definitions for the matching game
        const definitions = [
            { meaning: "postpone", text: "To delay to a later time" },
            { meaning: "rush", text: "To move or act with great haste" },
            { meaning: "inhabitants", text: "People who live in a particular place" },
            { meaning: "useful", text: "Able to be used for practical purposes" },
            { meaning: "inefficient", text: "Wasting time or resources" },
            { meaning: "laugh", text: "To make sounds of amusement" },
            { meaning: "expire", text: "To come to an end or cease to be valid" },
            { meaning: "folder", text: "A container for organizing documents" },
            { meaning: "users", text: "People who use services or products" },
            { meaning: "appear", text: "To become visible or present" },
            { meaning: "pain", text: "Physical suffering or discomfort" },
            { meaning: "back", text: "The rear surface of the human body" },
            { meaning: "gathering", text: "An assembly or meeting of people" },
            { meaning: "capable", text: "Having the ability to do something" }
        ];

        // Sentences for the fill-in-the-blanks game
        const sentences = [
            { text: "We had to <input type='text' class='fill-blank' data-answer='postpone' placeholder='answer'> the meeting until next week due to the storm.", answer: "postpone" },
            { text: "I had to <input type='text' class='fill-blank' data-answer='rush' placeholder='answer'> to catch the last train home.", answer: "rush" },
            { text: "The <input type='text' class='fill-blank' data-answer='inhabitants' placeholder='answer'> of the small island rely on fishing for their livelihood.", answer: "inhabitants" },
            { text: "This multitool is very <input type='text' class='fill-blank' data-answer='useful' placeholder='answer'> for camping trips.", answer: "useful" },
            { text: "The old manufacturing process was <input type='text' class='fill-blank' data-answer='inefficient' placeholder='answer'> and costly.", answer: "inefficient" },
            { text: "The children <input type='text' class='fill-blank' data-answer='laugh' placeholder='answer'> happily while playing in the park.", answer: "laugh" },
            { text: "My driver's license will <input type='text' class='fill-blank' data-answer='expire' placeholder='answer'> next month.", answer: "expire" },
            { text: "I keep all my important documents in a blue <input type='text' class='fill-blank' data-answer='folder' placeholder='answer'> on my desk.", answer: "folder" },
            { text: "The new app already has over a million active <input type='text' class='fill-blank' data-answer='users' placeholder='answer'>.", answer: "users" },
            { text: "The sun began to <input type='text' class='fill-blank' data-answer='appear' placeholder='answer'> from behind the clouds.", answer: "appear" },
            { text: "She felt a sharp <input type='text' class='fill-blank' data-answer='pain' placeholder='answer'> in her knee after falling.", answer: "pain" },
            { text: "My <input type='text' class='fill-blank' data-answer='back' placeholder='answer'> hurts from sitting at the desk all day.", answer: "back" },
            { text: "We're having a small <input type='text' class='fill-blank' data-answer='gathering' placeholder='answer'> at our house this weekend.", answer: "gathering" },
            { text: "She is a very <input type='text' class='fill-blank' data-answer='capable' placeholder='answer'> manager who handles difficult situations well.", answer: "capable" }
        ];

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences
            const shuffledSentences = shuffleArray([...sentences]);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Question ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                // Reset matching game state
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                document.getElementById('matching-feedback').style.display = 'none';
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            
            // Count correct answers in multiple choice
            multipleChoiceCorrect = document.querySelectorAll('#multiple-choice .option.correct.selected').length;
            updateScore();
        }

        function resetMultipleChoice() {
            document.querySelectorAll('#multiple-choice .option').forEach(option => {
                option.classList.remove('selected', 'correct', 'incorrect');
            });
            
            document.querySelectorAll('#multiple-choice .feedback').forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            multipleChoiceCorrect = 0;
            updateScore();
        }

        function updateScore() {
            // Total score
            score = fillBlanksCorrect + matchingCorrect + multipleChoiceCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
        }
    </script>
</body>
</html>
