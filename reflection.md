# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").

  Kateryna : Then I just stated with number 67 it showed me "Go HIGHER!" that is already not right, because it is supposed to be lower. Then I decided to do 100 and it showed, that it is should go Lower. 98  or 99 showes to go higher. I was suprised then find out that the number was 47...

  Additionally I noticed it asks you to press Enter to apply, but nothing happens, only message goes away 

  Scoring bugs( sometimes adds points. update_score gives +5 on even attempts), State bug (Win/lose status is set but the matching state guard never re-runs cleanly. Status is set to "won"/"lost" inside the submit block but there's no st.rerun(), so the end-of-game message shows differently on the next interaction. Minor, but inconsistent with the New Game path which does rerun.)


  My input was : 67, 89, 100, 98,99,100  Seceret Number : 47
**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

| Input | Expected Behavior | Actual Behavior | Console Output / Error |
|-------|-------------------|-----------------|------------------------|
|67     | "Too High"        | "Too Low"       | error text             | 
|89     | "Too High"        |"Too Low"        | error text             |
|99     | "Too High"        |"Too Low"        | error text             |
|100    | "Too High"        | "Too High"      | there is no other integer number between 99 and 100|
---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

  I used Claude (in Claude Code's agent mode) as my main teammate on this project. I drove the investigation by reporting the bugs I found while playing, and the AI helped me locate the code responsible and refactor it.

   When I noticed the end-of-game message only showed up one click late, the AI suggested adding `st.rerun()` after the status changes away from "playing" in `app.py`. I verified this in the game by winning a round — before the fix the win message appeared on my  interaction, and after adding the rerun it showed immediately. The AI also suggested extracting `check_guess` into `logic_utils.py` so the app and the tests share one source of truth, which I confirmed by running pytest and seeing the tests import and pass against the shared function.

  
---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

- I looked thorugh the changed careguly, adiitionally I prompt AI to do some test cases, of  that we already have

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
