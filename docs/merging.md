Merging a Pull Request
======================

Your code isn't really working until it's working in production. Developers at
Hypothesis are empowered (and required) to merge their own pull requests (PRs)
and verify that their changes work once deployed or released.

When you merge changes into a project, you're not done yet. Your changes need
to be deployed or released:

* **PRs merged into web apps** are automatically deployed to a QA environment
  where it is your responsibility to test them and deploy them to production
  without delay. See [our deploying docs](https://github.com/hypothesis/playbook/blob/main/docs/deploying.md)
  for details. Leaving undeployed commits on QA can slow down the next
  developer — who might be trying to deploy urgent changes — as their commits
  can't be deployed without also deploying yours.
* After **merging PRs into other projects**, you may need to release a version
  of that project. Instructions can be found in each project's `README`.

We ship working code incrementally ("continuous deployment") instead of trying
to release months of work all at once. You'll release or deploy a project right
after merging each PR or small batch of PRs. Deploying a single small PR
individually is typical. We do it this way because:

* We want to [get features and fixes to users fast](https://hyp.is/I3ILSBf3Ee2PtgdQobKl1A/web.hypothes.is/jobs/engineering-values/)
  and avoid giant leaps in the wrong direction.

* The best way to limit the risk of deploying code is to do it as often as
  possible. We know that our deployment mechanism is quick and safe because we
  use it many times a day.

* [The most plausible answer to "what went wrong" is usually "the last thing we changed."](https://blog.skyliner.io/ship-small-diffs-741308bec0d1)
  When a deployment breaks something it's easier to pinpoint the problem if the
  diff you just deployed was a handful of lines rather than thousands.
