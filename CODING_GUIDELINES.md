# Coding Guidelines

The **fraud-moving-sellers-op** is a collaborative effort from the start. The application's team thinks that contributions from different developer will
enrich it's feature set and make it more relevant to the community.

The purpose of this guide is to set a baseline for contributions. These guidelines are not intended to limit the tools at your disposal nor
to rewire the way you think but rather to encourage good neighbor behavior.

This documentation is based on the one produced in the [fury_python-melitk-metrics](https://github.com/mercadolibre/fury_python-melitk-metrics) application.

## Language Guidelines

We use **english** language. This is to be consistent everywhere, and to be considerate with developers that do not speak our native language.

Therefore: source code, comments, documentation, commit messages, review comments, and any other kind of contribution *MUST* use english language.

Typos are unavoidable, but try to reduce them by using a spellchecker. Most IDEs can be configured to run one automatically.

## Code Guidelines

* Follow the [Java](https://furydocs.io/code-quality/3.4.2/guide/#/languages/java) [Code Quality](https://furydocs.io/code-quality/guide/#/)
  standards (linting, styling and code smells).
* Always add docstrings to modules, classes and functions.
* Follow (as best as possible) [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html).
* We also took some elements from [Oracle's](https://www.oracle.com/technetwork/java/codeconventions-150003.pdf) ruleset.
* When writing Markdown documents, follow the [markdownlint](https://github.com/DavidAnson/markdownlint) rules. Is possible to integrate it
  with editors or you can use the [cli](https://github.com/igorshubovych/markdownlint-cli).


This rules will be enforced automatically when making a pull requests, and checks will fail if you do not follow them, resulting in your
contribution being automatically rejected until fixed.

## Comment Guidelines

Comments in code are a hard thing to write, not because the words are difficult to produce but because it is hard to make relevant comments.
Too much of it and people do not read comments (and it obfuscates code reading) and too little of it gives you no recourse but to read large
portions of codebase to get insight as to what a feature/codeblock is doing. Both situations are undesirable and efforts should be made at
all time to have a please comment reading experience.

As a general rule you would have to comment on decisions you made while coding that are not part of any specification.

In particular you should always comment any decision that:

* Departs from common wisdom or convention (The **why's** are necessary).
* Takes a significant amount of time to produce. A good rule of thumb here is that if you spent more than 1 hour thinking on how to produce a
  fragment of code that took 2 minutes of wrist time to write you should document your thinking to aid reader and allow for validation.
* Need to preserve properties of the implementation. This is the case of performance sensitive portions of the codebase, synchronization,
  implementations of security primitives, congestion control algorithms, etc.

As a general rule of what not to comment you should avoid:

* Commenting on structure of programs that is already part of a convention, specified or otherwise.
* Having pedantic explanations of behavior that can be found by immediate examination of the surrounding code artifacts.
* Commenting on behavior you cannot attest.

### Branching Guidelines

Currently `master` is our only long term branch and here resides the latest productive codebase.
Follow the work flow [Libflow](https://furydocs.io/release-process/guide/#/lang-es/workflows/04_libflow).

### Git Guidelines

We follow [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) specification to apply in commit messages.
Also all commits **SHOULD** follow the [seven rules of a great Git commit message](https://chris.beams.io/posts/git-commit):

1. Separate subject from body with a blank line.
2. Limit the subject line to 72 characters.
3. Capitalize the subject line.
4. Do not end the subject line with a period.
5. Use the imperative mood in the subject line.
6. Wrap the body at 72 characters.
7. Use the body to explain what and why vs. how.

Commits such as "fix tests", "now it's working" and many other common messages we find usually in code **WON'T** be accepted.

Ideally we would like to enforce these rules, but we are realistic and understand that it might be a big change for some people.
So unless deviating heavily from what was stated we might accept your commits even if not following these rules perfectly.

Please avoid taking to much time to deliver code, and always [rebase](https://git-scm.com/docs/git-rebase) your code to avoid reverse merge
commits.

