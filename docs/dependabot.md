Dependabot at Hypothesis
========================

We use [Dependabot](https://github.com/dependabot) to keep all our dependencies
up to date: it sends [automated pull requests][1] (PRs) to update the versions
of project dependencies like Python and JavaScript packages, Docker base
images, and actions from the GitHub Actions marketplace.

Why keep dependencies up to date?
---------------------------------

**The latest version is usually the greatest**:
new releases have new features, better security
(see [early research by Dependabot](https://web.archive.org/web/20190523170608/https://dependabot.com/blog/the-latest-dependency-version-is-probably-the-most-secure/)),
and more bug fixes. Developers want access to new language, framework and
library features, and we want to get improvements to users quickly.

We prefer to [**ship small changes, frequently**](https://hyp.is/I3ILSBf3Ee2PtgdQobKl1A/web.hypothes.is/jobs/engineering-values/).
Dependabot applies this to updating dependencies.
A small step from Pyramid 2.0 to 2.1 is easier than a big leap from 0.7 to
2.1: smaller changelogs mean less work and less chance of missing a bug.
Big leaps often require big upgrades to the dependencies-of-the-dependency as
well, even more work. If we're using an old version of a dependency when an
important fix is released only for newer versions then we could be forced to
rush a big upgrade under duress.

Being [conservative about adding new technology to our stack](dependencies.md)
helps to make reviewing Dependabot PRs more manageable.

See also: [Why bother keeping dependencies up-to-date?](https://web.archive.org/web/20190523170606/https://dependabot.com/blog/why-bother/)
from the original Dependabot blog.

How do I handle a Dependabot PR?
--------------------------------

Every developer is responsible for handling their fair share of Dependabot PRs.
To deal with a Dependabot PR you should:

1. Check whether CI passed on the PR.
   If CI failed the update likely breaks something that needs to be fixed.
2. Figure out what the project uses this dependency for.
   This will help you to know what to look out for in the dependency's
   changelog and where to focus any manual testing.
3. Read the changelog entry for the new version of the dependency.
   Does it mention any potentially breaking changes that might affect us? If so
   review and test the code that uses the dependency and verify whether
   everything still works.
4. If applicable, manually test the features of our project that make use of
   the dependency.

If all looks well then go ahead and merge the PR then deploy or release the
project. See our [docs about merging PRs](merging.md) for details.

### If the update breaks something

If the update breaks something you may need to fix our code to work with the
new version before merging the PR. Push your commits to the Dependabot PR
branch and get someone else to review your work before merging and deploying it.

**If the dependency itself has a bug** in the new version that affects us then
you may need to update our code to work around the bug. Alternatively you might
decide to skip this version: just close the PR without merging it, Dependabot
will send another PR when the next version of the library is released and
hopefully the bug will be fixed.

### Tactics for handling Dependabot PRs

**Delegate**: if you're not sure about a pull request feel free to ping a
developer who knows that area of the code and delegate it to them.

**Delay**: most Dependabot updates don't need to be deployed immediately. You
can leave them until the end of the week.  PRs with the `security` label
shouldn't be delayed.

**Ignore**: you can **close a Dependabot PR** and it will not send us another
PR for that version of that dependency, but will send us a PR for the next
version.  It's fine to close Dependabot PRs as long as we don't do it for
`security`-labelled upgrades and don't do it for too many consecutive versions
of a given dependency (we don't want to end up on a really old version).

**Remove**: should this dependency be removed from our project, perhaps
replacing it with some code of our own? If a dependency adds little value and
frequently releases new versions that're problematic to upgrade to then it may
make sense to remove the dependency.

**Schedule**: sometimes it's a big job to upgrade to a new version of a
dependency. It might make sense to schedule the work for the next sprint.

[1]: https://github.com/pulls?q=org%3Ahypothesis+is%3Aopen+is%3Apr+sort%3Acreated+label%3Adependencies+ "All open pull requests labelled 'dependencies'"
