# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").

**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

|   Input  | Expected Behavior | Actual Behavior | Console Output / Error |
|----------|-----------------------------------|-------------------------|-----------------------|
| Attempts | Attempts allowed should've been 8 | Attempts allowed were 7 | Console Output: none/ |
| Feedback | The user should be prompted "Go Lower" when their guess is too high and "Go Higher" when too low | The inverse of what should happen | Console Output: none/ |
| New Game | The reward notification should be removed, a new number generated, and all variables reset | A new number was generated, but variables were not reset and reward notification was not cleared | Console Output: none/ |

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
-> I used claude to create and run the py-tests.

- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
-> One example is an inline suggestion when I was correcting the third error. I would start the line and provided the suggestion matches what I was going to type, I would accept or reject the suggestion. Example of an accepted suggestion: st.session_state.score = 0.

- Give one example of an AI suggestion you did not accept as written (including what the AI suggested, why you rejected or changed it, and how you verified your version). It does not have to be a suggestion that was wrong: over-engineered, out of scope, harder to read, or a poor fit for this codebase all count.
-> An example of a suggestion I rejected is: st.session_state.secret = random.randint(low, high), because the range used during the application was specifically randint(1, 100).

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
-> By trying the same input and checking whether the output was the same. If the program acted as expected then the problem was solved, if not the problem persists.

- Describe at least one test you ran (manual or using pytest) and what it showed you about your code.
-> Varying the guess to check whether the program accurately compares the guess to the secret number. It showed that correctly compared the values, but provided incorrect feedback.

- Did AI help you design or understand any tests? How?
-> Not quite, because no major models were used during the debugging.

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
-> Due to the lack of AI usage (outside of the testing), how I think about AI generated code has barely changed. The application claims to be built from AI that claims the app was ready for deployment, but clearly it had some bugs however minor they may be. Because of this, I still believe AI is an invaluable tool to increase efficiency, but there needs to be a supervisor of sorts to ensure the quality of the AI's output.