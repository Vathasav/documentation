---
layout: episode
title: "Deploying Sphinx documentation to Read the Docs"
teaching: 5
exercises: 15
questions:
  - How do Python projects deploy their documentation?
  - Can we use their solutions for projects which do not use Python?
objectives:
  - Create a basic workflow which you can take home and adapt for your project.
---

## [Read the Docs](https://readthedocs.org)

- Free Sphinx hosting
- RST or Markdown
- PDF can be generated on the fly
- Equations and images no problem
- Layout can be styled
- Many projects use [Read the Docs](https://readthedocs.org) as their main site
- It is no problem to serve using your own URL `http://myproject.org` instead of `http://myproject.readthedocs.io`

---

## Typical Read the Docs workflow

- Host source code with documentation sources on GitHub.
- Each time you `git push` to the repository, a `post-receive` hook sends POST
  request to Read the Docs to rebuild the documentation.

```shell
$ curl -X POST http://readthedocs.org/build/myproject
```

- Read the Docs then fetches changes (typically from GitHub but can be
  somewhere else provided the repo is public) and rebuilds HTML and PDF.
- No problem to build several branches (versions) of your documentation.

---

## Exercise: Deploy Sphinx documentation to Read the Docs

In this exercise we will host our previously 
created Sphinx documentation on GitHub and deploy it to Read the Docs.
If you haven't created any Sphinx documentation yet, 
an alternative approach is provided below based on forking an example repository.

We will use GitHub for this exercise but it will also work with any Git
repository with public read access.

1. In the first step, create a GitHub repository and push your documentation to it.
2. In the second step, enable the project on Read the Docs

### Step 1: Create a new GitHub repository with your documentation

- Create a new Git repository on your GitHub page called `doc-example`. Do not initiate with README, license or gitignore files. 
- Inside your documentation directory, initiate the repo, add the required files and make your first commit.
- Then add a basic `README.md` and `.gitignore` files (where you ignore the `_build/` directory)
- Finally, add the URL of the remote repository, and push your local repository to GitHub.
- Before looking at the step-by-step instructions below, see if you remember how to do all these steps from the [Git introduction lesson](https://github.com/coderefinery/git-intro).

**Solution below:**


<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


Step-by-step instructions (after creating new repository on GitHub):
```shell
$ cd doc-example
$ git init
$ git add conf.py index.rst feature-a.rst feature-b.rst
$ git commit -m "first commit"
# create a simple README.md file and a .gitignore file where you add _build/
$ git add README.md .gitignore
$ git commit -m "add readme and gitignore"
$ git remote add origin git@github.com:user/doc-example.git  # change user to your GitHub username
# check that it works by `git remote -v`
$ git push origin master
```

#### Alternative approach: Make a copy (fork) of the [example repository](https://github.com/coderefinery/doc-example)

Fork [this repository](https://github.com/coderefinery/doc-example) and
then clone the fork to your laptop:

```shell
$ git clone git@github.com:user/doc-example.git  # adapt user, also ok to clone via https if you prefer
$ cd doc-example
```

#### Build HTML pages locally

If you already created your first Sphinx documentation in the [preceding episode](https://coderefinery.github.io/documentation/04-sphinx/), you can skip this step and proceed to the next section. 

Inside your documentation directory (or the cloned repository), run `sphinx-build . _build`.
Then point your browser to e.g.
`file:///home/user/doc-example/_build/index.html`. Adapt the path to the actual
path where you have cloned to (the `/home/user` part is almost certainly wrong in your case).


### Step 2: Enable the project on [Read the Docs](https://readthedocs.org)

Now you will import a project to Read the Docs by connecting to GitHub.  This
will automatically set up a webhook on GitHub and webhook integration on Read
the Docs so that `git push` will automatically rebuild the Read the Docs site.
One can also manually import the project to Read the Docs and set up the
webhook on GitHub, along with webhook integration on Read the Docs, but this
will not be needed here.

- Log into [Read the Docs](https://readthedocs.org) and visit your [dashboard](https://readthedocs.org/dashboard/)
- Click "Import a Project"
- Select "Connect to GitHub", and choose the doc-example repository
- Click "Next"

That's it! Your site should now be live on
[http://user-doc-example.readthedocs.io](http://user-doc-example.readthedocs.io)
(replace project name).

Finally, make some changes to your documentation, commit and push
them, and verify that the documentation website refreshes after your changes
(can take few seconds or a minute).

