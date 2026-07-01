# 🧩 Interactive Multi-Match Memory Game

Welcome to the **Memory Game**, a premium, highly responsive web-based card matching game. Unlike traditional memory games that only feature matching pairs, this game supports multi-match gameplay, ranging from standard pairs up to quintuplets (matching five cards at once) across 10 progressive levels of difficulty.

Developed with pure JavaScript DOM manipulation, custom event handling, and hardware-accelerated 3D CSS transitions, it provides a smooth, engaging user experience.

---

## 🚀 How to Run the Game

No build steps, dependencies, or servers are required to play the game:

1. Clone or download this repository.
2. Locate the [index.html] file on your computer.
3. Open [index.html] in any modern web browser (Chrome, Firefox, Edge, Safari).
4. Select a difficulty level (1-10) and start clicking cards to reveal matches!

---

## 🛠️ File Structure

The project has a clean, lightweight structure:

*   **[index.html]**: The structural skeleton of the game, setting up the container for the game grid and the level controls.
*   **[MemoryGame.js]**: Holds the primary game mechanics, game loop logic, and level configurations.
*   **[MemoryGame.css]**: Implements rich aesthetics, visual styles, and advanced 3D perspective animations for card flips and victory screens.
*   **[Event.js]**: A custom utility wrapper for cross-browser event handling (ensuring compatibility with standard and legacy APIs).
*   **[LICENSE]**: MIT License documentation.

---

## 🎮 Game Rules & Levels

To win a level, you must find all matching sets of cards. A set is determined by the level's specifications. If a flipped card doesn't match the active set, all currently open cards flip back face-down after a brief delay.

### Level Configuration Matrix

The game scales in grid size and the number of matching cards required per set:

| Level | Grid Layout (Rows × Cols) | Total Cards | Matches Required per Set |
| :---: | :-----------------------: | :---------: | :----------------------: |
|   **1**   | 3 × 4 | 12 | 2 (Pairs) |
|   **2**   | 4 × 4 | 16 | 2 (Pairs) |
|   **3**   | 4 × 5 | 20 | 2 (Pairs) |
|   **4**   | 3 × 4 | 12 | 3 (Triplets) |
|   **5**   | 3 × 5 | 15 | 3 (Triplets) |
|   **6**   | 3 × 6 | 18 | 3 (Triplets) |
|   **7**   | 4 × 4 | 16 | 4 (Quadruplets) |
|   **8**   | 4 × 5 | 20 | 4 (Quadruplets) |
|   **9**   | 4 × 6 | 24 | 4 (Quadruplets) |
|  **10**   | 5 × 6 | 30 | 5 (Quintuplets) |

### Performance Tracking
Upon successfully matching all cards in a level, the game displays:
*   **Clicks**: The total number of cards flipped.
*   **Efficiency**: An efficiency percentage calculated based on your total clicks relative to the minimum theoretically required flips. The formula used is:
    $$\text{Efficiency} = \text{round}\left(\frac{\text{Total Cards} \times 100}{\text{Clicks}}\right)$$

---

## 💻 Technical Overview

### 1. Cross-Browser Event Wrapper ([Event.js])
The code uses a helper instance of the `Event` class, which handles browser incompatibilities (e.g., standard `addEventListener` vs older IE `attachEvent`). It exposes:
*   `attach(evtName, element, listener, capture)`: Attaches a normalized event listener.
*   `detach(evtName, element, listener, capture)`: Detaches the listener.
*   `stop(evt)`: Prevents event propagation.
*   `prevent(evt)`: Prevents default event behavior.

### 2. Card Representation ([MemoryGame.js])
Each card is represented by an instance of the inner `Card` class:
*   `this.state`: Represents the visual state ($0$ for face-down, $1$ for face-up).
*   `this.freezed`: Set to $1$ when the card has been successfully matched, preventing further clicks.
*   `this.draw(idx, container)`: Dynamically generates the HTML markup for each card (consisting of `.card`, `.flipper`, `.front`, and `.back` faces).
*   `this.flip(state)`: Toggles classes and styles to execute the flipping animation.
*   `this.pulse()`: Plays an animation sequence when a matching set is completed.

### 3. Hardware-Accelerated 3D Animations ([MemoryGame.css])
To ensure premium visual quality, the game uses advanced CSS properties:
*   `perspective: 100` and `transform-style: preserve-3d` on card containers create depth.
*   `backface-visibility: hidden` hides the back of the card when it is flipped.
*   `transform: rotateY(180deg)` rotates the cards smoothly on the Y-axis.
*   Keyframe animation `@keyframes pulse` animates card background color to orange once they are matched.
