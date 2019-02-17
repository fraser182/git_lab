## Task (30 mins)

In pairs work through the following steps to create and merge branches and deal with any git merge conflicts. Work through the steps together, so you understand each part of the process.

You are going to start with a master and a develop branch. Then you are going to be making feature branches and merging them into develop.

## Person One

Person One is going to start by creating the directory structure and a develop branch.

### Master branch

1. Create a local directory called `git_lab` and initialise git inside it - `git init`
2. Create a new repo called 'git_lab' on GitHub and add it as the remote of your local directory `git remote add origin git@github.com:your_github_username/git_lab.git`
3. Create a file called greet.js inside the directory
4. Commit and push the changes

We now know that the local and remote master branch are the same.

### Develop branch

1. Create a develop branch off of master - `git checkout -b develop`. (The `-b` flag indicates you are making a new branch, and it is followed by the name of the branch. This command will move you into develop, so you will see the word 'develop' in your terminal, next to the directory name.)
2. Add the following to greet.js:
```js
const helloWorld = () => {
  return "Hello World!";
}
```
3. Add and commit your changes.
4. Push to develop branch - `git push origin develop`. We now know the local and remote develop branches are the same. These changes have **only** been committed on the develop branch. The master branch has not been not affected.
5. Add your partner as a collaborator to the repository on GitHub by going to the repository page. Click `settings` then `collaborators` and add a new collaborator. This will enable your partner to push and pull to the repository directly.

> When you move between branches, your editor will automatically update to display the state of the current branch. If you now checkout to master, those changes you have just made will not be displayed in the editor. Then when moving back to develop, they will appear again.

## Person Two

Person Two is going to work on a feature and merge it into develop.

1. Accept the invitation (you will have been sent an email).
2. Clone the repo. You will now have all the existing branches from the remote in your local cloned version.
3. Checkout to the develop branch - `git checkout develop`. (Notice there is no `-b` flag in the command because we are not creating a new branch, we are checking out to an exiting branch).
4. Create a new new feature branch - `git checkout -b feature/add_default_param` - notice we are branching off of the develop branch, so our new branch will be the same as develop.
5. Refactor the function to have a `name` parameter with a default value:
```js
const helloWorld = (name = "World") => {
  return `Hello ${name}!`;
}
```
6. Add and commit the changes
7. Push to the feature branch - `git push origin feature/add_default_param`.

We know that 'feature/add_default_param' local and remote branches are the same.

### Merging

Person two is happy that their feature branch is finished, and now wants to integrate their changes into develop. However, person two doesn't know if someone else has made changes to develop while they have been working on their feature branch, so they need to start by getting the latest version of develop.

1. Checkout develop - `git checkout develop`.
2. Pull develop - `git pull origin develop` - we now know that develop remote and local are the same so we can go ahead with the merge.

The end goal is having all our changes integrated into develop.

The principle of merging is that we first merge the stable branch (develop) into the feature branch, so we can fix any conflicts in the feature branch, before merging into develop. This means that develop is always stable.

3. Checkout to the feature branch.
4. Merge develop into feature/add_default_param - `git merge develop`. You can think of the merge command as "pulling" the branch specified in the command into your current branch. Make sure you are in your feature branch. We want to deal with any conflicts in the feature branch before merging into develop. (**If git tells you that your branch is 'already up-to-date', skip to the next section: 'Merging Feature into Develop'**)
5. Resolve any conflicts. When merging, sometimes there are conflicts. This means that git can't automatically merge the changes. Git will list the files that contain the conflicts in the terminal window. For exmaple:

```
CONFLICT (content): Merge conflict in greet.js
Automatic merge failed; fix conflicts and then commit the result.
```

If you open the file in Atom you will see something like the following:

![Git Conflict](images/conflict.png)

_Unresolved Git Conflict in the Editor_

The 'head' section shows your branches state, and the 'develop' section shows the state of the develop branch. You need to edit the file to be how you want it, check your code still runs, then add, commit and push the changes to your feature branch.

The "Use me" buttons are added by the Atom text editor, but the symbols (`<<<<<<<`, `=======` and `>>>>>>>`) are just text that has been added to your file. You must remove the symbols, and combine the two versions of the file to create the finished. Atom's "Use me" feature tries to make this easier, allowing you to choose one version and removing the symbols for you. However, you do not have to use this, you can just edit the file yourself.

Now you know your feature branch has all the latest changes from develop integrated, so you can merge it back into develop without any issues.

6. Add & commit your changes
7. Push to the feature branch. We now know local and remote of our feature are the same and that we have the latest version of develop integrated with our changes.

#### Merging Feature into Develop

Now want to merge our feature into develop:

1. Checkout develop - `git checkout develop`.
2. Do a pull on develop just to double check no new changes have been made on develop in the meantime - `git pull origin develop`. Note: If changes had been made to develop, you would revert back to step three of previous section.
3. Merge feature/add_default_param into develop - `git merge feature/add_default_param`. There should be no conflicts at this stage, as we already dealt with any conflicts on the feature branch.
4. Push to develop - we now know that the local and remote are the same in develop and our feature branch has been merged.

## Merging with conflicts

Each person is now going to work on a branch simultaneously, and a conflict is going to be created that you will need to handle.

Each person should:

1. Double check they have all the latest changes on develop - `git pull origin develop`
2. Make their own fix branch (Ensure you branch off develop):
  - Person 1: 'fix/implicit_return',
  - Person 2: 'fix/rename_function'.
3. Complete the fixes:
  - Person 1: Refactor the function to use the arrow function's implicit return
  ```js
  const greet = (name = "World") => `Hello ${name}!`;
  ```
  - Person 2: Rename the function from `helloWorld` to `greet`.
4. Both should add and push their changes to their respective branches.
5. One after the other, each person should follow the above merging process, finishing with all changes merged into develop.

## Merge into Master

Finally merge develop into master following the same merging process as above. First merging master into develop, dealing with any merge conflicts on develop, (there shouldn't be any in this case) and then merging develop into master.
