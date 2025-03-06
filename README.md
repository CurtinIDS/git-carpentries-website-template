[![Website](https://github.com/carpentries/workshop-template/actions/workflows/website.yml/badge.svg)](https://github.com/carpentries/workshop-template/actions/workflows/website.yml)

# The CIDS' Carpentries Workshop Template for Git

This repository is CIDS' version of The [Carpentries'][swc-site] template for creating websites for workshops.

1. **Please _do not fork this repository directly on GitHub._** Instead, please use GitHub's
   "template" function following [the instructions below](#creating-a-repository) to copy this
   `workshop-template` repository and customise it for your workshop.

2. Please *do your work in your repository's `gh-pages` branch*, since that is what is
   [automatically published as a website by GitHub][github-project-pages].

3. Once you are done, please also [let the Carpentries know][email] the workshop URL. If this is a self-organised workshop, you should also [fill in the self-organized workshop
   form][self-organized-workshop-form] (if you have not already done so), so they can keep track of
   all workshops. They build the list of workshops on their websites from the data included in your
   `index.md` page. They can only do that if you [customise][customization] that page correctly *and*
   let them know the workshop URL.

# Creating and Customizing the website
The website is made using jekyll, which creates static html pages from markdown (and/or html).   
Making the website is straightforward if you follow these steps after logging into github:
1. Use the Github template function (top-right green button) to create a new repository in the CIDS domain. Title the new repo "YYYY-MM-DD-curtin-carpentries-<lang>". e.g. "2025-04-03-curtin-carpentries-git".  

    ![screenshot of this repository's GitHub page with an arrow pointing to the the 'use this template' button on the top left](fig/select-github-use-template.png?raw=true)
2. If the repo is public, a new webpage should be created at `curtinids.github.io/<reponame>`.
3. Edit the workshop title in '_config.yml'. You shouldnt need to edit nay other settings.
4. Edit relevant information at the top of "index.md". If you want to change any other wording on the main page (other than the scheudle), scroll down and make your changes using html. Make sure to delete the alert block at the top (next to the comment that tells you to delete it).
5. Ensure `_episodes` (which contains the CIDS Git lesson material) is up-to-date.
6. Edit `_includes/schedule.html` to correspond with the lesson material and schedule. This file is inserted into the main index. You will be editing the two tables defined after the `<table class="table table-striped">` keywords. an enclosing `<tr>` indicates a row, and an enclosing `<td>` indicates a column. By default, there will be two rows per column.  
  If you want to insert another row, copy and paste the following into the desired location in the table after a `</tr>` (forward slash tr) and before the next `<tr>` (bare tr):
    ```html
    <tr>
      <td>TIME></td>
      <td>DESCRIPTION</td>
    </tr>
    ```
    To remove a row, delete everything withing an enclosing `<tr> ... </tr>`, including the `<tr>` \& `</tr>` parts.

7. Have a browse through the website and make sure there's no placeholders left and everything is correct

# Working locally
When making a large amount of changes to the website, it may be preferable to work locally to avoid needing to push to GitHub to test your changes. Here we describe both the setup needed and the commands to run it.
## Pre-requisites
This website currently requires a specific ruby version, 2.7.3.  
### Windows/OS X
Follow the instructions [here](https://carpentries.github.io/lesson-example/setup.html#jekyll-setup-for-lesson-development) for OS X/ Windows. There's also a Linux section in that link, but it involves installing homebrew. See below for an alternate way.

### Linux alternate install
Unfortunately the ubuntu/debian versions are currently out of date, and while conda-forge has newer and older versions, it does not have 2.7.3.  
To install 2.7.3 on linux, it's usually easiest to do the following:
1. Install [rbenv](https://github.com/rbenv/rbenv.git) (Ruby environment manager):
    ```shell
    git clone https://github.com/rbenv/rbenv.git ~/.rbenv
    ~/.rbenv/bin/rbenv init
    ```
    then <u><b>restart your shell</b></u>
2. Install the ruby build plugin into the rbenv folder
    ```
    git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build
    ```
3. Use the following commands to install ruby 2.7.3, download the repo, set the local ruby version in the local directory to 2.7.3, install all the needed packages, and then cleanup:
    ```
    rbenv init
    rbenv install 2.7.3
    git clone <repo>
    cd <repo dir>
    rbenv local 2.7.3
    rbenv shell 2.7.3
    gem install bundler
    make clean
    ```

## Building the website locally
Once you've installed the pre-requisites, simply `cd` into the repo folder in a  terminal and run:
```
make serve
```

If you're working on a remote server via ssh, you can pass through the ports with:
```
ssh -N -L <local port>:localhost:<port on host>
```
then navigate in your web-browser to localhost:<port>  

## Optional but Recommended Steps

### Update your repository description and link your website

At the top of your repository on GitHub you'll see

~~~
No description, website, or topics provided. — Edit
~~~

Click 'Edit' and add:

1.  A very brief description of your workshop in the "Description" box (e.g., "Oomza University workshop, Dec. 2016")

2.  The URL for your workshop in the "Website" box (e.g., `https://gvwilson.github.io/2016-12-01-oomza`)

This will help people find your website if they come to your repository's home page. You may wish to check the box "Use Github pages link."

### Update the content of the README file

You can change the `README.md` file in your website's repository, which contains these instructions,
so that it contains a short description of your workshop and a link to the workshop website.

## Creating Extra Pages

In rare cases,
you may want to add extra pages to your workshop website.
You can do this by putting either Markdown or HTML pages in the website's root directory
and styling them according to the instructions give in
[the lesson template][lesson-example].

- A `.../subdir/index.md` file will be mapped to `.../subdir` on the website,   and 
- any other `.../subdir/filename.md` file will be mapped to `.../subdir/filename.html` on the website

Be wary, that on github the pages will be hosted at `curtinids.github.io/<repo name>/page`, whereas on your local machine this will be `localhost:<port>/page`. This may mean links that work locally dont work on the web page, so be sure to specify links explicitly using the variable `relative_root_path`, e.g. 
```
<a href={{ relative_root_path }}/page>some text</a>
```

## Additional Notes

**Note:**
please do all of your work in your repository's `gh-pages` branch,
since [GitHub automatically publishes that as a website][github-project-pages].

**Note:**
this template includes some files and directories that most workshops do not need,
but which provide a standard place to put extra content if desired.
See the [design notes][design] for more information about these.

Further instructions are available in [the customization instructions][customization].
This [FAQ][faq] includes a few extra tips (additions are always welcome)
and these notes on [the background and design][design] of this template may help as well.

## Installing Software

If you want to set up Jekyll so that you can preview changes on your own machine before pushing them
to GitHub, you must install the software described in the lesson example .

## Setting Up a Separate Repository for Learners

If you are teaching Git,
you should create a separate repository for learners to use in that lesson.
You should not have them use the workshop website repository because:

* your workshop website repository contains many files that most learners don't need to see during
  the lesson, and

* you probably don't want to accidentally merge a damaging pull request from a novice Git user into
  your workshop's website while you are using it to teach.

You can call this repository whatever you like, and add whatever content you need to it.

## Getting and Giving Help

We are committed to offering a pleasant setup experience for our learners and organizers.
If you find bugs in our instructions,
or would like to suggest improvements,
please [file an issue][issues]
or [mail us][email].

[email]: mailto:team@carpentries.org
[customization]: https://carpentries.github.io/workshop-template/customization/index.html
[dc-site]: https://datacarpentry.org
[design]: https://carpentries.github.io/workshop-template/design/index.html
[faq]: https://carpentries.github.io/workshop-template/faq/index.html
[github-project-pages]: https://help.github.com/en/github/working-with-github-pages/creating-a-github-pages-site
[issues]: https://github.com/carpentries/workshop-template/issues
[lesson-example]: https://carpentries.github.io/lesson-example/
[self-organized-workshop-form]: https://amy.carpentries.org/forms/self-organised/
[swc-site]: https://software-carpentry.org
[lc-site]: https://librarycarpentry.org