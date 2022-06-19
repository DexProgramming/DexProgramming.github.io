---
title: "A Simple Hugo Site"
date: 2022-06-17T16:16:43+02:00
---

Hugo is a Static Site Generator that allows us to create fast, content-oriented websites. In this simple example, we will create a Hugo site, post it for free on GitHub Pages and use a custom domain. The process is simple and consists of a series of steps, so let's go(lang) in order:

*You do not need to install Go to use Hugo as your static site generator.*

# 1. INSTALL HUGO

There are instructions for all operating systems on the official website - [Install Hugo](https://gohugo.io/getting-started/installing/#:~:text=Install%20Hugo%20on%20macOS%2C%20Windows,with%20support%20for%20multiple%20platforms.). I personally use Ubuntu 22.04, so I had to install [Homebrew](https://brew.sh/) first and then run the next command in the terminal:

```bash
brew install hugo
```

# 2. CREATE A NEW HUGO SITE

In the terminal, find the location where you want to create a new hugo site (for example Desktop) and run the appropriate command:

```bash
cd Desktop
hugo new site <your_site_name>
```
# 3. INITIALIZE AN EMPTY GIT REPOSITORY

Now you need to initialize the empty git repository within the created Hugo site.

```bash
cd <your_site_name>
git init
```

# 4. INSTALL A THEME

You can find themes at the following link [Hugo themes](https://themes.gohugo.io/) and when you select the appropriate one run the following code (of course use the link from your theme instead of the one below):

```bash
git submodule add https://github.com/<git_user>/<your_theme_name>.git themes/ananke
```

Now if you open the themes folder, you can find the installed theme with the appropriate content. But in order for our site to use this theme, we need to edit the config.toml file and add the following line 

```toml
theme = '<your_theme_name>'
```

# 5. CREATE CONTENT AND TEST SITE

To make sure everything is working properly, we will create a few blog posts and launch the site locally.

```bash
hugo new posts/first-blog-post.md
hugo new posts/second-blog-post.md
```

In order to see these posts we need to edit them and delete the following line: 

```yml	
draft: true
```

Now it's time to test the Hugo site locally:

```bash	
hugo server
```

And we can visit the website at [http://localhost:1313/]()

# 6. CREATE A GITHUB REPOSITORY

Log in to your GitHub account and create a github repository.

# 7. CONNECT LOCAL AND GITHUB REPOSITORY

Run the following git commands in the terminal:

```bash
git status
git add .
git commit -m "initial commit"
git branch -M main
git remote add origin https://github.com/<your_github_name>/<yout_github_repo_name>.git/
git push -u origin main
```

And if you refresh the GitHub page you will see that everything has been uploaded.

# 8. ADD GITHUB ACTIONS

After we add this script, every time you push the repository to GitHub, GitHub Actions will build the website automatically.

Create the following structure in your folder: `.github/workflows/gh-pages.yml`

Then go to the official website, in the [Host on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/) and copy the script to `gh-pages.yml`.

Now you need to push all this into the GitHub Repository:

```bash
git status
git add .
git commit -m "github action"
git push
```

When workflow run successfully, it is necessary to select branch: `gh-pages` in the settings/pages and save everything.

Also copy the link where the website was published, something like [http://<your_github_name>.github.io/<your_repo_name>/]()

# 9. SET BASE URL

You need to configure the baseURL inside the `config.toml` file and push it all on GitHub again.

```toml
baseURL = 'http://<your_github_name>.github.io/<yout_github_repo_name>/'
```

```bash
git status 
git add .
git commit -m "baseURL change"
git push
```

# 10. SET A CUSTOM DOMAIN

If you have a custom domain, it is necessary to link it to the GitHub site by creating several records:

- A record for **@** pointing to _185.199.108.153_  
- A record for **@** pointing to _185.199.109.153_  
- A record for **@** pointing to _185.199.110.153_  
- A record for **@** pointing to _185.199.111.153_  
- CNAME record for **www** pointing to your _username.github.io_ (the username should be replaced with your actual GitHub account username):

For example for the Namecheap domain more information can be found on the following website - [link Namecheap domain to GitHub Pages](https://www.namecheap.com/support/knowledgebase/article.aspx/9645/2208/how-do-i-link-my-domain-to-github-pages/)

Then enter the custom domain in the GitHub repository in settings/pages and save everything.

It is also necessary to create a CNAME file in the static folder in which there will be a custom domain (for example "custom-domain.com").

Now change baseURL in `config.toml` to custom domain and push everything on GitHub again.

```bash
git status
git add .
git commit -m "custom domain setup"
git push
```

# And that is all.