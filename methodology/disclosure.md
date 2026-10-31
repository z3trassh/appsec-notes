# Coordinated disclosure

How I handle a finding once it is confirmed.

## Before I report

- Check the program's policy or the vendor's `security.txt` for the right
  channel and any safe-harbour terms.
- Stop at proof of impact. I do not read more data than one record needed to show
  the bug, and I delete any test data I created.

## The report

- One finding per report, with the write-up template filled in.
- Enough detail to reproduce: endpoint, steps, and a minimal proof of concept.
- The impact in plain terms, and the fix I would expect.

## Timeline

- Give the vendor a reasonable window to fix before any public write-up —
  90 days is my default, longer if they are engaging and need it.
- Agree the disclosure date with them. Publish the write-up only after the fix
  ships or the window passes, and only if the program allows public disclosure.
- Never publish customer data, credentials, or a working exploit against a live
  service.

## Public write-up

When a write-up goes public, it keeps the target anonymous unless the vendor
agreed otherwise, drops any live payload, and explains the fix so the next person
builds it right.
