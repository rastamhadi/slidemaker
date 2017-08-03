# slidemaker

`slidemaker` is a collection of Rake tasks that help me prepare slides for presentations.

## Prerequisites

* macOS
* Git
* [gitsh](https://github.com/thoughtbot/gitsh)
* Ruby
* rbenv
* Sublime Text
* bundler
* Google Chrome
* The [LiveReload](https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei) Chrome extension
* Apache set up as in [this article](https://medium.com/@rastamhadi/how-i-host-lightning-talk-slides-from-my-imac-7b00912e15a5)
* A [Bitbucket](https://bitbucket.org/) account for privately storing your slidedeck project

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

## Version control with Bitbucket

Run `rake gitsh` to launch the project in gitsh.

Don't forget to [create a new Bitbucket repository](https://bitbucket.org/repo/create) if you don't have one already.

## Hosting your slides locally

Run `rake host:url`. This command will print the URL for your slides.

```
$ rake host:url
http://192.168.123.456/~your_name/my_awesome_talk
```

## Exporting your slides as a PDF

1. Run `rake pdf`. This will launch your slides in Google Chrome in `print-pdf` mode.
2. Open the `Print` dialog (`File > Print...`) and `Save as PDF`.

![Print to PDF](https://user-images.githubusercontent.com/1012322/28924083-6653f602-789b-11e7-9a48-ae24d078eb32.png)
