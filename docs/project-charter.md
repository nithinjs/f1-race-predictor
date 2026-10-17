# Project Charter — F1 Race Predictor 

**Owner:** Nithin JS  **Start date:** 17 October 2026  **Method:** Agile (Scrum-style, solo), 2-week sprints

---

## 1. Problem
F1 fans and fantasy players guess race results from gut feel. Decades of public race data exist, but there's no simple tool that turns that history into clear, explainable predictions.

## 2. Goal
Build a web app that predicts **finishing positions for upcoming F1 races** using historical results, qualifying, driver and team form, and race strategy data, and explains *why* it made each prediction.

## 3. Target users
| Stage | User | What they want |
|---|---|---|
| v1 | Casual fan | "Who's likely to win this weekend, and why?" |
| v1 | Fantasy F1 player | "Which drivers are likely to score points?" |
| Later | Analyst | Deeper stats, model details, comparisons |

## 4. Scope
**In scope (v1)**
- Data pipeline: historical F1 data → own designed database
- ML model predicting finishing position / points-finish probability
- API serving predictions
- Website: predictions page, race history dashboard, projects page, About Me page
- Power BI season report
- CI/CD and cloud deployment (AWS)

**Later (v2)**
- RAG chatbot over the F1 rulebook
- Analyst-level features

**Out of scope**
- Live in-race predictions
- Betting features

## 5. Success criteria
- Model beats the simple baseline *"drivers finish where they start"* (measured on races the model never saw — time-based split)
- Site is live on a public URL
- Every sprint has a documented goal, review and retro on GitHub

## 6. Constraints
- Time: ~20 hours/week
- Budget: ~$0 — free tools first; AWS free-plan credits only at deployment
- Data: public sources only (FastF1 / jolpica-f1)

## 7. Risks
| Risk | Plan |
|---|---|
| Scope creep (too many tools) | Strict sprint goals; extras go to the backlog |
| AWS costs | Billing alarm on day one; build locally first |
| F1 is hard to predict (crashes, weather) | Report honest metrics; compare to baseline |
| Availability changes | Sprints can be re-planned at each sprint review |

## 8. Timeline (target: live before the 2027 season starts)
| Sprint | Dates | Goal |
|---|---|---|
| 0 | 17 – 30 Oct | Charter, requirements, GitHub board, architecture sketch |
| 1 | 31 Oct – 13 Nov | Database design + data pipeline |
| 2 | 14 – 27 Nov | Data exploration + baseline model |
| 3 | 28 Nov – 11 Dec | API + first web page (end-to-end working) |
| 4 | 12 – 25 Dec | Better model + predictions page + About Me |
| 5 | 26 Dec – 8 Jan | Power BI report |
| 6 | 9 – 22 Jan | CI/CD + AWS deployment |
| 7 | 23 Jan – 5 Feb | Polish, demo video, v1 launch |
| 8+ | Feb onward | RAG chatbot (v2) |
