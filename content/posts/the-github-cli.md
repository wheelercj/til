+++
title = 'The GitHub CLI'
date = 2025-03-10T13:31:32-07:00
+++

I had heard about [GitHub's CLI](https://cli.github.com/) a while ago, but didn't understand why it could be so useful. Below are a few reasons why.

When you have a terminal open in one of your projects, you can enter `gh browse` (without any project name or url!) and the project's GitHub page will open.

If you want to create a new issue without having to wait for the website to load, and without potentially being distracted by its notifications or other changes, you can run `gh issue create` and then follow the prompts to enter an issue title, body, assignees, and more.

`gh issue list` shows your current issues, and `gh status` shows a summary of many things including assigned issues, pull requests, review requests, and mentions.

Sometimes it's helpful to manually trigger a GitHub Actions workflow, and it's easiest from the command line. For example, if you have a workflow file named "pages.yaml" that builds and publishes a GH Pages site, you can run `gh workflow run pages.yaml` in your terminal to run the workflow.

You can even set up ways to be notified when a workflow finishes! One way shown in [the GH CLI docs](https://cli.github.com/manual/gh_run_watch) is `gh run watch && notify-send 'run is done!'`, which uses Linux's `notify-send` command to show a desktop notification. A great cross-platform way that can even send a notification to your phone is with [ntfy](https://github.com/binwiederhier/ntfy). For example, `gh run watch && curl -d "Run finished" ntfy.sh/your-topic-name-here`.

If you happen to use GitHub's API from the command line, the GitHub CLI makes it easier to make authenticated requests with its [`api` subcommand](https://cli.github.com/manual/gh_api).

There are so many more commands. With the GH CLI, you can search for anything, set rules and variables, create and manage releases, repos, projects, pull requests, gpg keys, gists, labels, and codespaces, and so much more. I'll still do a lot of this on the website, but sometimes using the CLI is faster and easier.
