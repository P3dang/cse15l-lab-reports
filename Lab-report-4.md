**Log into ieng6:**
  ![image](Screen Shot 2023-05-21 at 5.50.17 PM.png)
  type `ssh cs15lsp23__@ieng6.ucsd.edu`, press <enter>, type password, press <enter>. This allows us to get access to out remote server, and get access to bash. 

**Clone your fork of the repository from your Github account:**
  <img width="1469" alt="image" src="https://github.com/P3dang/cse15l-lab-reports/assets/130012963/d0a04f81-dfef-45da-a7e5-d2132dfc4a47">
  Open https://github.com/ucsd-cse15l-s23/lab7, click on Fork, click on Creat Fork, click on URL, press `<command>` + a, press `<command>` + c, type `git clone`, press `<command> + v`, press `<enter>`.

**Run the tests, demonstrating that they fail:**
  
  <img width="621" alt="image" src="https://github.com/P3dang/cse15l-lab-reports/assets/130012963/45aba19c-cc2c-4299-9a92-a39b49f59126">
 
  type `cd lab7/`, type `bash test.sh`, press `<enter>`. Inorder for us to run the file, we first have to enter the directory the file is in. For this we use `cd lab7/`. Now that we have entered the directory, we use bash to compile and run the test. Without any modification to the ListExamples.java file, one of the test should fail.  
  
**Edit the code file to fix the failing test:**
  
  <img width="373" alt="image" src="https://github.com/P3dang/cse15l-lab-reports/assets/130012963/17954959-106d-42f6-9e4a-eb68c297a53c">
   
  type `vim L`,press `<tab>`, type `.`, <tab>, <enter>, press `J` 43 times, press `L` 11 times,

  <img width="378" alt="image" src="https://github.com/P3dang/cse15l-lab-reports/assets/130012963/e1da83b5-ef2d-4963-8dde-26714ea3a5b0">
 
   press `X`,
  
  <img width="369" alt="image" src="https://github.com/P3dang/cse15l-lab-reports/assets/130012963/50dcc502-97f4-4862-962f-8231efcb797c">

   press `I`, type `2`, press `<esc>`, type `:wq:`, press `<enter>`
  
  Inorder for us to edit the java file, we have to use a text editor called `vim`. When we have entered a file via vim, there are many commands we can use to edit and move around the file. To move press h(left), l(right), j(down), k(up). To start editing the code press `i` to enter insert mode. When you're done editing `<esc>` and `:wq` to save and exit the file. 
  
**Run the tests, demonstrating that they now succeed:**

  <img width="395" alt="image" src="https://github.com/P3dang/cse15l-lab-reports/assets/130012963/3d8575fe-2983-4201-ba73-e24099b269d3">
  
  press `<up-arrow>` 2 times, press `<enter>`. Pressing `<up-arrow>` allows us to recall previous commands we have used. 
  
**Commit and push the resulting change to your Github account (you can pick any commit message!):**
  <img width="508" alt="image" src="https://github.com/P3dang/cse15l-lab-reports/assets/130012963/63ebab6b-e3cb-434d-bb83-027fc79a8bba">
  
  type `git commit -a`, press `i`, type any message, press `<esc>`, type `:wq`. Calling `git commit -a` allows us to record all the changes that has happened to all the files. The messages allows us to add notes to the commits. 
  
  <img width="531" alt="image" src="https://github.com/P3dang/cse15l-lab-reports/assets/130012963/97f8dbbc-3e2a-4d09-bedb-d92bb7fccf58">
  
  type `git push`, enter your username and password, press `<enter>`. Calling `git push` allows us to upload our files into github, updating our previous repository. 
  
  
