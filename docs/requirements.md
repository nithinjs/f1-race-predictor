# Requirements — F1 Race Predictor

**Version:** 0.1 (draft)  **Sprint:** 0  **Owner:** Nithin JS  **Related:** [Project charter](project-charter.md)

> This is a living document. New ideas are added to the sprint board's backlog as issues, prioritised at sprint planning, and recorded here when accepted.

---

## 1. Users

| User | Who they are | What they need |
|---|---|---|
|  **Casual fan** | Watches F1, wants to know what's likely to happen | Simple predictions, standings, results |
|  **Fantasy F1 player** | Plays F1 Fantasy ($100M budget, 5 drivers + 2 constructors) | Predictions *before* the lineup lock, value picks, risk |
|  **Recruiter / hiring manager** | Visits the site to assess the developer | About me, projects, how the model works |

## 2. Key decisions

- **D1.** The app's ML model predicts **race finishing positions** (the main target).
- **D2.** Two predictions per race weekend:
  - **Pre-qualifying:** must not use grid position (not yet known; avoids data leakage). Needed by fantasy players, whose lineups lock at the start of qualifying.
  - **Post-qualifying:** uses the starting grid (qualifying result after penalties).
- **D3.** Optional fan prediction game: fans make their own race prediction after qualifying and are scored with the same metrics as the model.
- **D4.** Circuit characteristics (e.g. overtaking difficulty) are expected to change how much the grid matters, and should be explored as a model feature.

## 3. Priorities (MoSCoW)

| Priority | Meaning |
|---|---|
| **Must** | v1 isn't viable without it |
| **Should** | Important, planned for v1 if time allows |
| **Could** | Nice to have; only after Musts and Shoulds |
| **Won't (this time)** | Agreed out of scope for v1; may return later |

## 4. User stories

###  Casual fan

**US-01 — Pre-qualifying race prediction** · *Must*
As a casual fan, I want to see the predicted race result before qualifying, so that I know who to watch this weekend.
- [ ] Shows predicted finishing order for all drivers for the next race
- [ ] Generated without using any qualifying or grid data
- [ ] Shows when the prediction was made

**US-02 — Post-qualifying race prediction** · *Must*
As a casual fan, I want to see an updated prediction after qualifying, so that I know how the grid changes the likely result.
- [ ] Updated after the starting grid is known
- [ ] Shows each driver's change vs the pre-qualifying prediction (↑/↓)

**US-03 — Starting grid** · *Must*
As a casual fan, I want to see the qualifying result and starting grid, so that I know where each driver starts the race.
- [ ] Shows qualifying position and starting position (including grid penalties)

**US-04 — Why the model predicted it** · *Should*
As a casual fan, I want to see why a driver is predicted to finish where they are, so that I can understand and trust the prediction.
- [ ] Shows the top 3 factors behind each driver's prediction in plain English

**US-05 — Drivers' championship standings** · *Should*
As a casual fan, I want to see the drivers' championship standings before the race weekend, so that I know who's in form.
- [ ] Shows the current points table, updated after each race

**US-06 — Constructors' championship standings** · *Should*
As a casual fan, I want to see the constructors' championship standings, so that I can follow how the teams compare.
- [ ] Shows the current constructors' points table, updated after each race

**US-07 — Past race results** · *Should*
As a casual fan, I want to look back at past race results, so that I can see how drivers and teams have performed.
- [ ] Results can be browsed by season and race

**US-08 — Make my own prediction** · *Should*
As a casual fan, I want to enter my own race prediction after qualifying, so that I can test my F1 knowledge.
- [ ] Fan can submit a predicted order before the race starts
- [ ] Submissions close when the race starts

**US-09 — Score my prediction** · *Should*
As a casual fan, I want to see how well my prediction did compared with the real result and the model, so that I can see if I beat the AI.
- [ ] Fan and model are scored with the same metrics (see section 6)
- [ ] Shows a "You vs the model" comparison

###  Fantasy F1 player

**US-10 — Prediction before the lineup lock** · *Must*
As a fantasy F1 player, I want to see each driver's predicted finishing position before qualifying, so that I can pick my team before the lineup lock.
- [ ] Uses the pre-qualifying prediction (US-01)
- [ ] Available before qualifying starts

**US-11 — Points-finish probability** · *Must*
As a fantasy F1 player, I want to see each driver's chance of finishing in the top 10, so that I can avoid drivers likely to score no points.
- [ ] Shows a probability (%) for each driver

**US-12 — Predicted constructors' results** · *Should*
As a fantasy F1 player, I want to see predicted constructors' results, so that I can choose my two constructors.
- [ ] Shows each team's predicted combined result for the race

**US-13 — Model track record** · *Should*
As a fantasy F1 player, I want to see how accurate past predictions were, so that I know how much to trust the model.
- [ ] Shows accuracy for each past race and the season average
- [ ] Compared against the baseline (section 6)

**US-14 — Value picks** · *Could*
As a fantasy F1 player, I want to compare a driver's predicted points against their fantasy price, so that I can find good-value picks within my budget.
- [ ] Shows predicted points per $1M of fantasy price
- [ ] Depends on finding a reliable source for fantasy prices (see Open questions)

**US-15 — DNF risk** · *Could*
As a fantasy F1 player, I want to see each driver's risk of not finishing, so that I can avoid big negative points.
- [ ] Shows a DNF probability (%) for each driver

**US-16 — Positions gained** · *Could*
As a fantasy F1 player, I want to see which drivers are likely to gain positions during the race, so that I can earn points for positions gained.
- [ ] Shows predicted positions gained/lost vs starting grid

###  Recruiter / hiring manager

**US-17 — About me** · *Must*
As a recruiter, I want to read about the developer's background and skills, so that I can judge whether they fit a role.
- [ ] About page with background, skills, and links to LinkedIn and GitHub

**US-18 — How it works** · *Should*
As a recruiter, I want to see how the project was built and how well the model performs, so that I can assess the developer's technical skills.
- [ ] Page explaining architecture, data, model, and honest metrics vs baseline
- [ ] Link to the GitHub repo and sprint board

**US-19 — Other projects** · *Should*
As a recruiter, I want to see the developer's other projects, so that I can see the range of their experience.
- [ ] Projects page linking to GitHub repos, including the AFL player tracking capstone

**US-23 — Contact the developer** · *Should*
As a recruiter, I want to send the developer a message from the website, so that I can reach out about a role quickly.
- [ ] Contact button on the About page opens a form (name, email, message)
- [ ] Messages are delivered to the developer's inbox
- [ ] The developer's email address is not shown publicly on the page
- [ ] Basic spam protection (e.g. a hidden honeypot field or rate limit)

###  Website and accounts

**US-20 — Home page** · *Must*
As a visitor, I want a home page showing the next race and its latest prediction, so that I can see the most important information straight away.
- [ ] Shows the next race name, date, and countdown
- [ ] Shows the latest prediction (pre- or post-qualifying) with a link to full details
- [ ] Navigation to all main pages

**US-21 — Sign up and log in** · *Should*
As a casual fan, I want to create an account and log in, so that my predictions and scores are saved between visits.
- [ ] Fan can sign up, log in, and log out
- [ ] Predictions and scores (US-08, US-09) are linked to the fan's account
- [ ] Predictions and race information can still be viewed without logging in

**US-22 — My prediction history** · *Could*
As a logged-in fan, I want to see my past predictions and scores, so that I can track whether I'm improving.
- [ ] Shows each past prediction, its score, and the model's score for the same race

###  Won't have (this time)

| Item | Reason |
|---|---|
| Live in-race predictions | Complex real-time data; out of scope in charter |
| Betting features | Out of scope in charter |
| Predicting the season's championship standings | Different problem (season-level); revisit after v1 |
| RAG chatbot over the F1 rulebook | Planned for v2 |

## 5. Non-functional requirements

| ID | Requirement |
|---|---|
| **NFR-01 Performance** | Pages load in under 3 seconds on a normal connection |
| **NFR-02 Freshness** | Post-qualifying prediction published within 2 hours of qualifying ending; results updated within 24 hours of each race |
| **NFR-03 Reliability** | The app reads from its own database, so it keeps working if FastF1 or its data sources are down |
| **NFR-04 No data leakage** | Each model only uses information available at prediction time; models are evaluated with a time-based split |
| **NFR-05 Reproducibility** | Dependencies pinned in `requirements.txt`; the same data and code give the same metrics |
| **NFR-06 Security** | No secrets (API keys, passwords) in code or Git history; stored in environment variables / GitHub Secrets. User passwords are never stored in plain text (hashed only) |
| **NFR-10 Privacy** | Only the minimum user data is stored (e.g. email, display name); users can delete their account |
| **NFR-07 Cost** | Hosting stays within AWS free-plan credits, then under ~A$10/month |
| **NFR-08 Mobile-friendly** | All pages usable on a phone |
| **NFR-09 Quality** | All changes go through pull requests; automated tests run in CI before merging |

## 6. Technical requirements

These describe *how the system is built*, not what users see. Full design goes in `docs/architecture.md` (#5).

| ID | Requirement |
|---|---|
| **TR-01 Database** | A relational database (PostgreSQL) designed for this project stores races, drivers, teams, results, predictions, and user accounts |
| **TR-02 Data pipeline** | A scheduled pipeline pulls new data from FastF1 after each session and loads it into the database |
| **TR-03 API** | A backend API (FastAPI) is the only way the website reads or writes data; the website never connects to the database directly |
| **TR-04 Model serving** | Trained models are versioned; predictions are generated by the pipeline and stored in the database |
| **TR-05 Website** | A React front end with pages for home, predictions, standings, results, fan game, how it works, projects, and about me |
| **TR-06 Authentication** | Secure login handled by the API (hashed passwords, token-based sessions) |
| **TR-07 Deployment** | Hosted on AWS; infrastructure costs monitored with a billing alarm |
| **TR-08 CI/CD** | GitHub Actions runs tests on every pull request and deploys `main` automatically |

## 7. How predictions are measured

| Metric | What it measures |
|---|---|
| **Mean absolute position error** | On average, how many places off each driver was |
| **Spearman rank correlation** | How similar the predicted order is to the real order (−1 to +1) |
| **Top-3 hit rate** | How many of the actual podium finishers were predicted in the top 3 |
| **Top-10 precision** | How many predicted points finishers actually scored points |

**Baselines the model must beat:**
- **Post-qualifying:** "drivers finish where they start" (starting grid order)
- **Pre-qualifying:** "drivers finish in championship standings order" (the grid isn't known yet)

## 8. Open questions

- [ ] **Sprint weekends:** handle them in v1, or treat only the main race? (Fantasy lineups lock before the Sprint on these weekends.)
- [ ] **Fantasy prices (US-14):** is there a reliable public source? Check during the data spike (#4).
- [ ] **Training data:** how many seasons have enough detail? Check during the data spike (#4).
- [ ] **Login method (US-21):** email and password, or sign-in with Google/GitHub? Decide when building the website.