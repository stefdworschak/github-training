# Git Training

## Setup

1. Fork the repository

1. Go to your fork's `Actions` tab and click on the button saying `I understand my workflows, go ahead and enable them`.
This will enable the different automated workflows we have created to enable the tutorials. The tutorials will not work otherwise.

1. Create a new Personal Access Token

```
Click on your Account (top-right) > Settings
> Developer Settings > Personal access tokens
> Generate new token
```

Direct link [https://github.com/settings/tokens/new](https://github.com/settings/tokens/new)

4. Give the token a name (e.g. github-training) and select `repo` as scope
1. Copy the generated token 
1. Create a new Secret in your forked GitHub repo with the name `GH_TOKEN` and paste the generated token

```
Open the forked repo > Settings > Secrets > New repository secret
```


## Tutorial 1 - Merge Conflict

### Setup

1. Checkout to a new branch called `new_branch1` and push it to your fork

```
git checkout -b new_branch1
git push origin new_branch1
```

2. Add the below code to the body of the `index.html` file

```
<h1>This is my heading</h1>
<p>This is my paragraph</p>
```

3. Add, commit and push your changes to your branch

```
git add .
git commit -m "Updating index file"
git push origin new_branch
```

4. Create a new Pull Request on GitHub to your own fork's main branch (not the original repo). You should see that there is a merge conflict now.

### Solution - Change file and commit changes

1. Go back to your terminal and pull the changes from the main branch into your branch.

```
git pull origin main
```

The termninal should show a similar message to the one shown below. Explaining that there is a merge conflict in the index.html file which will have to be resolved before being able to merge.

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

2. To resolve the merge conflict, open the index file.
You should see the below error:

```
<<<<<<< HEAD (Current Change)   
	    <h1>A Heading</h1>
	    <p>This is a paragraph</p>
======= 
        <h1>This is a heading</h1>
>>>>>>> 5be693431cd5e6562f8b960cc38b24a93daa7e4b (Incoming Change)
```

What this means is that the changes on your branches "HEAD" (Incoming Change) and the changes pulled from another branch (Incoming Change) are in conflict.

The exact conflicting lines are always displayed between the merge conflict markers indicated by `<` (start), `=` (separator between branches) and `>` (end).
Here a more simplified example:

```
<<<<<<<
branch 1 changes
======= 
branch 2 changes on the same line
>>>>>>>
```

A lot of editors will give you an integrated option to accept either of the branches' versions or both, but for the purpose of this exercise simply delete the merge conflict markers and the content of the _Incoming Change_.

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
3. Now that the merge conflict is resolved; add, commit and push your changes to your branch and merge your Pull Request.

```
git add index.html
git commit -m "Resolving merge conflict"
git push origin main
```

4. If you were working with other developers you would now communicate that you have merged your changes into the `main` branch and that they need to update their local `main` branches and any development branches they are currently working on.
