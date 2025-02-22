# Git init - Creation of .git File

`git init` initializes a Git repository by creating a `.git` directory with some files & directories inside it. The .git folder is usually hidden.

<figure><img src=".gitbook/assets/image.png" alt="" width="351"><figcaption><p>The File Structure of .git folder.</p></figcaption></figure>



* `config` is a text file that contains your git configuration for the current repo. If you look into it, you would see some basic settings for you repo like the author, filemode etc.
* `HEAD` contains the current head of the repo. Depending on what you have set your "default" branch to be, it will be `refs/heads/master` or `refs/heads/main` or whatever else you had set to. This would be written as soon as you add the file to the staging area. As you might have guessed, this is pointing to `refs/heads` folder that you can see below, and into a file called `master` which does not exist as of now. This file `master` will only show up after you make your first commit.
* `hooks` contain any scripts that can be run before/after git does anything. Although we haven't yet explored hooks as a part of this project, so this is where it starts and ends.
* `objects` contains the git objects, i.e the data about the files, commits etc in your repo. This is where all the git objects are stored and this where we would work the most.
* `refs` as we previously mentioned, stores references(pointers). `refs/heads` contains pointers to branches and `refs/tags` contains pointers to tags.
* `info` directory keeps a global exclude file for ignored patterns that you don’t want to track in a `.gitignore` file.

Git was initially a toolkit for a version control system rather than a full user-friendly VCS, it has a number of subcommands that do low-level work. These commands are generally referred to as Git’s “plumbing” commands, while the more user-friendly commands are called “porcelain” commands.
