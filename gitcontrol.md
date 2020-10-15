…or create a new repository on the command line
echo "# gitsava" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/gitsava/gitsava.git
git push -u origin profil
                
…or push an existing repository from the command line
git remote add origin https://github.com/gitsava/gitsava.git
git branch -M main
git push -u origin profil
