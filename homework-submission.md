#Instructions for Submitting Homework

### Dawn/Dusk Exercise Submission

Please submit your solutions to **individual exercises / problem sets** (from dawn/dusk) using your homework repo.

- Copy/paste your solutions into your homework repo (e.g. john-doe/week-01/day-01/solutions.md)
- Follow the instructions below for *Creating Pull Requests*.

### Lab Work Submission
Unlike dawn/dusk exercises, *labs* are projects you started in class that you had to fork and clone. Because labs live in a separate repo, they require a slightly different submission flow:

- When you begin a lab, you must remember to first `fork` the lab! (Just click the `fork` button).
- Next, `git clone` your fork of the lab so that you can work on it locally (on your computer).
- When it's time to submit your homework, follow the instructions below for *Creating Pull Requests*.

For detailed instructions, see the [Fork, Clone & Pull Request](fork-clone-pull-request-flow.md) guide.


## Creating Pull Requests
When you're ready to submit your homework (and it's okay if you only have a partial solution, we still want to see it!), you need to push your changes to github and create a pull request:

1. First, `git add` and `git commit` your changes:

    ``` bash
    git status                                  # check everything's okay
    git add week01/day-1/solutions.md           # add your files, one by one
    git commit -m "homework solution for day 1" # describe your changes
    ```

2. Next, `git push` your updates to your fork of the homework repo on github.

    ``` bash
    git push origin master # push your changes to your github repo
    ```

3. Finally, go to your homework repo on github and submit a *pull request (PR)* using the *Pull Request Format* described below.

### Pull Request Format
```
w1d1
```
```
comfort: 4/5
completeness: 3/5

This homework was awesome! Here are my thoughts on how it went...
```

