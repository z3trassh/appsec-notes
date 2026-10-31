# appsec-notes

How I approach web security work: a reusable testing methodology, a disclosure
write-up template, and short notes on bug classes I keep meeting. These are
working notes, not a textbook — they say how I actually test and report.

## Contents

- [methodology/web-testing.md](methodology/web-testing.md) — the checklist I run on a web target, in order
- [methodology/disclosure.md](methodology/disclosure.md) — how I report and coordinate a finding
- [templates/writeup.md](templates/writeup.md) — the write-up template I fill in for each finding
- [notes/](notes/) — one page per bug class, each tied to a lab in [web-vuln-labs](https://github.com/z3trassh/web-vuln-labs)

## Principles

- Only test what you are authorized to test, and keep proof to the minimum that
  shows impact.
- A finding is not real until it is reproduced from a clean state.
- Report the fix, not just the break. A write-up without a remediation is half a
  write-up.

## License

Prose under [CC BY 4.0](LICENSE). Reuse the templates freely.
