# How do we decide when to add a new technology?

How do we decide when to add new tech to our stack,
like a new Python or JavaScript package,
or a new database or alerting system?
 
Adding a dependency can save us significant development and
maintenance time: we don't want to implement things that are already
well-solved by the ecosystem. But each dependency is also one more thing that
Hypothesis developers need to learn, and we'll always have to keep it up to
date. 
[New problems don't typically require new technology or architectures.](https://hyp.is/-LfAyByIEe2Ws3_8PLlVpA/web.hypothes.is/jobs/engineering-values/)

[We want a small number of high quality, well-maintained, mature technologies](https://boringtechnology.club/)
that are easy to learn and keep up to date, not a large number of poorly
maintained dependencies that are hard to use and frequently cause problems.

When proposing to add a new dependency to a project you should:

* Discuss the new dependency with other developers.

  Always ask how you'd solve your immediate problem without adding anything new.
  Write down exactly what about the current stack makes solving the problem prohibitively expensive and difficult.
  Does it outweigh the costs of adding the new technology?

* Send a pull request (PR) that adds the new dependency, explaining in the PR description the motivation for adding the new dependency

## Guidelines

Some guidelines for deciding whether to add a new technology:

### Consistency speeds everyone up

There's are many good reasons to use the same stack to solve the same problems in different projects, here's just a few:

* **Cognitive load reduction**: Hypothesis developers only need to learn one thing, not multiple.
* **Maintenance load reduction**:  when the dependency releases a new version you only need to read the
  changelog once to update all our projects. No need to deal with all the breaking changes from new releases of multiple projects when one
  would have sufficed.
* **Operational load reduction**: deployment, monitoring, scaling, backups. Learning how to operate a stack effectively is hard.

### Adding a new dependency might be a good idea if...

* **We already use the dependency** in other Hypothesis projects.
* It **solves a significant problem**, making carrying this dependency worth the cost.
* It's **widely used**. This is a sign of maturity, could imply better support, and new developers are more likely to be familiar with the project.
* It's **actively maintained**, with regular releases and good changelogs.
* It has **good documentation**, making it easier to learn and use.  
 * Python packages should **document what versions of Python they support**, this makes upgrading our Python version easier.
* It **works with our existing technology stack** (e.g. supports our web framework or build tooling),
  and is easy to integrate into our projects.
* It will be **easy to remove** if we change our minds.

### Adding a new dependency might **not** be a good idea if...

* **We already use another dependency** to solve the same problem in this or another project.
* **It solves only a trivial problem**.
  Would it be cheaper to write our own code and maintain that?
* It would mean **using a big, complex technology to solve a small, simple problem**.
  The cost of Hypothesis developers having to learn the technology might
  outweigh the benefits.
* It would introduce **architectural complexity** (for example adding
  a message queue server). This greatly increases the cost.
