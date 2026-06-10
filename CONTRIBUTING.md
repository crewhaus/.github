# Contributing to CrewHaus

Thanks for considering a contribution. This is the org-wide guide; it routes you to the right repository and covers the rules that apply everywhere. The compiler repo has its own, much more detailed guide — [`factory/CONTRIBUTING.md`](https://github.com/crewhaus/factory/blob/main/CONTRIBUTING.md) — which governs anything touching compiler code.

## Where to contribute

| You want to change... | Go to |
|---|---|
| The compiler, emitters, IR, eval loop, security fabric, CLI | [`factory`](https://github.com/crewhaus/factory) — read its [CONTRIBUTING.md](https://github.com/crewhaus/factory/blob/main/CONTRIBUTING.md) first |
| Guides, references, module briefs, the whitepaper | [`docs`](https://github.com/crewhaus/docs) |
| Runnable starters and walkthroughs | [`demos`](https://github.com/crewhaus/demos) |
| Studio, visualizers, playground, IDE integrations | [`utilities`](https://github.com/crewhaus/utilities) |

Not sure where something belongs? Open an issue on [`factory`](https://github.com/crewhaus/factory/issues) and we'll route it.

## Rules that apply in every repo

- **Code of Conduct.** The [Contributor Covenant 2.1](CODE_OF_CONDUCT.md) applies in all community spaces.
- **Issue first.** For anything more than a typo fix or a small, obvious bug fix, open an issue before writing code. We close PRs that didn't get pre-aligned, even when the code is good — the change might conflict with planned architecture, and we don't want to waste your time.
- **DCO sign-off.** Every commit needs `Signed-off-by: Your Name <email>` (`git commit -s`). This is the [Developer Certificate of Origin](https://developercertificate.org/) — a lightweight alternative to a CLA.
- **Conventional Commits.** Use [Conventional Commits](https://www.conventionalcommits.org/) prefixes (`feat:`, `fix:`, `docs:`, `chore:`, ...) in commit messages and PR titles.
- **Security reports are private.** Never file a vulnerability as a public issue — see [SECURITY.md](SECURITY.md).

## Licensing

Code contributions are licensed under [Apache-2.0](https://github.com/crewhaus/factory/blob/main/LICENSE), matching the codebase. Documentation (including the whitepaper) is [CC-BY-4.0](https://github.com/crewhaus/docs/blob/main/whitepaper/LICENSE). The DCO sign-off is your assertion that you have the right to make that license grant.

## Support expectations

CrewHaus is maintained at side-project pace; support is async-first and bounded. [SUPPORT.md](SUPPORT.md) explains the channels and what response times to expect.

---

Thanks for contributing. We mean it.
