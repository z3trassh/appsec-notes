# Web testing methodology

The order I work through a web target I am authorized to test. It is a checklist,
not a script: I stop and go deep whenever something answers in an unexpected way.

## 1. Scope and ground rules

- Confirm the scope in writing: hosts, apps, accounts, what is out of bounds.
- Note the rate limits and the test window the program allows.
- Set up two accounts at different privilege levels; most access-control bugs
  need a second identity to prove.

## 2. Map the application

- Walk every feature as a normal user. Record each endpoint, parameter, and the
  identity it answers for.
- List the trust boundaries: browser to server, service to service, server to
  third party.
- Note where the app fetches a URL, renders user input, or makes an authz
  decision. These are where I return later.

## 3. Test by bug class

For each class I keep one question and the fix I expect to see:

| Class | Question | Expected fix |
| --- | --- | --- |
| Access control (BOLA/IDOR) | Can one user reach another's object by id? | Ownership check on every object load |
| Authentication | Can I forge or replay a token? | Server pins the algorithm and validates fully |
| SSRF | Can I make the server request an internal host? | Parse and validate the host; block private ranges |
| Injection | Does input reach a query, template, or shell? | Parameterised APIs, context-aware encoding |
| Race conditions | Does a check-then-act break under concurrency? | Atomic update or a lock |
| Business logic | Can I reach a state the flow should forbid? | Server enforces the state machine |

## 4. Confirm and measure impact

- Reproduce from a clean state, in the fewest steps.
- State impact in terms of what data or action it exposes, not the payload.
- Keep the smallest proof. No mass extraction, no pivoting beyond what shows the
  bug.

## 5. Report

Fill in [the write-up template](../templates/writeup.md) and follow the
[disclosure notes](disclosure.md).
