#Merge
- this is a wrong notes doc


- well here is some new correct notes

### conflicts

- given 2 branches with conflicts
- *ours*: dump conflicts on the branch, master wins
- *theirs* dump conflict on master, branch wins

- now inside the repo, create a branch using the following command:
```shell
> git checkout -b feature/uniform_hellos
```
- commit something on the feature/uniform_hellos branch

- switch to master
```shell
> git checkout master
```
- commit someting on the master

- now compare the two branches
```shell
> git diff master feature/uniform_hellos
```
- You are currently on master, try merging from the feature branch
```shell
> git merge feature/uniform_hellos
```
- you will get the following message
```shell
Auto-merging people/mary.rb
CONFLICT (content): Merge conflict in people/mary.rb
Automatic merge failed; fix conflicts and then commit the result.
git_playground $ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)

	both modified:   people/mary.rb

no changes added to commit (use "git add" and/or "git commit -a")

```
- the source code will show the conflict
```ruby
module People

  class Mary
    def name
<<<<<<< HEAD
      "hello, I'm mary from feature 2"
=======
      "hello, I'm mary from master"
>>>>>>> master
    end
  end
end

```
- Now in order to resolve conflicts, there are three options

1.use our code (we are currently master)
```shell
> git checkout --ours people/mary.rb
```

OR

2.use their code (because we are currently master, this means we are using the branch code)
```shell
> git checkout --theirs people/mary.rb
```

OR

3.MANNUALLY CHANGE THE CONFLICS

```ruby
module People

  class Mary
    def name
#<<<<<<< HEAD
#      "hello, I'm mary from feature 2"
#=======
#      "hello, I'm mary from master"
#>>>>>>> master

    "hello i'm mary from master and feature"

    end
  end
end
```

```shell
> git add people/mary.rb

> git commit -m "merging feature2 to master"
```
- example
```git
git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   people/bob.rb
	modified:   people/mary.rb

no changes added to commit (use "git add" and/or "git commit -a")
git_playground $ git commit -a -m "adding lalalal to master"
[master 48b0598] adding lalalal to master
 2 files changed, 2 insertions(+), 2 deletions(-)
git_playground $ git push origin master
fatal: 'origin' does not appear to be a git repository
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
git_playground $ git diff master feature/uniform_hellos
diff --git a/people/bob.rb b/people/bob.rb
index 4d8fa38..362061c 100644
--- a/people/bob.rb
+++ b/people/bob.rb
@@ -1,7 +1,7 @@
 module people
   class Bob
     def name
-      "Hello, i'm Bob, allalalal"
+      "Hola, i'm Bob"
     end
   end
 end
diff --git a/people/mary.rb b/people/mary.rb
index 7a5f828..ea3f8ea 100644
--- a/people/mary.rb
+++ b/people/mary.rb
@@ -1,7 +1,7 @@
 module people
   class Mary
     def name
-      "Hello, i'm Mary, alalal"
+      "Hola, i'm Mary"
     end
   end
 end
```

#Fork
- owner has access to upstream
- contributors send pull request instead of merge
