Writing Commits and Pull Requests
=================================

Small, atomic commits and pull requests (PRs) with helpful commit messages,
PR titles and PR bodies are great for collaboration and key to a maintainable
project. Tools like [`git rebase`](https://docs.github.com/en/get-started/using-git/using-git-rebase-on-the-command-line)
can help you to rewrite commits and split up branches to tell a clean and coherent story.

Make small PRs and atomic commits
---------------------------------

A good guide is that each PR should do "one thing": a single logical change.
Needing "and" in your PR title might be a sign that you should split it up. If
you discover a bug while adding a new feature, send a separate PR to
fix the bug. If code doesn't follow current conventions do a refactoring commit
first then a separate commit to make your functional change. We like small PRs
because:

* They're necessary for [continuous deployment](merging.md): you can't deploy a small diff without first merging a small PR.
* They get faster, better reviews: it takes less time and context-switching to review a small, focused PR.
* They improve the quality of your work by encouraging clearly organized thinking, modular code, and purity of purpose.

Make commits atomic: CI should be passing after each commit to make tools like
`git revert` and `git bisect` effective and history easier to navigate (no
"fix", "typo" and "test" commits).

<details><summary><b>When should you include more than one commit in a PR?</b></summary>
If a few closely related commits would be easier to review and deploy together
then you might want to include them in the same PR.
If commits can be decoupled into independently-reviewable, smaller PRs then it
might be better to split them up.
</details>

Write helpful commit messages, PR titles, and PR bodies
-------------------------------------------------------

Good commit messages make tools like `git blame`, `git revert` and `git log`
come to life. Good titles and bodies make PRs easier to review by explaining
your intent, reasoning and context rather than making your reviewer figure it
out.

[Every line of code is always documented](https://mislav.net/2014/02/hidden-documentation/):
write to explain your change to the whole team, not just the individual who'll review it.
Enable future code archaeology: make it possible to understand and revisit your
change months or years from now.

As with breaking changes into atomic commits and small PRs, writing good commit
and PR messages improves the quality of your work: it's a self-review that helps
you clearly organize your thoughts and understand what you've done and whether
it really solves the problem.

#### What should go in commit and PR messages?

A commit's diff shows **how** the change was made: what lines of code were
changed. It's up to the commit message to document **what you intended** the
commit to achieve, **why** you're making this change, and any **context**
or background knowledge necessary to understand the change.
[My favourite Git commit](https://dhwthompson.com/2019/my-favourite-git-commit) (written by a former Hypothesis developer)
and [Telling stories through your commits](https://blog.mocoso.co.uk/talks/2015/01/12/telling-stories-through-your-commits/)
have some great tips.

The first line of a commit should summarize the intent in less than 50 chars
because it works well with Git and GitHub which treat the first line as a title
and use it throughout their interfaces.
Use the [imperative mood](https://en.wikipedia.org/wiki/Imperative_mood) because it's short and clear.[^1]

For single-commit PRs GitHub pre-fills the title and body from the commit
message. You might add some more details yourself: screenshots, testing
instructions, review notes. Multi-commit PR titles can follow the same style as
for single commits[^2], the PR title and body can document the PR as a whole
while commit messages can add detail to individual commits.

[^1]: Using the imperative mood means writing your commit title as if giving
  the code a command to change itself, for example
  <b>Refactor foo service for readability</b> (not <q>Foo service refactoring</q>) or
  <b>Fix crash when creating user with long name</b> (not <q>Fixed...</q> or <q>This fixes...</q> etc).
  This matches the style of automated commit messages:
  <b>Revert <code><title_of_earlier_commit></code>"</b> (from `git revert`),
  <b>Merge pull request #2371</b> (from GitHub's merge button),
  <b>Bump marshmallow from 3.17.1 to 3.18.0a</b> (from Dependabot).

[^2]: GitHub pre-fills multi-commit PR titles from the **branch name**,
  capitalising the first letter and replacing dashes with spaces,
  so a good style is to name branches like PR titles:
  summarize the intent in imperative mood in less than 50 chars, but in
  lower-case and with dashes for spaces:
  `refactor-foo-service-for-readability`,
  `fix-crash-when-creating-user-with-long-name`.
  This makes for descriptive branch names that aren't too long or short and
  that match their PR titles.
  It doesn't require you to be clairvoyant about knowing what the PR title will
  be before you create the local branch: you can always rename the branch
  before pushing with `git branch --move <new_name>`.

Respond collaboratively to reviews
----------------------------------

Respond graciously to critiques:
appreciate your reviewer's effort,
see review notes as objective discussion and helpful lessons,
be patient and polite,
and try not to get defensive.
Michael Lynch's [How to Make Your Code Reviewer Fall in Love with You](https://mtlynch.io/code-review-love/)
has some great advice for this.