# 1 Installing Git for Linux
Download and install Git for Linux:
```
sudo apt-get install git
```
The above command is for Ubuntu and works on all Recent Ubuntu versions, tested from Ubuntu 16.04 to Ubuntu 18.04 LTS (Bionic Beaver) and it's likely to work the same way on future versions.

# 2 Configuring GitHub
Once the installation has successfully completed, the next thing to do is to set up the configuration details of the GitHub user. To do this use the following two commands by replacing "user_name" with your GitHub username and replacing "email_id" with your email-id you used to create your GitHub account.
```
git config --global user.name "user_name"
git config --global user.email "email_id"
```
# 3 create a new repository on the command line
echo "# Mytest" >> README.md
```
git init
```
or
```
git init folder
```
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/gitasep/Mytest.git
git push -u origin main

# 4 Push an existing repository from the command line
git remote add origin https://github.com/gitasep/Mytest.git
git branch -M main
git push -u origin main
