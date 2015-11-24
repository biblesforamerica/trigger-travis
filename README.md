# trigger-travis

A Heroku-ready travis triggerer. Allows you to manually or periodically trigger a build for a specific branch.

Heavily inspired by:

* https://github.com/philou/daily-travis
* https://github.com/coderanger/nightlies

## Usage

### Prerequisites

* You have the [Heroku Toolbelt](https://devcenter.heroku.com/articles/quickstart) installed
* You have a [Github Token](https://help.github.com/articles/creating-an-access-token-for-command-line-use) with the default settings

### Setup

```shell
git clone https://github.com/larslockefeer/trigger-travis.git
heroku apps:create {my-prefix}-trigger-travis
heroku config:add TRAVIS_REPOSITORY={user/organization}/{repository}
heroku config:add GITHUB_TOKEN={token}
heroku config:add TRAVIS_BRANCH={branch}
git push heroku master
```

If you are using Travis Pro instead of Travis for Open Source projects, you also need to do the following:

```shell
heroku config:add TRAVIS_PRO=true
```

### Trigger a build manually

You can now trigger a build manually by executing:

```shell
heroku run rake build
```

### Periodically trigger a build

Or you can schedule a periodical build:

```shell
heroku addons:create scheduler:standard
heroku addons:open scheduler
```

Add the task `rake build` to your heroku scheduler
