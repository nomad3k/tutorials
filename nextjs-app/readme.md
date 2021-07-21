```
git flow init -d
curl https://raw.githubusercontent.com/fjsj/gitignore/master/Node.gitignore > .gitignore
git add .gitignore
git commit -m "Added .gitignore"
npx lerna init
mkdir services/app
cd services/app
npx create-next-app . --ts
