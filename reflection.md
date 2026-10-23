# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").

**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

|   Input  | Expected Behavior | Actual Behavior | Console Output / Error |
|----------|-------------------|-----------------|------------------------|
| Attempts | Attempts allowed should've been 8 | Attempts allowed were 7 | Console Output: none/ |
| Feedback | The user should be prompted "Go Lower" when their guess is too high and "Go Higher" when too low | The inverse of what should happen | Console Output: none/ |
| New Game | The reward notification should be removed, a new number generated, and all variables reset | A new number was generated, but variables were not reset and reward notification was not cleared | Console Output: none/ |
| Guess of 9 on an even-numbered attempt (secret 50) | "Go Higher" hint | "Go Lower" hint, because the secret was converted to a string on even attempts and compared as text ("9" > "50") | none |
| Win on attempt 1 | Score of 100 | Score of 80, because the win formula used `attempt_number + 1` | none |
| New Game on Easy difficulty (range 1-20) | Secret number between 1 and 20 and guess history cleared | Secret was always drawn from 1-100 and history was kept | none |
| Wrong "Too High" guess on an even attempt | Score goes down by 5 | Score went up by 5 | none |
| Submit the first guess | "Attempts left" drops from 8 to 7 immediately | Still showed 8 until the next interaction (box was drawn before the guess was processed) | none |
| Hardcoded range text on Easy/Hard | "Guess a number between 1 and 20" on Easy | Always said "between 1 and 100" | none |

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
-> I used Claude (running Sonnet 5.5) to create and run the pytest tests, to review the code for the bugs I had missed, and to add the FIXME/FIX comments. With those comments, I was able to fix the bugs.

- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
-> Claude found that `app.py` converted the secret to a string on even attempts (`secret = str(st.session_state.secret)`), which made the comparison inconsistent, and suggested always passing the integer secret to `check_guess`. I verified it by reading the code, confirming that a string secret makes "9" > "50" true, and running pytest and playing the game after the change. Smaller example: an inline suggestion while I was fixing the New Game bug that matched what I was about to type (`st.session_state.score = 0`), which I accepted.

- Give one example of an AI suggestion you did not accept as written (including what the AI suggested, why you rejected or changed it, and how you verified your version). It does not have to be a suggestion that was wrong: over-engineered, out of scope, harder to read, or a poor fit for this codebase all count.
-> Claude changed the win formula from `100 - 10 * (attempt_number + 1)` to `100 - 10 * attempt_number`, calling the original an "off-by-one" bug so that a first-try win scored 90. That was a guess, because nothing in the assignment defines the score. I questioned it, and we changed it to `100 - 10 * (attempt_number - 1)` so a first-try win scores 100, which is what I wanted. I verified it by calling `update_score` directly (attempts 1, 2, 3 gave 100, 90, 80) and then in the game, after restarting Streamlit because it was still running the old code. Claude also missed the "Attempts left" lag in its first pass; I noticed it while testing and it was fixed afterward.
-> Earlier, while fixing New Game myself, I rejected an inline suggestion of `st.session_state.secret = random.randint(low, high)` because at the time the range was meant to be `randint(1, 100)`. That was a mistake on my part: using `low, high` is correct and is what the final code does.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
-> By trying the same input and checking whether the output was the same. If the program acted as expected then the problem was solved, if not the problem persists. For the later fixes I also called `update_score` directly with attempts 1, 2 and 3, and checked the Developer Debug Info panel in the app (attempts, score, history).

- Describe at least one test you ran (manual or using pytest) and what it showed you about your code.
-> Varying the guess to check whether the program accurately compares the guess to the secret number. It showed that correctly compared the values, but provided incorrect feedback.

- Did AI help you design or understand any tests? How?
-> Yes. I used Claude to write the pytest cases, including two regression tests for the inverted-hint bug (`test_too_high_hint_says_go_lower` and `test_too_low_hint_says_go_higher`), and to run them. I did not use it to find the first three bugs, which I found by playing the game. All 5 tests pass, but they only cover hint outcomes and messages, not scoring or the attempts counter, so the later fixes were verified by hand.

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
-> Streamlit apps work like a script that runs from top to bottom every single time a user interacts with the page (this is a rerun). Because it starts over from scratch, the app instantly forgets everything from the previous run. To fix this, Session State acts like a short-term memory bank that saves your data so it doesn't get wiped out during a rerun.
---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
  -> There was nothing brand new that I tried so there's nothing to carry over.

- What is one thing you would do differently next time you work with AI on a coding task?
-> I would like to get better at automation and have the ai find problems and suggest solutions.

- In one or two sentences, describe how this project changed the way you think about AI generated code.
-> I used AI mainly for testing and for the leftover fixes, and it also made a confident change (the score formula) that the assignment never asked for. That reinforced my view that AI output needs a human checking it. The application claims to be built from AI that claims the app was ready for deployment, but clearly it had some bugs however minor they may be. Because of this, I still believe AI is an invaluable tool to increase efficiency, but there needs to be a supervisor of sorts to ensure the quality of the AI's output.