Setting up Your Hypothesis Development Environment
==================================================

Set up your GitHub account and SSH key
--------------------------------------

You need to be able to `git clone` private repositories from the
[hypothesis organization on GitHub](https://github.com/hypothesis/):

1. [Sign up for a free GitHub account](https://github.com/signup) if you don't already have one
2. Get someone to add your GitHub account to the `hypothesis` organization if it hasn't already been added
3. [Set up an SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
   for git to use to authenticate to GitHub

Install prerequisites
---------------------

You'll need:

1. [Git](https://git-scm.com/)
2. [Node.js](https://nodejs.org/en/)
3. [Yarn 1 (Classic)](https://classic.yarnpkg.com/)
4. [Docker](https://www.docker.com/)
5. [pyenv](https://github.com/pyenv/pyenv)
6. [GNU Make](https://www.gnu.org/software/make/)
7. [pg_config](https://www.postgresql.org/docs/current/app-pgconfig.html)

<details>
<summary>Installing the prerequisites on macOS</summary>

1. Install [Homebrew](https://brew.sh/)
2. Run:
   ```terminal
   brew install git node postgresql pyenv
   npm install --global yarn
   ```
3. Follow [Docker's install instructions](https://docs.docker.com/get-docker/). You **don't** need to install Docker Compose
4. Follow pyenv's instructions to [set up your shell for pyenv](https://github.com/pyenv/pyenv#set-up-your-shell-environment-for-pyenv)
5. Follow pyenv's instructions to [install Python build dependencies](https://github.com/pyenv/pyenv/wiki#suggested-build-environment)
</details>

<details>
<summary>Installing the prerequisites on Ubuntu</summary>

1. Run:
   ```terminal
   sudo apt install git make libpq-dev
   sudo snap install --classic node
   ```
2. Follow [Docker's install instructions](https://docs.docker.com/get-docker/) including the [Post-installation steps for Linux](https://docs.docker.com/engine/install/linux-postinstall/). You **don't** need to install Docker Compose
3. Follow [pyenv's installation instructions](https://github.com/pyenv/pyenv#installation):
   1. The [Basic GitHub Checkout](https://github.com/pyenv/pyenv#basic-github-checkout) method works best on Ubuntu
   2. [Set up your shell](https://github.com/pyenv/pyenv#set-up-your-shell-environment-for-pyenv) for pyenv
   3. [Install the Python build dependencies](https://github.com/pyenv/pyenv/wiki#suggested-build-environment)
      that pyenv needs
</details>

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

[Via](https://github.com/hypothesis/viahtml) is a proxy that injects the client
into arbitrary PDFs. To install and run it:

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

[Via HTML](https://github.com/hypothesis/viahtml) is the component that handles
HTML pages for Via.  To install and run it:

```terminal
git clone https://github.com/hypothesis/viahtml.git
cd viahtml
make devdata
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
