**Warning, this isn't actually implemented yet!!**

# Heroku buildpack: Lineman + Ruby

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for Ruby, Rack, and Rails apps that want to incorporate Lineman apps.

```
$ heroku create --stack cedar --buildpack https://github.com/testdouble/heroku-buildpack-lineman-ruby.git
```

## Configuration

This buildpack should behave just like the official Ruby buildpack, with the added behavior of compiling and placing a built Lineman app (or apps).

To get started, you'll need a lineman.json file in the project root. Here's an example:

```
"linemanApps": [
  {
    "type": "git",
    "location": "git@github.com:searls/lineman-ember-template.git",
    "revision": "ac84a7a",
    "installToPath": "public/app1"
  },
  {
    "type": "file",
    "location": "front_end",
    "installToPath": "public/app2"
  }
]
```

The above configuration specifies that two Lineman apps should be deployed alongside the Ruby app.

### Using git

The first app is stored in a separate git repo that will be cloned during the Heroku slug compilation, then built, and its built `dist` assets will be moved to a path `public/app1`. The "revision" property is optional and can be useful for locking down to a specific version of the git repo, either a SHA or tag or branch's HEAD.

### Using local files

The second app is stored in a directory off the root of the repo called "front_end" and should be built and then moved to "public/app2".
