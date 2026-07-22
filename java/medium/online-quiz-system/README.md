# Online Quiz System

A JSP web app that runs a multi-team, multi-round elimination quiz from an admin console. Also referred to internally as "Computerization of Blue Book."

## What it does

An administrator logs in, sets up a quiz (number of teams, number of questions, marks per correct/wrong answer, pass marks), and the app runs the quiz one question at a time with a 30-second timer per question. Questions rotate across teams. After a round, teams that clear the pass marks advance to the next round; the rest are eliminated. Rounds continue until a single winner remains or nobody passes.

It's built as a set of JSP pages that talk to a relational database. Server-side state between pages is carried in the HTTP session; scores and quiz config are persisted in database tables.

This is a learning/academic project (classic college-style JSP + JDBC). It works as a walkthrough of session handling, JDBC access, and page-to-page flow, but it is not production code — see [Caveats](#caveats).

## Stack

- **JSP** (JavaServer Pages) with scriptlets — no framework, no servlets of its own
- **JDBC** via a helper class `vdb.Db` (`Db.connect`, `Db.insert`, `Db.update`, `Db.getSelected`, `Db.getTable`, `Db.deleteTable`)
- **Plain HTML + JavaScript** for the client (timer, form validation)
- Runs on any servlet container (Tomcat, etc.)

Note: the `vdb.Db` class, the `default.css` stylesheet, and the database schema are **not** included in this directory. They are external dependencies the pages assume exist.

## Database tables (inferred from the SQL in the pages)

- `admin` — one row per quiz round: `quizno, noteams, marksperq, negscore, noques, passmarks, maxscore, status`
- `teams` — one row per team: `teamname, marks, status`
- `questions` — question bank: `qno, question, answer, optionA, optionB, optionC, optionD` (columns 1–7 read positionally)

## Page flow

```
adminlogin.jsp        admin login (user/pass)
   ↓
adminduties.jsp       main menu: Start Quiz / Delete Results / Quit
   ↓
startquiz.jsp         enter quiz details (teams, questions, marks, pass marks)
   ↓
save.jsp             writes admin + team rows to DB, shows quiz rules
   ↓
nonpasson.jsp         serves the first question (team 1, question 1)
   ↓
checkanswer.jsp       grades the submitted answer, updates team score
   ↓
next.jsp             serves the next question / rotates to next team
   ↓  (loop until questions run out)
over.jsp             "Quiz Over" → Score
   ↓
score.jsp            score board + winners; offers next round or end
   ↓
nextquiz.jsp          resets for the next round with surviving teams
   ↓
endquiz.jsp → thanks.jsp   clears admin + teams tables, done
```

Diagrams for the same system live alongside the code: `e-r-diagram.png`, `class-diagram.png`, `user-case-diagram.png`, `client-server-architecture.png`, `proposed-system-architecture.png`, `architectural-diagram-of-system-based-on-modules.png`.

## Scoring logic

- Correct answer: team gains `marksperq`.
- Wrong answer: team loses `negscore`, but only if `marks > 0` and the result won't go below zero (score is floored at 0).
- Unanswered questions still count as wrong — the 30-second timer auto-submits the form when it expires (`next.jsp` / `nonpasson.jsp`).
- After a round, `score.jsp` finds `max(marks)`; teams with `marks >= passmarks` advance. If exactly one team qualifies, it's the winner and the quiz ends there.

## Build & run

There is no build file (no `pom.xml` / `build.gradle`) in this directory — it's a loose set of JSPs. To run it you supply the missing pieces and drop the pages into a servlet container:

1. Provide the `vdb.Db` JDBC helper class (compiled onto the container's classpath) and a JDBC driver for your database.
2. Create the `admin`, `teams`, and `questions` tables and populate `questions`.
3. Add a `default.css` (the pages link to it for styling).
4. Copy the `.jsp` files into a web app (e.g. Tomcat `webapps/quiz/`).
5. Start Tomcat and open `http://localhost:8080/quiz/adminlogin.jsp`.

## Usage example

1. Go to `adminlogin.jsp`, log in as admin.
2. On **Start Quiz**, enter e.g. teams = 2, questions = 4, marks for correct = 10, marks for wrong = 5, pass marks = 20. "Calculate Average Marks" computes `(questions / teams) * marksPerCorrect` as a suggested total; the app blocks setup if pass marks exceed that total, or if questions aren't evenly divisible by teams.
3. Save → read the rules → Start Quiz.
4. Each question shows the current team, four options (A–D), and an elapsed-time counter. Pick an answer and hit **Next** (or let the 30s timer submit for you).
5. After the last question, view the **Score Board**, then either play the next round with the surviving teams or end the quiz.

## Caveats

Worth being upfront about, since this is study code:

- **Admin login is broken and client-side only.** The check `(us=="admin")&&(psw="admin")` uses `=` (assignment) instead of `==`, so the password is never actually compared — any login with username `admin` passes. Credentials are also hardcoded in JavaScript, so there's no real authentication.
- **SQL is built by string concatenation** (e.g. `"insert into admin values(" + quiznum + ...)`), which is open to SQL injection and has no prepared statements.
- **`window.navigate(...)`** is used for client-side redirects — that's an old Internet Explorer API and won't work in modern browsers. `change()` / MAIN MENU / QUIT buttons rely on it.
- Errors are swallowed with `catch(Exception e){ System.out.println(e); }` and page state leans heavily on the HTTP session, so a refresh or back-button mid-quiz can desync the flow.
- External dependencies (`vdb.Db`, schema, `default.css`) aren't in this repo, so the app can't run as-is from this directory alone.
