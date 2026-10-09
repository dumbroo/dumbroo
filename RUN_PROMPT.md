Read PROGRESS.md, OPEN_ISSUES.md and PROJECT_INSTRUCTIONS.md in this folder first. This folder is engine v20.12 (the iccc-ebooks folder). The main library folder is C:\Users\User\OneDrive\Desktop\ICCC bharat\ICCC Ebook Library (02_Raw_PDFs, 03_Master_Data, 04_Ebooks, 06_Code).

Build NEET PG 2025 ebooks for the remaining states, one at a time, in this order: Uttarakhand, Himachal Pradesh, Jharkhand, Puducherry, Goa, Chandigarh, Delhi (first check it has its own state-quota counselling; skip it if seats go only through MCC), then North-East states only where official allotment lists exist, then Tamil Nadu Government quota only if its lists are available. Do not stop to ask me anything: flag problems and continue.

For each state, in order, finish it completely before starting the next:
1. Re-read PROGRESS.md (sections 1, 6, 7) and OPEN_ISSUES.md.
2. Download the official allotment lists, merit lists (for NEET AIR) and fee documents from the official counselling or university site only. Save them in data/raw/<CODE>_PG_2025/ in this engine folder AND in the library's 02_Raw_PDFs\PG\<CODE_State>, with the usual naming (e.g. UK_PG_2025_CUTOFF_R1.pdf). Register them in cutoff_sources.csv / fee_sources.csv. If a site can't be reached or a list is missing, log it in OPEN_ISSUES.md and build with what exists.
3. Write the parser: find rounds and columns by their headings, stop with a clear error if the layout is unexpected. No numbers typed by hand. Add the ebooks.json entry, copied from the most similar existing state.
4. Follow every rule in PROGRESS.md section 6: a round counts only newly allotted seats; rank = NEET AIR (from the merit list by roll number if the allotment list doesn't print it); fee per year with its source; missing fees blank, never guessed; separate CQ and MQ ebooks where the state counsels them separately; v20 design. Any new judgment call: use the closest existing rule and add it to section 6 as "proposed by Claude, confirm".
5. Run build.py. Check: a second reading of the lists, an AIR spot check, ebook = CSV, every other ebook byte-for-byte unchanged, no page errors.
6. Independent rule check: start a subagent that has not seen this work. Give it PROGRESS.md section 6, the state's source PDFs, its CSV and its ebook. Ask it to check each rule (newly allotted seats only per round, NEET AIR, fee per year with source, blanks not guesses, CQ/MQ split, seat types and categories as printed) and list every break with an example row. Fix every break, or mark the state "not ready" with the reason.
7. Update PROGRESS.md (section 3 row, section 7 version line, "Last updated") and OPEN_ISSUES.md (a section for the state). Make the new engine version (v20.13, v20.14 ...) as a zip in the library's 06_Code (leave out data/raw, as before). Save the ebook and its personal copy in the library's 04_Ebooks\preview and 04_Ebooks\personal, and the state's CSVs in 03_Master_Data.
8. Only then move to the next state. Never edit an earlier state's parser or ebook while working on a later one; if you find a problem in an earlier state, log it in OPEN_ISSUES.md.

Always:
- Never change the template, contact.json, ui.json or any existing parser or ebook. If a state needs an engine change, make it optional (off for every existing ebook) and prove the other ebooks are byte-for-byte unchanged.
- Before each new state, copy the ebooks.json entry of the most similar existing state as the starting point.
- Explain decisions in plain language in the tracker; I am not a developer.
- If you are resumed in a new session, read RUN_PROMPT.md and PROGRESS.md and continue with the next state that isn't done.
- At the end, write a short summary at the top of PROGRESS.md: which states were built, which are "not ready" and why, and every new "proposed by Claude" rule.
