# git-multiple-ssh

When you have multiple accounts on GitHub, you can use `~/.ssh/config` to set up different configurations for each account, and then modify the URL when you use `git clone`. This script can help you avoid manually modifying the URL each time.

# Install
Copy the git file from this project to `/usr/local/bin/git` or another location, and set the environment variable to make it the default `git` command.

Example:
```
$ where git
/usr/local/bin/git
/usr/bin/git

$ which git
/usr/local/bin/git
```

# Usage
`git ssh <github account> <ssh key file> [git user.name] [git user.email]`

Example: 
```
$ git ssh user1 ~/.ssh/company user1 user1@xxx.com
```

This will add the following configuration to `~/.ssh/config` :
```
# Generated by git-multiple-ssh. DO NOT EDIT. user1 company.github.com user1 user1@xxx.com
Host company.github.com
    User git
    Hostname github.com
    IdentityFile /Users/liuchao/.ssh/company
```

When executing `git clone git@github.com:user1/project.git` , it actually executes:
```
git clone git@company.github.com:user1/project.git
cd project
git config user.name user1
git config user.email user1@xxx.com
```

You can add multiple users to an ssh key.

```
$ git ssh user2 ~/.ssh/company user2 user2@xxx.com
```

The configuration in `~/.ssh/config` is:
```
# Generated by git-multiple-ssh. DO NOT EDIT. user1 company.github.com user1 user1@xxx.com
# Generated by git-multiple-ssh. DO NOT EDIT. user2 company.github.com user2 user2@xxx.com
Host company.github.com
    User git
    Hostname github.com
    IdentityFile /Users/liuchao/.ssh/company
```
