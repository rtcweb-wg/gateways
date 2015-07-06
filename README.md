# Internet Draft Template Repository

The contents of this repository can be used to get started with a new internet
draft.

## Getting Started

This all assumes that you have an [account](https://github.com/join) with
GitHub.

### Working Group Setup

Make a [new organization](https://github.com/organizations/new) for your working
group.  This guide will use the name `unicorn-wg` for your working group.

### New Draft Setup

[Make a new repository](https://github.com/new).  This guide will use the
name name `unicorn-protocol` here.

Clone that repository:
```sh
$ git clone https://github.com/unicorn-wg/unicorn-protocol.git
```
Copy the contents of this respository in:
```sh
$ cd unicorn-protocol
$ git pull https://github.com/martinthomson/i-d-template.git master
```
Choose whether you want to use markdown, outline, or xml as your input form.
If you already have a draft, then that decision is already made for you.

Move the template file into place.
```sh
$ git mv template.md draft-ietf-unicorn-protocol.md
```
Or add an existing file.
```sh
$ git add draft-ietf-unicorn-protocol.xml
````
Edit the draft so that it has the right name.  This template uses the
`-latest` suffix in place of the usual number ('-00', or '-08').
```xml
   <rfc docName="draft-ietf-unicorn-protocol-latest" category="std">
```
Or in markdown:
```yaml
docname: draft-ietf-unicorn-protocol-latest
```
And add it:
```sh
$ git add draft-ietf-unicorn-protocol.md
```
Remove the unnecessary template files.
```sh
$ git rm template.md template.xml
```
Move the README.md template into place.
```sh
$ git rm README.md
$ git mv README-template.md README.md
```
Edit the `README.md` and `CONTRIBUTING.md` files.  Note that `CONTRIBUTING.md`
file is just the latter part of `README.md`.
```sh
$ vi README.md CONTRIBUTING.md
# ...
$ git add README.md CONTRIBUTING.md
```
Commit and push
```sh
$ git commit
$ git push
```

Optional: If you are using markdown, you might like to add the following line to your
`.gitignore` to avoid committing the intermediate XML file that this might create.
```
draft-*.xml
```


### Setting Up The Editor's Copy

GitHub uses the `gh-pages` branch as source for a project web page.  This branch
needs to be initialized first.  The `setup-ghpages` make target does that:

```sh
$ make setup-ghpages
```

You can maintain `gh-pages` manually by running the following command
occasionally.

```sh
$ make ghpages
```

Or, you can run an automatic commit after each checkin with Travis.


### Automatic Update for Editor's Copy

This requires that you sign in with [Travis](https://travis-ci.org/).

First enable builds for the new repository on the Travis site.  (Hit the button
with a '+' on it once you are logged in.)  Note that Travis only synchronizes
repositories with GitHub once a day, so you might have to force a refresh.

You will need the Travis command line tool for the next step; this is available
as a [Ruby](https://www.ruby-lang.org/) [gem](https://rubygems.org/):

```sh
$ sudo gem install travis
```

*WARNING*: You might want to use a dummy account for this next part to minimize
any problems from accidental leaks of your key.  Once you enable pushes from
Travis, be very careful accepting pull requests that alter `.travis.yml` or
`Makefile`.  Those files can cause the value of the token to be published for
all to see.  You don't want that to happen, even though tokens can be revoked
easily.  Only pushes to the main repository will be able to see the token, so
don't worry about pull requests.

Then, you need to get yourself a [new GitHub application
token](https://github.com/settings/tokens/new).  The application token only
needs the `public_repo` privilege.  This will let it push updates to your
`gh-pages` branch.

Then, you update the Travis configuration file with an encrypted copy of that
token, as follows:

```sh
$ travis encrypt GH_TOKEN=<YOUR TOKEN HERE> -a -p
$ git add .travis.yml
$ git commit
$ git push
```

As a side benefit, Travis will now also check pull requests for errors, letting
you know if things didn't work out so that you don't merge anything suspect.


## Updating the Makefile

Occasionally improvements and changes are made to the Makefile or the support
files in this repository.  The `update` make target looks after the update of
the core files.

```sh
$ make update
$ git commit
```

This script is cunning enough to handle merging any simple changes that you
might have made to the Makefile yourself, such as adding targets.


## Submitting Drafts

See `SUBMITTING.md`.
