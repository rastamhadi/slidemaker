# slidemaker

`slidemaker` is a collection of Rake tasks that help me prepare slides for presentations.

## Prerequisites

* Ruby
* rbenv
* Sublime Text
* bundler
* Google Chrome
* The [LiveReload](https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei) Chrome extension

## Installation

Clone this git repository:

```
$ git clone git@github.com:rastamhadi/slidemaker.git
```

## Generating a new slidedeck project

1. Create a new directory for your slidedeck project:

   ```
   $ mkdir my_awesome_talk
   ```

2. Copy the `slidemaker` Rakefile into your new directory:

   ```
   $ cp /path/to/slidemaker/Rakefile /path/to/my_awesome_talk
   ```

3. Modify the `SLIDEMAKER_PATH` in your Rakefile as necessary.

4. Run `rake init` and supply a title when prompted.

   ```
   $ rake init
   ...
   What is the title of your slides?
   My Awesome Talk!
   ...
   ```

## Working on your slides

1. Run `rake`. This will launch:

   * your workspace in Sublime Text
   * your slides in Google Chrome
   * [Guard](http://guardgem.org/)

2. Enable your LiveReload extension to refresh your slides on the fly.

## Hosting your slides locally

:construction: Coming Soon! :construction:
