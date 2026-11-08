# Scratch log (raw, unpolished)

Fri Nov 6 11:30 - Kit downloaded to ~/Downloads/LabFiles; relocated to ~/Labfiles (lowercase f) to match guide paths. Briefly opened the wrong kit (WA3870) first; caught it by checking before copying.
Fri Nov 6 11:50 - Starter ships with NO .gitignore despite the guide saying it keeps node_modules out. SECOND PHASE IN A ROW (same in Phase 2). Caught before first commit; created a minimal one. Raise with instructor.
Fri Nov 6 12:15 - Day 1 assembly verified: 6 quotes seeded (auto q1 q4 q6; renewal q1 q5). Seeded docs have NO createdAt; API-created quotes will. npm test fails with Cannot find module src/routes.js, as documented.
Fri Nov 6 13:00 - Board built with 13 issues (3 closed Day 1). Closed issues do not appear in the board Add item picker; added them from each issue sidebar instead. Board set Public and checked in an incognito window.
Sun Nov 8 (Day 2) - Routes wired. curl tour matched Friday mongosh inspection exactly. Validation: age 5 -> 400 naming field and rule; type boat -> 400; unknown id -> 404.
Sun Nov 8 (Day 2) - DEMO LIED, TESTS TOLD THE TRUTH: POST returned a clean 201 with monthlyPremium 0.35 for 50000 auto coverage. npm test: 6 of 7 pass; premium test fails 0.35 !== 400. Cause: AI-drafted POST handler passed age and coverageAmount in the wrong order. Kit one-line fix applied; 7 of 7 pass; same POST now returns 400.
Sun Nov 8 (Day 2) - BAD DATA OUTLIVES BAD CODE: the 0.35 quote is still in the database after the fix. Thursday seed reset clears it.
Sun Nov 8 (Day 2) - SERVICE_NAME set (manual restart needed: watch reloads code, not .env). Rates 90/135/70: auto 35/50000 = 450, tests 7/7. GraphQL mounted: life 30/100000 = 700 via mutation, visible through REST. All four INSERT markers filled.
