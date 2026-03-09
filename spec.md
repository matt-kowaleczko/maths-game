I want to creat a game for my 9 year old son to teach him timestables.
The time tables are up to 12 on default but it's adjustable in the menu.
The game needs to be web based and playable on a tablet or phone as well as on desktop.
He needs to answer questions in 6 seconds.
There is a man running from a monster representing 6 seconds time frame, the closer the monster gets to the man the less time left.
There is a score counter, if he answers the question correctly the score goes up by 1, if he answers incorrectly the score goes down by 1.
If the monster catches the man the game is over and the score is reset.
There is a menu where you can select the time tables you want to practice and the time frame you want to play in.
There is also a button to start the game.
When he answers correctly it "Very good my little teddy bear".
When he answers incorrectly it says "Jestes Pimpuch".
The input is free from keypad, not a multiple choice.
## Technical Architecture & Implementation Guidelines

### 1. Project Structure
*   **Frontend-Only:** Use a single-page application (SPA) approach. A single HTML file with embedded CSS and JavaScript is preferred for portability, or a simple Vite/React setup for better state management.
*   **State Management:** Use a central state object to track:
    *   `gameState`: (menu, playing, gameOver)
    *   `score`: Integer
    *   `settings`: { maxTable: 12, timeLimit: 6000 }
    *   `currentQuestion`: { a: number, b: number, answer: number }

### 2. Game Logic & Timer
*   **Game Loop:** Use `requestAnimationFrame` for smooth animation of the chase scene.
*   **Timer Logic:** The timer should be a countdown based on `Date.now()` to ensure accuracy across devices, rather than relying on `setInterval` which can drift.
*   **Visual Representation:** 
    *   The "Man" and "Monster" can be represented by SVG icons or Emoji.
    *   Calculate horizontal position: `distance = (remainingTime / totalTime) * containerWidth`.

### 3. Responsive UI/UX
*   **Input Method:** Implement a custom on-screen HTML/CSS numeric keypad. This ensures a consistent experience on tablets/phones without triggering the native OS keyboard which might obscure the game area.
*   **Layout:** Use Flexbox/Grid. The top bar shows the score, the middle section shows the chase animation, the center shows the question, and the bottom contains the keypad.

### 4. Audio & Feedback
*   **Feedback Triggers:** On answer submission, trigger a visual toast message or text overlay with the specific phrases:
    *   Success: "Very good my little teddy bear" (Green color).
    *   Failure: "Jestes Pimpuch" (Red color).
*   **Reset Logic:** If the timer reaches zero, transition to a "Game Over" screen, display the final score, and reset the score to 0 before allowing a restart.

### 5. Configuration Menu
*   **Dynamic Range:** Allow users to toggle specific tables (e.g., only practice 7s and 8s) or set a maximum range.
*   **Difficulty:** Provide a slider or input for the "Time Limit" (seconds) to adjust difficulty as the child improves.

### 6. Prompt Engineering Guidelines for Implementation
When prompting an LLM to generate the code, use the following constraints:
*   "Write the game in vanilla HTML5, CSS3, and JavaScript."
*   "Ensure the keypad is large and touch-friendly."
*   "Use CSS animations for the monster/man movement to ensure high performance on mobile devices."
*   "Ensure the game logic handles 'Enter' key presses for desktop users and 'Submit' button presses for touch users."
