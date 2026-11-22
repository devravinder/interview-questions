# Senior Full Stack Scenarios

Read these first; this file adds only what they don't cover:

- [HR / behavioral questions](questions.md): job change, strengths, conflicts, pressure, situational questions
- [Mock interview](../java/mock-interview.md): project walk-through, architecture, slow API in production
- [Senior developer topics](../system-design/senior-dev.md): leadership skills, trade-offs

## Design and ownership

1. Tell me about a technical decision you made that turned out wrong. How did you find out and what did you do?
2. How do you decide between building something and using an existing library or service?
3. How do you estimate a large feature that touches the frontend, backend and database?
4. How do you handle technical debt while the business wants features?
   - Tie debt to a cost the business sees (incidents, slow delivery), and fix it in small steps inside feature work.
5. How do you design an API that both a React app and mobile apps use?

## Production and quality

1. Tell me about the hardest production incident you handled. What was the root cause and what changed after?
2. How do you make sure a feature works in production, not just in tests?
   - Metrics and alerts for the feature, feature flags, canary release, and checking real usage after launch.
3. How do you improve a slow page end to end, from the browser to the database?

## Working with people

1. A product manager asks for a deadline you think is unrealistic. How do you respond?
2. How do you onboard yourself onto a large unfamiliar codebase quickly?
3. How do you share knowledge across a team? (design docs, ADRs, pairing, short talks)

## Questions to ask the interviewer

1. What does a typical release look like, from merge to production?
2. How are on-call and incidents handled?
3. What is the biggest technical problem the team has right now?
4. How are technical decisions made and written down?
