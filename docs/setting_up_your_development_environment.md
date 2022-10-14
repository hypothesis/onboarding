Setting up Your Hypothesis Development Environment
==================================================

This guide will walk you through setting up your Hypothesis development environment: installing everything and getting the apps running locally.

You will need
-------------

1. A GitHub.com account that is a member of the `hypothesis` organization. If you've been hired by Hypothesis this should already have been set up for you.

Install prerequisites
---------------------

You need to install:

1. [Git](https://git-scm.com/)
2. [GitHub CLI](https://cli.github.com/)
3. [Node.js](https://nodejs.org/en/)
4. [Yarn 1 (Classic)](https://classic.yarnpkg.com/)
5. [Docker](https://www.docker.com/)
6. [pyenv](https://github.com/pyenv/pyenv)
7. [GNU Make](https://www.gnu.org/software/make/)
8. [pg_config](https://www.postgresql.org/docs/current/app-pgconfig.html)

<details>
<summary>Installing the prerequisites on macOS</summary>

1. Install [Homebrew](https://brew.sh/)
2. Run:
   ```terminal
   brew install git gh node postgresql pyenv
   npm install --global yarn
   ```
3. Follow [Docker's install instructions](https://docs.docker.com/get-docker/). You **don't** need to install Docker Compose
4. Install pyenv's shell integration and build dependencies. The `brew` command above will have installed pyenv itself but you still need to:
   1. Follow pyenv's instructions to [set up your shell for pyenv](https://github.com/pyenv/pyenv#set-up-your-shell-environment-for-pyenv)
   2. Follow pyenv's instructions to [install Python build dependencies](https://github.com/pyenv/pyenv/wiki#suggested-build-environment)
</details>

<details>
<summary>Installing the prerequisites on Ubuntu</summary>

1. Run:
   ```terminal
   sudo apt install git make libpq-dev
   ```
2. Follow [NodeSource's instructions](https://github.com/nodesource/distributions/blob/master/README.md#installation-instructions)
   to install their Node.js Debian/Ubuntu package
3. Enable Corepack in order to get the `yarn` command
   (as in [Yarn's install instructions](https://yarnpkg.com/getting-started/install)):
   ```terminal
   sudo corepack enable
   ```
4. Follow [GitHub CLI's install instructions](https://cli.github.com/)
5. Follow [Docker's install instructions](https://docs.docker.com/get-docker/) including the [Post-installation steps for Linux](https://docs.docker.com/engine/install/linux-postinstall/). You **don't** need to install Docker Compose
6. Follow [pyenv's installation instructions](https://github.com/pyenv/pyenv#installation):
   1. The [Basic GitHub Checkout](https://github.com/pyenv/pyenv#basic-github-checkout) method works best on Ubuntu
   2. [Set up your shell](https://github.com/pyenv/pyenv#set-up-your-shell-environment-for-pyenv) for pyenv
   3. [Install the Python build dependencies](https://github.com/pyenv/pyenv/wiki#suggested-build-environment)
      that pyenv needs
</details>

Set up Git &rarr; GitHub.com authentication
-------------------------------------------

Set up Git to authenticate requests to GitHub.com using your GitHub.com account.
The easiest way to do this is to run GitHub CLI's [`gh auth login` command](https://cli.github.com/manual/gh_auth_login) and answer **Yes** (the default answer) when it asks **Authenticate Git with your GitHub credentials?**

```terminal
gh auth login -p https -h github.com
```

Install the Hypothesis apps
---------------------------

### h

[github.com/hypothesis/h](https://github.com/hypothesis/h/) is the main
annotation API service that all the other apps talk to. To install and run it:

```terminal
git clone https://github.com/hypothesis/h.git
cd h
make services
make devdata
make dev
```

You should now be able to open http://localhost:5000/login and log in with
username `devdata_user` and password `pass`.

<details>
<summary>What is <code>make services</code>?</summary>

An app's `make services` command starts the services that the app requires
(things like Postgres and Elasticsearch) in Docker Compose.  `make services`
generally needs to be re-run each time you restart your computer.
</details>

<details>
<summary>What is <code>make devdata</code>?</summary>

An app's `make devdata` command loads development data from the [our devdata
repo](https://github.com/hypothesis/devdata) into the app's database and
environment variables. `make devdata` doesn't generally need to be re-run
unless we update the devdata repo.
</details>

<details>
<summary>What is <code>make dev</code>?</summary>

An app's `make dev` command is what starts the app. For example a web app like h will
be running and accepting HTTP requests on its localhost port (5000 in h's case)
when the app's `make dev` command is running.
</details>

#### Troubleshooting

##### Connection in use: ('0.0.0.0', 5000)

macOS's AirPlay Receiver uses port 5000. If you're on macOS and you get a
`Connection in use: ('0.0.0.0', 5000)` error when running `make` commands in h
then go to <kbd>System Preferences &rarr; Sharing</kbd> and un-check
<samp>AirPlay Receiver</samp>.

### Client

[github.com/hypothesis/client](https://github.com/hypothesis/client) is the frontend app that provides
a sidebar for reading and writing annotations over web pages or PDFs. To
install and run it:

```terminal
git clone https://github.com/hypothesis/client.git
cd client
make dev
```

You should now be able to open http://localhost:3000/ and see an HTML page with
the client sidebar embedded. You should be able to log in to the client and
annotate the test page. If it asks for a username and password you can use
`devdata_user` and `pass`.

### Via

[Via](https://github.com/hypothesis/via) is a proxy that injects the Hypothesis client
into PDFs so users can annotate them. To install and run it:

```terminal
git clone https://github.com/hypothesis/via.git
cd via
make services
make devdata
make dev
```

You should now be able to visit <http://localhost:9083/>, paste in the URL
of a PDF (like [this one](https://en.wikipedia.org/api/rest_v1/page/pdf/Comet_Kohoutek)),
see the PDF, and annotate it with the injected client sidebar.

### Via HTML

[Via HTML](https://github.com/hypothesis/viahtml) is a proxy that injects the Hypothesis client
into HTML pages so users can annotate them. To install and run it:

```terminal
git clone https://github.com/hypothesis/viahtml.git
cd viahtml
make services
make dev
```

You should now be able to visit <http://localhost:9083/> again, paste in the
URL of a web page (like [this one](https://en.wikipedia.org/wiki/Pantala_flavescens)),
and annotate it with the injected client sidebar.

### LMS

[LMS](https://github.com/hypothesis/lms) integrates Hypothesis into Learning
Management Systems like Canvas, Blackboard, Moodle and others. To install and
run it:

```terminal
git clone https://github.com/hypothesis/lms.git
cd lms
make services
make devdata
make dev
```

You should now be able to visit
<https://hypothesis.instructure.com/login/canvas> (our test Canvas instance),
log in using **Canvas: Instructor (Testing Account)** (the username and
password are in 1Password) visit [Developer Test Course with Sections Enabled](https://hypothesis.instructure.com/courses/125),
load localhost test assignments like
[localhost (make devdata) HTML Assignment](https://hypothesis.instructure.com/courses/125/assignments/873),
and annotate the assignment web pages and PDFs.

Other things to do
------------------

1. Make sure that the tests, linting and code formatting are all passing.
   In each project run:

   ```terminal
   make sure
   ```

2. Explore other development environment commands.
   In each project run:

   ```terminal
   make help
   ```
