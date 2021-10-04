# Rush Example setup instructions

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

Read this https://rushjs.io/pages/maintainer/setup_new_repo/

```sh
rush init
rm .travis.yml
git add .
git commit -m "Initial commit"
```

Following the link above check the main config settings mentioned underneath "Step 3". Prefer keeping default settings unless there's a good reason to change it.

- Choose a package manager (recommended to keep pnpm)
- Check your Rush version (rushVersion)
- Check other version fields (pnpmVersion, npmVersion, yarnVersion, nodeSupportedVersionRange)
- Decide whether to use the “category folders” model.
- Configure your registry access (if using a private registry)

It is highly recommended to go through the `rush.json` file and read the comments for each config setting and decide if you want to keep the defaults or change them. Reading through the configuration can give a good idea of some of the complications 

For this we have choses the following settings

- `pnpmOptions.pnpmStore=local` (default) to avoid potential pnpm version conflicts across different projects.
- `pnpmOptions.strictPeerDependencies=true` to try and default to strict package resolution by default (If we run into issues later on this might need to be changed but hopefully not).
- `pnpmOptions.resolutionStrategy=fewer-dependencies` (default) to avoid potential incompatibilities mentioned.
- `pnpmOptions.preventManualShrinkwrapChanges=true` to prevent manual changes to the lock/shrinkwrap files.
- `nodeSupportedVersionRange=">=14.15.0 <15.0.0"` to make sure we're always using an up to dave version of NodeJS `14` (matches `.nvmrc` file).
- `suppressNodeLtsWarning=false` (default) to prefer only using LTS versions of NodeJS.
- `ensureConsistentVersions=true` to ensure consistent package versions.
- `projectFolderMinDepth=1` and `projectFolderMaxDepth=2` (default) good rule to guide project/package structure
- `allowMostlyStandardPackageNames=false` (default) good to keep this disabled unless absoloutely necessary to enable
- `approvedPackagesPolicy` set to simple config of having `production` and `tools` categories.
- `gitPolicy.allowedEmailRegExps` set to a regex matching the expected company email(s) eg `"[^@]+@digio\\.com\\.au"`
- `repository.url` create a remote repo and make this config match.
- `repository.defaultBranch=main` use the `main` branch as the default
- `repository.defaultRemote=origin` (default)
- `variants=[]` (default) leave empty as part of initial setup
- `telemetryEnabled=false`
- `hotfixChangeEnabled=false` (default)

When defining the `packages` in `rush.json` think of the folder structure/categories you want. An example folder structure might look like

```raw
tools/
  eslint/
    package.json
libs/
  example-library/
    package.json
services/
  example-website/
    package.json
```

After updating all the config make sure to run `rush update`.
