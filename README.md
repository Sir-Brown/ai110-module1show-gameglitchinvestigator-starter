# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the broken app: `python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

- [x] Describe the game's purpose.
It is a simple number guessing game. It randomly generates a number and prompts the user to guess it. If they are too low or too high, it will let them know via hints and end once they have made a correct guess. The user is limited to 8 attempts each of which, if unsuccessful, result in a 5 point reduction of their total score.

- [x] Detail which bugs you found.
Three bugs were found:
1. The attempts allowed was incorrect.
2. The hints were incorrect.
3. The new game button did not work correctly.

- [x] Explain what fixes you applied.
1. I changed the syntax that resulted in the incorrect attempts allowed issue (started the count from 0 instead of 1).
2. Simply changed what result warranted what hint.
3. Changed the syntax of the new game function (clears existing prompts, resets variables, and generates new number).

## 📸 Demo Walkthrough

Describe your fixed game in numbered steps so a reader can follow along without watching a video:

1. User enters a guess of 23
2. Game returns "Too Low"
3. Score updates correctly after each guess
4. User enters a guess of 37
5. Game returns "Too High"
6. Score updates correctly after each guess
7. User enters a guess of 32
8. Game returns "Congratulations! You win!"
9. Game ends after the correct guess
10. User has option to play again by clicking the "New Game" button

**Screenshot** *(optional)*: <!-- Insert a screenshot of your fixed, winning game here -->

## 🧪 Test Results

I added two regression tests to `tests/test_game_logic.py` that target the inverted-hint bug: `test_too_high_hint_says_go_lower` and `test_too_low_hint_says_go_higher`. I also moved the game logic from `app.py` into `logic_utils.py` and updated the starter tests to unpack the `(outcome, message)` tuple that `check_guess` returns.

```
$ python -m pytest -v
============================= test session starts =============================
platform win32 -- Python 3.13.7, pytest-9.0.2, pluggy-1.6.0 -- C:\Users\djain\AppData\Local\Programs\Python\Python313\python.exe
collecting ... collected 5 items

tests/test_game_logic.py::test_winning_guess PASSED                      [ 20%]
tests/test_game_logic.py::test_guess_too_high PASSED                     [ 40%]
tests/test_game_logic.py::test_guess_too_low PASSED                      [ 60%]
tests/test_game_logic.py::test_too_high_hint_says_go_lower PASSED        [ 80%]
tests/test_game_logic.py::test_too_low_hint_says_go_higher PASSED        [100%]

============================== 5 passed in 0.02s ==============================
```

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
