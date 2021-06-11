# Making your own inclusive bot

## What, why, how
Ever saw a word in a repository that really made you feel bad? 
Why use it? Can't we use something else? We can!
How? At the point we use them, when we are making changes, wouldn't it be great to have a reminder of what anyone in our team found to be unhelpful and unfriendly?

## What we will cover, what we won't cover

- We will create a github action and cover how you go about running a node js file on an incoming pull request to search for certain words
- We will pick a word we are going to look for
- We will talk about how best to curate a list of unfriendly or unhelpful terms within your team
- We will generate our own personal github token so that we have permission to post as us in the repo we use the action on 

- I won't cover how you might go about creating a specific user to post messages on the repo the action is installed on (the PR comments will come from your github user)
- We won't be covering how you might change or adjust to process for private repositories
- There are many ways you can customise your javascript e.g. to flag what lines the words appear in and what specific words were used, we will just be covering sending a message when a word appears in a pull request

There are lots of different ways to do things, I'll go through this is one way that has worked for me with methods that are readable to me and to my colleagues, you may have improvements and suggestions, you can feel free to continue to add those to your own code during or after the workshop. Throughout the steps there will be chances to catch up if you're getting stuck, or chances to skip ahead if you're wanting to go at a faster pace. Every step we go through here is for you to keep and refer to later so if you don't get everything finished or as you want it, you can come back to it later.

## Step 1

To begin, you'll need to be logged into your GitHub account, and you'll need to create a new repository. Make it public for the moment.

You can call it `inclusiveBot_yourname`

Open your terminal, navigate to the location you want the repo to live locally and copy the first set of commands from the newly created gitub repo.

Update the readme (copy and paste from this gist link).

from your terminal, in this repo `npm init` to initialise node and create a `package.json` file

*finished this step early?* go to step 2 and create your action.yml file


## Step 2

Create a new file named `action.yml` within the root directory of your own repository.

The actions toolkit is a collection of Node.js packages that allow you to quickly build JavaScript actions with more consistency.

The toolkit @actions/core package provides an interface to the workflow commands, input and output variables, exit statuses, and debug messages.

The toolkit also offers a @actions/github package that returns an authenticated Octokit REST client and access to GitHub Actions contexts.

The toolkit offers more than the core and github packages. For more information, see the actions/toolkit repository.

At your terminal, install the actions toolkit core and github packages.

```
npm install @actions/core
npm install @actions/github
```

*Getting stuck?* [Here is the link](https://gist.github.com/melanierogan/0c324dfd3795a57f23c6e58fb1fdec4f) to the `action.yaml` file (ADD LINK GIST)
*finished this step early?* Go to step 3 and start thinking about what word or words you want to flag.


## Step 3
Get wordy - generate your list of words 
*stuck* pick one word you want to look for e.g. banana
*finished this step early?* Move to step 4 and get started writing your javascript to read through an incoming PR


## Step 4
Create a file called `index.js` and begin writing the functions that will look at the incoming pull requests

*Getting stuck?* grab the pre-written functions from [this gist](https://gist.github.com/melanierogan/03e2fb2983d80dee2bdec4870efd1af6) and place them in your `index.js` file
*finished this step early?* move through step 5 and step 6


## Step 5
Let's get everything committed to your repo. We are also going to ensure we tag our releases.

```
git add action.yml index.js node_modules/* package.json package-lock.json README.md
git commit -m "My first inclusive bot is ready"
git tag -a -m "My first inclusive bot release" v1.1
git push --follow-tags
```

Most of the time you might not have committed `node_modules` but we are doing it here as the github action must have access to the modules to run our `index.js` file from our `action.yml`

*finished this step early?* Skip ahead to step 6.


## Step 6
We need to generate a key to use in our github action script that allows us to post a message.
To do this we go to profile, developer settings then Personal access tokens
You generate one and name it 'INCLUSIVE_BOT_TOKEN'. Give it 'workflow' access, admin:repo_hook and write:discussion.

What must be there: rest before the issues create so that we get the permission in the context of the issue.
A personal key so we have permissions to post comments

To ensure you can make use of this in your project, copy the code and go to your repo on github, settings, then secrets and new repository secret and call it 'INCLUSIVE_BOT_TOKEN' and paste in the key you generated.

Remember: for future reference, should you end up customising this inclusivebot action further you should consider having a .gitignore file with .env or config files listed so you can ensure you're not committing secrets.
*finished this step early?* Move to step 7


## Step 7
Copy the following gist YAML into a new file at `.github/workflows/main.yml`, and update the uses: melanierogan/repo line with your username and the name of the public repository you created. 

Commit the `main.yml` file, remembering to add a release tag before pushing.

```
git add .
git commit -m "My first inclusive bot is ready"
git tag -a -m "My first inclusive bot release" v1.2
git push --follow-tags
```

*Getting stuck?* you can copy the main.yml file [from this gist](https://gist.github.com/melanierogan/293d156ac73941c6b2a598cba9149cd2)
*finished this step early?* Move to step 8, and gather your questions and if we don't get to them, drop me a line i'll give contact details at the end


## Step 8
Open a PR on your repo to test your work.

*Getting stuck?* double check your `action.yml` and `main.yml` files, try open PR on your own repo. Some gotchas: watch your branch names, and ensure you list @ before the version number on the repo.

*finished this step early?* 
- What features could you add now? How would you make that list of words something work for your team? A google sheet? What works for your team workflow? A gist that you update as a team and node fetch from? 
- Create a status badge for your action
- Install the workflow on another repo 
