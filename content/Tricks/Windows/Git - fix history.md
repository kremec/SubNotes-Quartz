[Gitleaks](https://github.com/gitleaks/gitleaks) detects any leaked secrets - passwords, keys, ... in git repos.

The commits need to be local only, not pushed to remote, as with git reflog (knowing the problematic commit's hash), anyone can use `git fetch origin <COMMIT HASH>` to see the history, even if rewritten with following solutions.

- If the secret is in the last commit:
`git reset --soft HEAD~1` goes back 1 commit from the latest and puts all reset commits into staged changes.
You can now edit files, stage changes to git and commit.
  
- If the secret is in one of the earlier commits, git reset will override all commits up to this one:
Instead, get the commit hash of the commit to change, and use it in interactive git rebase: `git rebase -i <COMMIT HASH>~1`
This will open the default text editor with options of what to do with commits up to to the problematic one.
The default option is `pick` which will change nothing. Change the option before the (top) problematic commit to `e` or `edit`.
Once you save and exit the editor, you are brought to shell that is inside rebase mode.
You can now edit files, stage changes and use `git rebase --continue`, which will open the text editor once again, this time to edit the commit message.
When ready, save and exit the file, then the rebase will continue.
Likely, you will encounter merge conflicts, which you resolve normally.