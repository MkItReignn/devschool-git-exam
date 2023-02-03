# Git Exercise

Please clone this [Git repository](https://github.com/imc-trading/devschool-git-exam).

1. Check out the branch `resume`. Change the commit message from "Add Wok Experience" to
   "Add Work Experience". What commands did you run?

```bash
git checkout resume
git commit --amend -m "Add Work Experience"
```

2. Add this "Work Experience" item in "Resume.md":

```
### The Normal Brand

- Web Developer -- 2019-2021
  - Implemented OAuth login process to support Social Login.
  - Added web analytics
```

Commit it on the branch `resume` with the message "Add Normal Brand item". What command(s) did you run?

```
git commit -m "Add Normal Brand item"
```

3. The commit on the branch `resume` with the message "fill edu" has some issues. Fix it like this: 1. Change the
   message to "Add content for Education section". 2. The commit has introduced some whitespaces at the end of two lines.
   Remove those. What command(s) did you run? Explain your actions.

```
git rebase -i HEAD~3
# Change first commit to 'edit'
git commit --amend -m "Add content for Education section"
# Not sure what whitespaces at the end of two lines...
```

4. The commit with the message "Add empty lines" is not useful. Remove it from the history. What command(s) did you run?

```
git rebase -i HEAD~4
# Remove the first commit
```

5. There is a branch called `skills`. How can you show the content of the `Resume.md` file on that branch without
   switching to the branch?

``` 
git checkout skills Resume.md # I think there is no other way?
```

6. On the branch `skills` there is a commit called "Add skills". Add that commit on top of the branch `resume` without
   switching branches away from `resume`. That should create a conflict. Fix it by incorporating both the previous and
   the new changes. What commands and actions did you do?

```
git cherry-pick 7c050af
vim Resume.md
git add Resume.md
git cherry-pick --continue
```

7. In `Resume.md` there is a line `### Illinois State University`. How can you find out what is the last commit that
   changed/introduced that line? What is the message of that commit? What commands did you run?

```
git log -S "### Illinois State University" --oneline
```

8. Create a branch called `letter_of_intent` forking off from the branch `job_applications`. Create a file there called
   `letter.txt` with the content `I need this job, please!`. Commit this file on the `letter_of_intent` branch with
   the commit message `Add letter of intent`. Add another commit that adds this line to `letter.txt`: 
   `Sincerely yours, Norman`. Commit it with the message `Sign letter`. What commands did you run?

```
git checkout job_applications
git checkout -b "letter_of_intent"

echo 'I need this job, please!' > letter.txt
git add letter.txt
git commit -m "Add letter of intent"

echo 'Sincerely yours, Norman' >> letter.txt
git add letter.txt
git commit -m "Sign letter"
```

9. Rebase the `letter_of_intent` onto the `resume` branch without including the commits on the
   `job_applications` branch. Basically add the commits `Add letter of intent` and `Sign letter` on top of `resume`
   without changing `resume` and point `letter_of_intent` to the last commit. Do not use `cherry-pick`.
   What command did you run?

```
git rebase --onto resume job_applications letter_of_intent
```

10. Merge the branch `letter_of_intent` into the branch `resume`. What commands did you run? Explain the merge strategy
    taken.

```
git checkout resume
git merge letter_of_intent
# Merge strategy is fast forward
```

11. Merge the `job_applications` branch into the branch `resume`. What commands did you run? What merge strategy was
    taken? What happened to the git history of the `resume` branch?

```
git merge job_applications
# 'ort' strategy -> had to make a new commit
# New commit had to be made to combine the resume branch tip, 
# job_applications branch tip and the divergent ref
```
