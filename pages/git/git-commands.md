<div align='center'>

# Git-Commands
</div>

## A. General

- #### `Create Git`
    ```bash
    git init
    ```

- #### `Add All Files`
    ```bash
    git add .
    ```

- #### `Commit`
    ```bash
    git commit -m "Your Message"
    ```

- #### `Add & Commit together`
    ``` bash
    git commit -am "Your Message"
    or,
    git commit -a -m "Your Message"
    ```

- #### `Push`
    ```bash
    git push -u origin main
    or,
    git push
    ```

- #### `Clone`
    ```bash
    git clone [url-link.git]
    ```

- #### `Fetch`
    ```bash
    git fetch
    ```

- #### `Pull`
    ```bash
    git pull
    ```

- #### `Check file status`
    ```bash
    git status
    ```

- #### `Check all log`
    ```bash
    git log
    ```

- #### `Merge file`
    ```bash
    git merge <branch-name>
    ```
    <i>This command merges the specified branch’s history into the current branch.</i>
    
- #### `Undo merge before commit & push`
    ```bash
    git merge --abort
    ```
 
- #### `Steps to remove directory from Repository`
    ```bash
    git rm -r --cached YourFolderName
    git commit -m "Removed YourFolderName from repository"
    git push origin main
    ```

    
- #### `Check remote origin`
    ```bash
    git remote -v
    ```

- #### `Change remote origin`
    ```bash
    git remote set-url origin https://github.com/......
    ```

- #### `Add remote url`
    ```bash
    git remote add origin [url-link]
    ```

- #### `To push with new branch`
    ```bash
    git push --set-upstream origin <New-Branch>
    ```

- #### `To Check Remote Origin`
    ```bash
    git remote -v 
    ```

- #### `To change remote origin`
    ```bash
    git remote set-url origin https://github.com/......
    ```
	
- #### `If gitignore not working, then run this command`
    ```bash
    git rm -r --cached directory/sub-directory
    ```
    then use `git add .` , `git commit -m message` & `git push` 
	   
<br>

## B. Branch

- #### `Check all branch List`
    ```bash
    git branch
    ```
- #### `Create New Branch`
    ```bash
    git branch <Your-Branch-Name>
    ```
- #### `Push the new branch in github`
    ```bash
    git push --set-upstream origin <Your-New-Branch-Name>
    ```
- #### `Switch Branch`
    ```bash
    git checkout <Branch-Name>
    ```
- #### `Delete branch locally`
    ```bash
    git branch -d <Branch-Name>
    or,
    git branch -D <Branch-Name>
    ```
    <i>The -d option will delete the branch only if it has already been pushed and merged with the remote branch</i> 
    <br><br>
    <i>
    -D instead if you want to force the branch to be deleted, even if it hasn't been pushed or merged yet.
    </i>


- #### `Delete branch remotely`
    ```bash
    git push origin --delete <Branch-Name>
    ```
    
### Merging branch via command line:
If you do not want to use the merge button or an automatic merge cannot be performed, you can perform a manual merge on the command line. However, the following steps are not applicable if the base branch is protected.
- Step 1: Clone the repository or update your local repository with the latest changes.
```bash
git pull origin develop
```

- Step 2: Switch to the base branch of the pull request.
```bash
git checkout develop
```

- Step 3: Merge the head branch into the base branch.
```bash
git merge tenant-authorization
```

- Step 4: Push the changes.
```bash
git push -u origin develop
```

### Fetch new branch from remote to local machine:
If a team member has created a new branch on the GitHub server and you want to fetch and work with that branch locally, you can follow these steps:

- Step 1: Fetch Branches from the Remote
```bash
git fetch origin
```

- Step 2: List Remote Branches
```bash
git branch -r
```

- Step 3: Check Out the New Branch
```bash
git checkout -b new-branch-name origin/new-branch-name
```
This command will create a new local branch named branch-name that tracks the remote branch of the same name. It also checks out the new branch so you can start working on it.


- Step 4: Push Changes to the Remote (Optional)
```bash
git push origin new-branch-name
```
<br>

## C. Publish your private assignments in your github public repository

- #### `Check Current URL`
    ```bash
    git remote -v
    ```

<i>Then create a new repository. After get new repository link update something in your locale machine which is in private mode. Copy the new url and jus change <b>set-url</b> instead of <b>add</b></i> 

```bash
git remote set-url origin https://github.com/Irfan-Chowdhury/your_new_repository.git
```

```bash
git push
```

<br>

## D. Undo last commit from local and remote 

- #### `Locally`
```bash
git reset --soft HEAD~1
```

- #### `Remotely`
```bash
git push origin +HEAD
```

<br>

## E. Tag
- #### `For Releasing New Version`
```bash
git tag -a v0.1.2 -m "Release v0.1.2"
git push --follow-tags
```

<br>

## F.  Control your specific files/directory to visible/hide in GitHub
- #### `For remove/hide`
```bash
git rm -r --cached app/Http/Controllers
```

- #### `For add/visible`
```bash
git add -f app/Http/Controllers/Landlord
```
- #### `After doing these, please run these commands given below` 
```bash
git commit -m "Control my controller files"
git push origin main
```
<br>

## G. Pushing Issues
If you face authenticate issue during try to push from terminal, first check which remote url exists in your repository. 
- check remote url
```bash
git remote -v
```
- if url start with `https://github.com/` then replace with `git@github.com`. For example, suppose your url is `https://github.com/Irfan-Chowdhury/Git-Commands.git`. Now set with `git@github.com:Irfan-Chowdhury/Git-Commands.git`.
```bash
git remote set-url origin git@github.com:Irfan-Chowdhury/Git-Commands.git
```
Now you can push easily from your terminal.

## H. Explore Git

- ### `Git Restore`
    ```bash
    git restore . 
    ```
    git restore কমান্ডটি মূলত আপনােক কোন ফাইল বা ডিরেক্টরি আগের অবস্থায় (শেষ কমিটের অবস্থায়) ফিরিয়ে আনতে সাহায্য কের। ধরেন আপনার অলরেডি কমিটেড একটা  প্রজেক্টের নতুন একটা ফিচার ডেভ্লপ করার চেষ্টা করেছিলেন কিন্তু কিছু কোড করার ফলে মনে হল পূর্বের অবস্থায় চলে যাওয়া বেটার তখন এই কমান্ডা ব্যবহার করলে লাস্ট Commit অবস্থায় ফিরিয়ে নিয়ে যাবে ।

- ### `Git Stash`
    যদি কোন কাজের মাঝামাঝি থেকে কোন প্রকার কমিট ছাড়া অন্য কোন টাস্ক বা ব্রাঞ্চে যাওয়া লাগে, ঐ কাজ গুলো টেম্পোরারি কোথাও স্টোর করার জন্য নিচের কমান্ডি ব্যবহার করা যেতে পারে ।  

    ```bash
    git stash . 
    ```
    কমান্ডটি দেয়ার সাথে করা কাজগুলো ভ্যানিশ হয়ে যাবে । চিন্তার কোন কারণ নেই । 

    স্ট্যাশ কমান্ডটি এভাবে করলে আপনার অলরেডি গিটে ট্র্যাক করা (কমিটেড) ফাইল বা ডিরেক্টরির চেঞ্জসগুলাও স্ট্যাশে রাখবে । যদি শেষ কমিটের পর একেবারে নতুন কোন ফাইল অথবা ডিরেক্টরি এড করে থাকেন তাহলে সেগুলা এভাবে স্ট্যাশে যাবেনা সেক্ষেত্রে আপনাকে ফ্ল্যাগ ব্যবহার করে গিটকে বলে দিতে হবে যে আপনি নতুন ফাইল, ডিরেক্ট্রিগুলাও স্ট্যেষে নিতে চান । 
    ```bash
    git stash -u . 
    ```
    <br>
    <b>Listing stashes:</b> You can view a list of your stashes using:
    ```bash
    git stash list
    ```

    <b>Restoring the stash and removing it:</b> for getting latest stash data, you've to command this 
    ```bash
    git stash pop
    ```

    <b>Applying a stash: </b>সুবিধা হল আপনি চেঞ্জেস এপ্লাই করার পরও স্ট্যাশ থেকে এগুলার এক্সেস পাবেন । 
    ```bash
    git stash apply
    ```

    <b>To apply a specific stash :</b>  যদি খেয়াল করেন তাহলে দেখবেন প্রত্যেকটা আইটেমের আগে এখানে stash@{n}, এখানে n মানে নাম্বার দিয়ে মার্ক করা আছে । আপনি এটা ব্যবহার করেও pop অথবা apply করতে পারবেন । 
    ```bash
    git stash apply stash@{3}
    git stash pop stash@{1}
    ```

    <b>Clear Stash :</b> To clear all stashes, you can use this.
    ```bash
    git stash clear
    ```

    <b>Specific Clear Stash :</b> To clear  specific stash, you can use this.
    ```bash
    git stash drop stash@{3}
    ```

- ### `Git Reset`
    ভুলে কোন কমিট করে ফেললে সেটি পূর্বের অবস্থায় ফিরিয়ে আনতে নিমোক্ত কমান্ডটি করতে হবে - 

    ```bash
    git reset <commit_id>
    ```
    যদি উক্ত কমিটের সবগুলাই যদি চেঞ্জ হয়ে যাক চান তাহলে নিমোক্ত কমান্ড 
    ```bash
    git reset <commit_id> --hard
    ```

- ### `Git Revert`
    Reset  - এর মতই তবে এখানে Revert করার এর পর আরেকটি কমিট দেয়া লাগে ।

    ```bash
    git revert <commit_id>
    ```

    Reset এবং Revert এর মধ্যে মূলত পার্থ্য হল -

    Reset কমান্ডে একটি কমিট পর্যন্ত থাকা চেঞ্জেসগুলা পর্যন্ত ফিরে পাওয়া যায় পরবর্তী সব কমিট বাদ দিয়ে । এক্ষেত্রে নতুন কোন কমিট তৈরি হয়না ।

    Revert এর ক্ষেত্রে একটা কমিটের চেঞ্জেসগুলা সব বাদ দিয়ে নতুন আরেকটা কমিট এর মাধ্যম । সেক্ষেত্রে আপনার প্রজেক্টটি গিটহাবে বা রিমোট কোন রিপোতে থাকলে অন্যান্য কন্ট্রিবিউটাররা রিভার্টের কমিটটা দেখতে পাবে এবং কনফিউজড হবেনা । এছাড়াও আপনি গিট লগ দেখলে দেখবেন যেখানে Reset করা হলে কোন প্রমাণ বা লগ পাবেন না সেখানে Revert করা হলে সেটার জন্য আরেকটা কমিট মানে লগ দেখতে পাবেন । 
    
- ### `Git Rebase`

    ```bash
    git rebase main    
    ```
    নরমাল মার্জ করার মতই তবে এক্ষেত্রে লগ ক্লিন থাকে । 
    Details in - 
    <br> 
    <b>Book :</b> "এক পলকে গিটহাব" 
    <br>
    <b>Author :</b> জুনায়েদ আহমেদ  
    <b>Page No:</b> 133
    

- ### `Git Squash`

    If you create another new branch, currently you now in `main` branch and want to merge with the new branch - 
    ```bash
    git merge new-feature --squash      
    ``` 
    নতুন ব্রাঞ্চে থাকা অবস্থায় যত গুলা কমিট করা হয়েছে সেগুলা চাইল সব এক কমিটেই মেইন ব্রাঞ্চের সাথে এড করে দিতে পারবো । এতে লগ ক্লিন থাকে ।
    প্রাথমিকভাবে স্টেজড অবস্থায় পাবেন । 
    উপরক্ত কমান্ডি চালানোর পর আরেকটি কমিট দিতে হবে যাতে সবগুলা চেঞ্জেস যাস্ট একটা কমিটের মাধ্যমে আপনার ব্রাঞ্চে যুক্ত হয়ে যায় - 

    ```bash
    git commit -m “new feature introduced”      
    ``` 
