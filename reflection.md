# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

---

## 1. What was broken when you started?

When I first ran the game, it had multiple issues that made gameplay confusing and inconsistent.

### Bug 1: Incorrect feedback on guesses
| | Detail |
|---|---|
| **Expected** | Guessing low → "Go HIGHER!"; guessing high → "Go LOWER!" |
| **Actual** | Feedback was reversed — low guesses got "Go LOWER!", high guesses got "Go HIGHER!" |

### Bug 2: Attempts tracking and game state mismatch
| | Detail |
|---|---|
| **Expected** | Attempts count down correctly and stop the game at 0. |
| **Actual** | Attempts only incremented every other guess; history was delayed. End-game messages appeared alongside active game prompts. |

### Bug 3: New Game button didn't reset properly
| | Detail |
|---|---|
| **Expected** | Clicking "New Game" resets the secret, attempts, and history — ready to play immediately. |
| **Actual** | History and end-game messages persisted. Users had to refresh or switch difficulty to start fresh. |

### Bug 4: Difficulty settings were inconsistent
| | Detail |
|---|---|
| **Expected** | Difficulty scales logically: easier = smaller range or more attempts. |
| **Actual** | Easy (1–20, 6 attempts), Normal (1–100, 8 attempts), Hard (1–50, 5 attempts) — Hard was easier than Normal. Switching difficulty didn't reset the secret. |

---

## 2. How did you use AI as a teammate?

- **Tools used:** GitHub Copilot (VS Code) and ChatGPT — for explaining code, identifying bugs, and reasoning about session state.

- **✅ Correct AI suggestion:** Copilot correctly identified that `check_guess` was giving reversed feedback, explaining that high guesses triggered "Go HIGHER!" instead of "Go LOWER!" I verified this by manually testing guesses before and after the fix.

- **❌ Incorrect AI suggestion:** Copilot initially suggested the difficulty range inconsistency might be intentional. After comparing the ranges myself, I determined it wasn't — and manually refactored them so difficulty scales logically.

- **Bonus insight:** AI helped explain why guess history and attempts were delayed due to Streamlit's session state model, which pointed me toward using `st.form` for proper state updates.

---

## 3. Debugging and testing your fixes

- **How I decided a bug was fixed:** I tested manually across multiple scenarios. A fix counted when the incorrect behavior was gone, session state updated correctly, and no new issues appeared.

- **A specific test I ran:** I guessed numbers above and below the secret to verify hints were accurate. I also made sequential guesses to confirm attempts decremented every single time — and that the game ended exactly at the limit. Switching difficulties and clicking "New Game" confirmed everything reset as expected.

- **Did AI help with testing?** Yes — AI helped clarify expected outputs and edge cases like invalid inputs or repeated guesses, which shaped what I tested.

---

## 4. What did you learn about Streamlit and state?

Streamlit reruns the entire script on every interaction (button click, form submit, etc.). Session state is the memory that persists across those reruns — it's how the secret number, attempts, and guess history survive between interactions.

I also learned that wrapping inputs in `st.form` enables Enter key submission and prevents state updates from being delayed, which was key to fixing the attempts and history bugs.

---

## 5. Looking ahead: your developer habits

- **One habit to reuse:** Tackling one bug at a time and fully testing each fix before moving on — it keeps debugging manageable and prevents new issues from sneaking in.

- **One thing to do differently with AI:** Be more skeptical of AI suggestions upfront. Verify with testing before applying a fix, rather than assuming the suggestion is correct.

- **How this changed my view on AI-generated code:** AI is a great accelerator for debugging and reasoning through problems — but it's not always right. Treating it as a helpful teammate rather than a source of truth leads to more reliable results.

---