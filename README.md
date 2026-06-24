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

- [x] Describe the game's purpose. A Streamlit number-guessing game: the app picks a secret number within a difficulty range, and the player guesses until they find it, getting Too High / Too Low hints and a score that rewards fewer attempts.

- [x] Detail which bugs you found.
  - Backwards hints: a guess above the secret said Go HIGHER and a guess below said Go LOWER.
  - Scoring glitch: update_score added +5 on even-numbered attempts, so wrong guesses could increase the score.
  - Late UI update: the win/lose message rendered one interaction behind because the submit block set the status but never re-ran.
  - Duplicated logic: check_guess lived in app.py while logic_utils.py (used by the tests) had only an unimplemented stub.

- [x] Explain what fixes you applied.
  - Corrected the hint direction in check_guess (Too High now points lower, Too Low points higher) and added int coercion for a safe numeric comparison.
  - Removed the +5 on even attempts branch in update_score so a wrong guess always deducts 5.
  - Added st.rerun() once the game ends so the result shows immediately.
  - Moved check_guess into logic_utils.py as the single source of truth and imported it into app.py, then added pytest cases for scoring and hint direction.

## 📸 Demo Walkthrough

A step-by-step walkthrough of a sample game on the fixed app, so a reader can follow along without a video:

1. Launch the app with `python -m streamlit run app.py` and open it in the browser. The "Glitchy Guesser" page loads with a difficulty selector and a guess input.
2. Pick a difficulty (e.g. **Normal**, range 1–100). A new secret number is chosen once and stays fixed for the round — it no longer changes on every Submit.
3. Enter a guess that's too high, say **80**, and click **Submit**. The game responds **"Too High — 📉 Go LOWER!"** (the hint now points the correct direction), and the score drops by 5.
4. Guess too low, say **30**, and Submit. The game responds **"Too Low — 📈 Go HIGHER!"** and again deducts 5 — wrong guesses always lose points, with no accidental bonus on even attempts.
5. Narrow in with another guess, e.g. **55**, using the hints to adjust up or down.
6. Enter the correct number, e.g. **47**, and Submit. The game shows **"🎉 Correct!"**, awards points based on how few attempts you used, and the end-of-game message appears immediately (thanks to `st.rerun()`) instead of lagging a click behind.
7. Click **New Game** to reset the score and status and start a fresh round with a new secret number.

## 🧪 Test Results

```
# Paste your pytest output here, e.g.:
# pytest tests/
# ========================= X passed in 0.XXs =========================
```

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
