# Finched Rails CLI

This is a fork of [rails/docked](https://github.com/rails/docked).

Setting up Rails for the first time with all the dependencies necessary can be daunting for beginners. Finched Rails CLI uses a Open Container Initiative (OCI) image to make it much easier, requiring only Finch to be installed.

Install [Finch](https://github.com/runfinch/finch). Then copy'n'paste into your terminal:

```bash
finch volume create ruby-bundle-cache

alias finched='finch run --rm -it -v ${PWD}:/rails -v ruby-bundle-cache:/bundle -p 3000:3000 --entrypoint "" ghcr.io/yokawasa/rails/cli'
```

Then create your Rails app:

```bash
finched rails new weblog
cd weblog
finched rails generate scaffold post title:string body:text
finched rails db:migrate
finched rails server
```

That's it! Your Rails app is running on `http://localhost:3000/posts`.

## Adding more aliases

If you'd like to have the standard Ruby and Rails bins available without writing `finched` before each command, you can add them as aliases:

```bash
alias rails='finched rails'
alias rails-dev='finched bin/dev'
alias bundle='finched bundle'
alias yarn='finched yarn'
alias rake='finched rake'
alias gem='finched gem'
```
