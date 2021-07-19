# Git Training

## Setup

1. Fork the repository

![Forking screenshot](https://gist.github.com/stefdworschak/7b6e93f38b98256fd5ce00982b3ba1ca/raw/25e3632cfea3a5308cb75c24440f75cd85b48ab3/fork_repo.png)

2. Go to your fork's `Actions` tab and click on the button saying `I understand my workflows, go ahead and enable them`.
This will enable the different automated workflows we have created to enable the tutorials. The tutorials will not work otherwise.

![Enable repo actions](https://gist.github.com/stefdworschak/7b6e93f38b98256fd5ce00982b3ba1ca/raw/25e3632cfea3a5308cb75c24440f75cd85b48ab3/activate_actions.png)

3. Create a new Personal Access Token

Direct link to the form: [https://github.com/settings/tokens/new](https://github.com/settings/tokens/new)

Or navigate there through the GitHub UI:
```
Click on your Account (top-right) > Settings
> Developer Settings > Personal access tokens
> Generate new token
```

4. Give the token a name (e.g. github-training) and select `repo` as scope

![Create personal access token](https://gist.github.com/stefdworschak/7b6e93f38b98256fd5ce00982b3ba1ca/raw/25e3632cfea3a5308cb75c24440f75cd85b48ab3/assign_scope.png)

5. Copy the generated token 

![Copy token](https://gist.github.com/stefdworschak/7b6e93f38b98256fd5ce00982b3ba1ca/raw/25e3632cfea3a5308cb75c24440f75cd85b48ab3/copy_generated_token.png)

6. Create a new Secret in your forked GitHub repo with the name `GH_TOKEN` and paste the generated token

```
Open the forked repo > Settings > Secrets > New repository secret
```

![Create repo secret](https://gist.github.com/stefdworschak/7b6e93f38b98256fd5ce00982b3ba1ca/raw/25e3632cfea3a5308cb75c24440f75cd85b48ab3/create_repo_secret.png)


## Tutorial 1 - Merge Conflict

### Setup

1. Open the repo in Gitpod (or clone it locally and open your IDE)

2. In the terminal, checkout to a new branch called `new_branch1` and push it to your fork

```
git checkout -b new_branch1
git push origin new_branch1
```

3. Add the below code to the body of the `index.html` file

```
<h1>This is my heading</h1>
<p>This is my paragraph</p>
```

4. Add, commit and push your changes to your branch

```
git add .
git commit -m "Updating index file"
git push origin new_branch1
```

5. Go back to your own fork's repo and click on the "Compare & Pull Request" button

6. You should see that there is a merge conflict now.
Even though there is a merge conflict, click on "Create Pull Request" to finish the setup.

__TODO: ADD A GIF__


### Solution - Change file and commit changes

1. Go back to your terminal and pull the changes from the main branch into your branch.

```
git pull origin main
```

The terminal should show a similar message to the one shown below. Explaining that there is a merge conflict in the index.html file which will have to be resolved before being able to merge.

```
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
Unpacking objects: 100% (3/3), 340 bytes | 340.00 KiB/s, done.
From https://github.com/repo/github-training
 * branch            main       -> FETCH_HEAD
   a77976a..5be6934  main       -> origin/main
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

2. Open the index file and have a look at the merge conflict to better understand what is going on.
You should see the below error:

```
<<<<<<< HEAD (Current Change)   
	    <h1>A Heading</h1>
	    <p>This is a paragraph</p>
======= 
        <h1>This is a heading</h1>
>>>>>>> 000aaa000aaa000aaa000aaa (Incoming Change)
```

What this means is that the changes on your branch's "HEAD" (Current Change) and the changes pulled from another branch (Incoming Change) are in conflict.

The exact conflicting lines are always displayed between the merge conflict markers indicated by `<<<<<<< HEAD` (start), `=======` (separator between branches) and `>>>>>>> 000aaa000aaa000aaa000aaa` (end).
Here a more simplified example:

```
<<<<<<< HEAD
branch 1 changes
======= 
branch 2 changes on the same line
>>>>>>> 000aaa000aaa000aaa000aaa
```

3. To resolve the merge conflict simply delete the merge conflict markers (see above) and the content of the _Incoming Change_. A lot of editors will give you an integrated option to accept either of the branches' versions or both for ease of use as well.

Your file should look like this after:
```
<!DOCTYPE html>
<html>
    <head>
        <title></title>
    </head>
    <body>
        <h1>A Heading</h1>
        <p>This is a paragraph</p>
    </body>
</html>
```
3. Now that the merge conflict is resolved; add, commit and push your changes to your branch.

```
git add index.html
git commit -m "Resolving merge conflict"
git push origin branch1
```

4. Go back to your fork's GitHub repo, click on "Pull Requests" and open the Pull Request you created.

1. Scroll down to the Checks section. It should now say that there are no Merge Conflicts.

1. Click the "Merge pull request" Button to merge your changes into your fork's main branch.

1. Go back to your terminal, checkout to your main branch and pull the changes from GitHub

```
git checkout main
git pull origin main
```

8. If you were working with other developers you would now communicate that you have merged your changes into the `main` branch and that they need to update their local `main` branches and any development branches they are currently working on.
