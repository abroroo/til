## Git Submodules

So me and my friend were working on a project, frontend and backend, with one git repo. I was making updates in the frontend, and he was in the backend, and we were committing our changes in our respective folders only, `git add ./backend` or `git add ./frontend` and pushing them to the repo.

However, we've got a problem: whenever either of us pushed changes in our designated folder, it unintentionally overwrote the contents of the `/frontend` or `/backend` directory too.

Then we learned about **[git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)** , this [article](https://github.blog/2016-02-01-working-with-submodules/) also explains it well

***Submodule is a repository embedded in your main repository. It is mostly used to include another project within your main project.***

 
It was also useful in our case, where we had a backend in Django and a frontend in Next.js

### How To Use git submodules in Your Project Where You Have Backend and Frontend in Different Environments.  
1. First create separate repos for the backend and frontend. aka "submodules"
2. Then create the main repository to include your backend and frontend as submodules.
   * `git init myProject cd myMainProject`
3. In the root of your myMainProject, add frontend and backend as submodule
   * `git submodule add <repository_URL> frontend`
   * `git submodule add <repository_URL> backend`
     
   _Note:_ This submodules aren't cloned yet

4. Initialize (set up) the submodules. 
   * `git submodule init ` It adds the necessary submodule metadata to the repository so that Git is aware of the submodules.
5. Fetch the contents of the submodules according to the recorded commit in the main repository.
   *  `git submodule update`
     
   _Note:_ Above steps 4 and 5 can be run with one command `git submodule update --init --recursive`

   The `--recursive` flag makes sure that submodules of submodules are also initialized and updated.

    **You are all set up by now**

### But How do you commit your changes to submodules now?

 > Because of sub­mod­ules are ​“sta­t­i­cal­ly point­ed” at a spe­cif­ic com­mit object, you need ensure that you **push any changes to the sub­mod­ule project before you push up changes to the par­ent project**. If you don’t, you’ll have a par­ent project link­ing a sub­mod­ule at a com­mit object that doesn’t yet exist in a remote repository.

1.  Go to your respective submodule `cd frontend` or `cd backend`, and make your changes. 
2.  Commit your changes as usual `git add .` & `git commit -m " " `
3.  Within your submodules, push the changes `git push`
4.  ***Important part***
    * Go back to myMainProject `cd myMainProject`
    * Run `git submodule update --remote`
      
    `--remote` **option**: When you add `--remote`, it tells Git to fetch the latest changes from the upstream repository of each submodule. Without this option, Git only updates to the commit recorded in the myMainProject, not fetching the latest changes from the submodule's remote repository.

    Now you can continue working in your respective submodule, and pushing changes as above. 

### When collaborating on someone else's project that includes integrated submodules.

#### Cloning with Submodules
  * `git clone --recursive <MainProject_URL>`
#### Pulling Changes
  *  `git pull`
  *  `git submodule update --recursive --remote`



