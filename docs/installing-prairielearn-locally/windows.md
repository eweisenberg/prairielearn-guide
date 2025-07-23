---
title: Windows
layout: default
parent: Installing PrairieLearn Locally
---

# Installing PrairieLearn Locally on Windows



1. Open PowerShell. Install Ubuntu in WSL2 using the command `wsl --install -d Ubuntu`

2. Install [Docker Desktop](https://www.docker.com/products/docker-desktop/). If you don't have an account, create one using your UVA email.

3. In Docker Desktop, go to Settings (gear icon) > Resourses > WSL integration and ensure the following options are selected:<br><br>
![Image]({{ site.baseurl }}/assets/images/docker-wsl-enable-integration.png)

4. Head over to [GitHub](https://github.com/). Go to Settings > Developer Settings > Personal access tokens > Tokens (classic). Select Generate new token > Generate new token (classic). Fill in the following options:
- *Note*: PrairieLearn CS2100
- *Expiration*: Custom > end of the semester (you should create a new token each semester for security)
- *Select scopes*: Check all the boxes in the "repo" section. All other checkboxes should be left unchecked.

5. Click "Generate token". **Copy the token that appears on screen now and save it somewhere.** You will need it later and cannot see it again! If you lose it, you can always create a new token.

6. Go to following GitHub repository: [https://github.com/PrairieLearn/pl-virginia-cs2100](https://github.com/PrairieLearn/pl-virginia-cs2100). This is where all the question, assessment, and course data is stored. If your GitHub account does not have access, please contact Professor Morrison and ask her to add your GitHub username as a collaborator. You need access to this repository to continue.

7. Search for the "Ubuntu" app on your computer and open it. It should launch a terminal window of Ubuntu in WSL2. Run the command `pwd` and ensure you are in the `/home/[yourusername]` directory. If not, navigate to this directory using `cd /home/[yourusername]`. If you don't know your username, run the command `whoami` and it will tell you.

8. Run the command `git clone https://github.com/PrairieLearn/pl-virginia-cs2100.git`. Enter your GitHub username when prompted. For your password, paste the token you created earlier. This clones the repository into a new directory `pl-virginia-cs2100`.

9. After cloning the repository, we need to create another folder on the same level as `pl-virginia-cs2100`. Ensure your terminal is still located at `/home/[yourusername]` and run the command `mkdir pl-jobs`. This directory will be used to store autograder jobs. Still create this folder even if you aren't planning to write questions using an autograder.

10. Run the command `docker run -it --rm -p 3000:3000 -v "$HOME/pl-virginia-cs2100:/course" -v "$HOME/pl-jobs:/jobs" -e HOST_JOBS_DIR="$HOME/pl-jobs" -v //var/run/docker.sock:/var/run/docker.sock --add-host=host.docker.internal:172.17.0.1 prairielearn/prairielearn` (it may take longer the first time).

11. Open your browser and go to [http://localhost:3000/](http://localhost:3000/). You should now see PrairieLearn running locally!

12. Click "Load from disk" on the top right. After it is done, click "Back to previous page". You should now see CS 2100 as a course with instructor access. When you click on it, it takes you to the course homepage. From here, you'll probably be using the "Questions" tab the most.

**Important:** When you are finished with your locally running PrairieLearn instance, it is important to shut it down. To do this, go back into your terminal where you launched PrairieLearn and press Ctrl+C. To launch PrairieLearn again, paste the same long command from step 10 into an Ubuntu terminal and go to [http://localhost:3000/](http://localhost:3000/).