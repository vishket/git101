### Pull Request 101

###### MAC
Step 1: Check for SSH keys

---
1. Check for existing SSH keys on your computer. Open Terminal and enter:  
`$ ls -al ~/.ssh`  
`# Lists the files in your .ssh directory, if they exist`
        
2. If there are files in your .ssh directory then check the directory listing to see if you already have a public SSH key. By default, the filenames of the public keys are one of the following:

       
	- id_rsa.pub
	- id_dsa.pub
	- id_ecdsa.pub
	- id_ed25519.pub

3.If you see an existing public and private key pair listed (for example id_rsa.pub and id_rsa) that you would like to use to connect to GitHub, you can skip **Step 2** and go straight to **Step 3** .

            
Step 2: Generate a new SSH key
---
1. In the terminal window, enter the following:  
`$ ssh-keygen`

2. Press enter for the next three prompts.

3. You'll be given the fingerprint, or id, of  your SSH key.  It will look something like this:  

    `Your authentication has been saved in /Users/==you==/.ssh/id_rsa.`  
    `Your public key has been saved in /Users/==you==/.ssh/id_rsa.pub`  
    `The key fingerprint is:`  
    `01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your_email@us.ibm.com`

Step 3: Add your SSH key to your account
---
1. Copy the SSH key to your clipboard. In Terminal type:  
`cat ~/.ssh/id_rsa.pub`

2. Select and copy the output to your clipboard.

3. In the top right corner of any GitHub page, click the gear icon.

4. In the user settings sidebar, click **SSH keys**.

5. Click **Add SSH key**.

6. In the title filed, add a descriptive label for the new key. For example, if you're using your MacBook, you might call this key MacBook.

7. Paste your key in the "Key" field.

8. Click **Add key**.

Step 4: Test the connection
---
To ensure everything is working, SSH into GitHub Enterprise:

1. Open a terminal window and enter:  
    ` $ ssh -T git@github.ibm.com`  
    ` # Attempts to ssh to GithHub Enterprise`

2. If you see the following warning:  
    `The authenticity of host 'github.ibm.com (9.45.202.184)' can't be established.
    RSA key fingerprint is 5f:4f:03:35:22:4d:02:f9:d1:a1:58:13:f3:ac:b1:54.
    Are you sure you want to continue connecting (yes/no)?'  
Type `yes`.

3. If you see the following message with your username, you've successfuly set up your SSH key!  
    `Hi **username**! You've successfuly setup your SSH key!`

Step 5: Do some onetime-github setup
---
From a terminal window:

1. Type `git config --global user.name "Your githubt username"`
2. Type `git config --global user.email "you@country.ibm.com"`
3. Confirm the information by entering `git config --list`

Step 6: Fork the Repo
---
1. Navigate to [The Practice Repo](https://github.ibm.com/millarde/pull-request-exercise) in the Github web interface.
2. In the top-right corner of the page, click **Fork**.
3. You may be prompted with the following question:  
    "Where should we fork this repository?"  
    Select your name from the list. 
4. That's it!  You've forked the original repo. This means that a new repo has been created underneath your account on github.ibm.com.  In the next step, we will make a local copy.

Step 7:  Create a local clone of your fork:
---
Right now, you have a fork of the repo, but you don't have the files in that repository on your computer.  Let's create a  clone of your fork locally on your computer.

1. On [github](https://github.ibm.com), navigate to your fork's repository page.  You can find it by going to your profile and then clicking on repos. If you just finished the previous step, it should already be open to the desired page.
2. In the right sidebar, look for the text that reads "*You can clone with HTTPS, SSH, or Subversion*". Click the SSH link.
3. Copy the ssh clone command into your clipboard.
3. Open Terminal.
4. Navigate to the directory in which you want to clone your fork.  
    Tip: You are probably in your root directory, you may want to create a directory for your repos (eg mkdir repos).
5. Type `git clone`, and then paste the command that you copied in Step 2.
6. Press **Enter**. Your local clone is created.
7. If you receive a message indicating that you need to install Developer Tools, click **Install**.
![Picture of Install Prompt](/images/commandLineDevTools.png)

Step 8: Configure Git to synch your fork with the original repository
---
When you fork a project to propose changes to the original directory, you can configure Git to pull changes from the original, or *upstream* repository into your local clone of your fork.

1. In the terminal window and go to the root of your local cloned repo.  Type `git remote -v` and press **Enter**. You'll see the current configured remote repository for your fork.
![Picture of window](/images/gitRemote.png)
2. **IMPORTANT: Make sure that you read this step carefully.  Don't copy your own repo cloned command** 
Go to the repo that you forked **FROM** (jimjones) and copy the ssh clone command.  In this case, you can go [here](https://github.ibm.com/jimjones/devops_learning_repo)
3. At your command prompt, type `git remote add upstream URL_COPIED_IN_STEP_2`
4. To verify the new upstream repository you've specified for you fork, type `git remote -v`.  You should see the URL for your fork as `origin` and the URL for the original repository as `upstream`.

Step 9:  Add to the story for your pair -- be sure to edit the right file:
---
In the terminal window:  
1. Checkout a local branch by entering `git checkout -b <your_name>`.  
2. Edit the appropriate file by whatever means you want to add to the story.  
3. From the root of your local repo, type `git add .`  
4. Then type `git commit -m "Added <your_name> content"`.  
5. Then type `git push origin <your_name>`.  

Step 10: Create a pull request:
---
1. Go to the repo where you want to submit the pull request (for this exercise, the one we started with: https://github.ibm.com/millarde/pull-request-exercise). It should look similar to this:
![picture of github dashboard with Pull Request Prompt](/images/pullRequest.png)  
2. Click on the Green `Compare & Pull Request` buttton. If you left that window open in a browser, you may need to refresh it to see this. You should be rewarded with a screen similar to the following:
![Picture of pull request console](/images/openPullRequest.png)  
3. Check the following details by the numbers:  
    1. You should see your change in green.  
    2. Make sure that the base fork is pointing to millarde/pull-request-exercise
    3. Make sure that the head fork is pointing to yourname/pull-request-exercise
4. Add a comment by box 4.  
5. Click `Create pull request`.  
6. Slack your partner that you've submitted a request (they should also get an email).  

Step 11: Bring your local fork up to date:
---

Navigate to your local copy of the repo and from within that directory, enter the following commands.

1. `git checkout master`  
2. `git fetch upstream`  
3. `git merge upstream/master`  
4. `git add .`  
5. `git commit -m "Bring local repo up to date"`  
6. `git push`  

