---
layout: post
title: "Bundler: Using Local Gems"
date: 2016-03-23 18:39
categories:
---

With [Bundler], you can easily switch to a local gem by using the `path` option.

```ruby
  # Gemfile
  gem 'my_gem', path: '/home/jd/projects/my_gem'
```

However, this method requires changing the Gemfile. There is an easier way.

```sh
  bundle config local.my_gem /home/jd/projects/my_gem
```

Afterwards, this can be reset by deleting this config.

```sh
  bundle config --delete local.my_gem
```

Note that, this method requires the local gem to be in the same git branch as defined in the Gemfile.
To ignore this check, use the following

```sh
  bundle config disable_local_branch_check true
```

Also see the [bundler docs]

[Bundler]: http://bundler.io
[bundler docs]: http://bundler.io/v1.2/git.html#local
