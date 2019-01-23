# Git Pull Activity

## Setup

We've talked about using `git push` to send local changes to GitHub, but when using git to collaborate with others it's likely that you'll end up in the opposite situation, where there are changes on GitHub you don't have locally. Git provides the `git pull` command to handle this.

To demonstrate `git pull`, we've provided a repository to work with. Follow these instructions to get started:

1. Find a partner
1. **One** partner should fork the repository linked in the calendar
1. Whoever forked the repo should add the other partner as a collaborator.
1. **Both** partners should clone the forked repo.
1. **Both** partners should open `pull_practice.rb` in VS Code.

## Pulling Changes From GitHub

Look at `Task 1` in the `pull_practice.rb`.

1. **Partner 1** should uncomment the `duck_noise` method and save the file.
1. **Partner 1** should then `git add` the file, `git commit`, and `git push`. You should now be able to see the changes on GitHub.
1. **Partner 2** should run `git pull`. This will retrieve all commits from GitHub that aren't yet on the local repository.
1. You should now be able to see the `duck_noise` method uncommented in partner 2's copy of the repo.

Switch roles and do the same thing for `Task 2`, the `truck_noise` method.

Running `git pull` when you don't have any changes is also known as performing a _fast-forward merge_.

## Merging Changes

What happens if both partners have made changes? Turns out git is pretty intelligent about putting together work from different sources. Most of the time, even if you're working in the same file, it can figure out the right thing to do.

Turn your attention to `Task 3` in the activity. Here are your instructions:

1. **Partner 1** should uncomment the `robot_noise` method and save the file.
1. **Partner 1** should then `git add` the file, `git commit`, and `git push`. You should now be able to see the changes on GitHub.
1. **Without pulling**, **Partner 2** should now uncomment the `train_noise` method and save the file.
1. **Partner 2** should then `git add` the file and `git commit`.
1. If **Partner 2** tries to `git push`, they should see an error message something like this:

    ```
    $ git push
    To https://github.com/droberts-ada/git-pull-activity.git
     ! [rejected]        master -> master (non-fast-forward)
    error: failed to push some refs to 'https://github.com/droberts-ada/git-pull-activity.git'
    hint: Updates were rejected because a pushed branch tip is behind its remote
    hint: counterpart. Check out this branch and integrate the remote changes
    hint: (e.g. 'git pull ...') before pushing again.
    hint: See the 'Note about fast-forwards' in 'git push --help' for details.
    ```

    Git won't let you push if there are changes on the server that you don't have locally. This is a good thing! It reduces the chance of something going wrong.
1. **Partner 2** should now `git pull`. These two changes should be compatible, but git will still need to do some work to put them together. Like any other piece of work, the merge needs to have a commit, so git will open up ask for a commit message. The default message is perfect, and it's standard to accept the default commit message. Finishing this commit message will allow the pull process to finish-- you have completed pulling the `git pull` (fetch and merge) command with this!
1. After doing a merge, it's always wise to check git's work. **Partner 2** should open up the file and verify that the two commits were merged cleanly. Both methods should be uncommented. In the real world, you would run your tests and make sure nothing broke.
1. **Partner 2** is now free to push their work to GitHub.

## Merge Conflicts

As clever as Git may be, sometimes there's not an obvious right way to merge two changes. This situation is called a _merge conflict_. In this case the only way forward is for a human to do the merge by hand.

`Task 4` demonstrates a merge conflict. Instructions are as follows:

1. **Partner 1:** Change the `clock_noise` method to `puts "tick"`, save, add, commit and push.
1. **Partner 2:** **Before pulling**, change `clock_noise` to `puts "tock"`, and save, add and commit.
1. **Partner 2:** Try to push. As before, git should warn you that your local copy is out of date.
1. **Partner 2:** Now run `git pull`. Git should tell you that there's a merge conflict! It has also modified `pull_practice.rb` to tell you what the conflict is. The `clock_noise` method should now read as follows:

    ```ruby
    def clock_noise
    <<<<<<< HEAD
      puts "tock"
    =======
      puts "tick"
    >>>>>>> master
    end
    ```

    Git has included both versions of the method, and labeled where they came from. `HEAD` is the local copy, and `master` is the version from GitHub.
1. **Partner 2:** Work with your partner to resolve the conflict.
    - Using VS Code, pick which of the versions you want to use, and remove all the extra stuff that GitHub added. The end result should be valid ruby code.

      ```ruby
      def clock_noise
        puts "tick tock"
      end
      ```

    - Use `git add pull_practice.rb` to mark the conflict as resolved.
    - Use `git commit` to finish the merge.
1. **Partner 2:** Is now free to push their work to GitHub.

This one was simple, but in the real world merge conflicts can get _really_ hairy. But as weird as it can be, without git collaboration would be a thousand times more difficult. We'll talk more about resolving merge conflicts in another lecture.
