# semantic-release-net-poc

## Install commitlint

Install `commitlint` and a `commitlint-config-*` of your choice as devDependency and
configure `commitlint` to use it.

```bash
# For Windows:
npm install --save-dev @commitlint/config-conventional @commitlint/cli

# Configure commitlint to use conventional config
# File .commitlintrc
{
  "extends": [
    "@commitlint/config-conventional"
  ]
}
```

## Install husky

Install `husky` as devDependency, a handy git hook helper available on npm.

```sh
# Install Husky v6
npm install husky --save-dev

# Active hooks
npx husky install

# We can add a prepare step which enables the husky hooks upon installation
npm set-script prepare "husky install"

# Add hook
npx husky add .husky/commit-msg 'npx --no -- commitlint --edit $1'
```

## Test

### Test simple usage

For a first simple usage test of commitlint you can do the following:

```bash
npx commitlint --from HEAD~1 --to HEAD --verbose
```

### Test the hook

You can test the hook by simply committing. You should see something like this if everything works.

```bash
git commit -m "foo: this will fail"
husky > commit-msg (node v10.1.0)
No staged files match any of provided globs.
⧗   input: foo: this will fail
✖   type must be one of [build, chore, ci, docs, feat, fix, perf, refactor, revert, style, test] [type-enum]

✖   found 1 problems, 0 warnings
ⓘ   Get help: https://github.com/conventional-changelog/commitlint/#what-is-commitlint

husky > commit-msg hook failed (add --no-verify to bypass)
```

Since [v8.0.0](https://github.com/conventional-changelog/commitlint/releases/tag/v8.0.0) `commitlint` won't output anything if there is not problem with your commit.\
(You can use the `--verbose` flag to get positive output)

```bash
git commit -m "chore: lint on commitmsg"
husky > pre-commit (node v10.1.0)
No staged files match any of provided globs.
husky > commit-msg (node v10.1.0)
```