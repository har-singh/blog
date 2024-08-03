# Blog

###### 3-Aug-24

A while ago (1 year) I moved block posts from Wordpress to GitHub Pages using https://jsanz.github.io/gh-pages-minima-starter/ as reference.

Dependabot has been sending weekly reminder emails about the vulnerabilities and there were still some references to Wordpress for the image source which were address in the `dev` branch but I never got chance to merge to main.

Today I have spend most part of the day reviewing and finally have got updated and smaller `Gemfile.lock`.

ChatGPT was the main assistant in doing all the work. Main takeaway are that there is a `Pages` section in the repository where reference branch can be changed. Other notes:

- For the `Gemfile` it took a while installing the correct version (build?) on ubuntu. So at first the file `Gemfile.lock` was deleted and recreated with `bundle install` but it still resulted in a long lock file. Later on I tried to create the Minima setup from scratch where chat suggested to create `Gemfile` with `gem "minima", "~> 2.5"`. Once done I realized the original file had `gem 'github-pages', group: :jekyll_plugins`. ~But this trick helped with getting rid of most of the packages from the lock file.~
- I realized later but there is option to `remediate` from the Dependabot page which would run a Actions workflow and then create a pull request with the remedies.
