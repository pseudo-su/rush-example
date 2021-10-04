# Setup steps

## Repo setup

```sh
# Create folder
mkdir rush-example
cd rush-example
git init

# Set .nvmrc
echo "14.18.0" > .nvmrc
nvm install;
nvm use;

# Install rush globally
npm install -g @microsoft/rush
```

## Rush setup

https://rushjs.io/pages/maintainer/setup_new_repo/

```sh
rush init
rm .travis.yml
git add .
git commit -m "Initial commit"
```
