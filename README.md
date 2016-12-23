# yarn-offline-cache-ssh

This repo is intended to showcase an issue in yarn 0.18.1, where installing a dependency using git+ssh will correctly add it to the offline yarn mirror cache,
but it will be saved in the `yarn.lock` file with a resolved from pointing to github instead of the mirror, and thus failing to use the offline mirror in installs.

When used in combination with a `yarn install --offline`, installs will fail because of this issue.

### Steps to reproduce

1. Create a package.json
2. Run `yarn add yarn add webpack@git+ssh://git@github.com/webpack/webpack.git#v2.2.0-rc.2` or any private git dependency
3. This will create a yarn.lock file and node_modules. To create the mirror with the correct refs: `rm -rf yarn.lock node_modules && yarn install --offline`
4  Now references of all npm packages point to the cache, but not the git+ssh one
