# Monorepo Commands

Some convenience scripts can be run in any folder of this repo and will call their counterparts defined in packages and apps.

| Name                         | Description                                                                                                                          |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `yarn g:changeset`           | Add a changeset                                                                                                                      |
| `yarn g:typecheck`           | Run typechecks in all apps & packages                                                                                                |
| `yarn g:lint`                | Display linter issues in all apps & packages                                                                                         |
| `yarn g:lint --fix`          | Attempt to run linter auto-fix in all apps & packages                                                                                |
| `yarn g:lint-styles`         | Display css stylelint issues in all apps & packages                                                                                  |
| `yarn g:lint-styles --fix`   | Attempt to run stylelint auto-fix issues in all apps & packages                                                                      |
| `yarn g:test`                | Run tests in all apps & packages                                                                                                     |
| `yarn g:test-unit`           | Run unit tests in all apps & packages                                                                                                |
| `yarn g:test-e2e`            | Run unit tests in all apps & packages                                                                                                |
| `yarn g:build`               | Clean every caches and dist folders in all apps & packages                                                                           |
| `yarn g:clean`               | Add a changeset                                                                                                                      |
| `yarn g:check-dist`          | Ensure build dist files passes es2017 (run `g:build` first).                                                                         |
| `yarn deps:check --dep dev`  | Will print what packages can be upgraded globally (see also [.ncurc.yml](https://github.com/sortlist/packages/blob/main/.ncurc.yml)) |
| `yarn deps:update --dep dev` | Apply possible updates (run `yarn install && yarn dedupe` after)                                                                     |
| `yarn check:install`         | Verify if there's no dependency missing in packages                                                                                  |
| `yarn install:playwright`    | Install playwright for e2e                                                                                                           |
| `yarn dedupe`                | Built-in yarn deduplication of the lock file                                                                                         |

PS:

> * Convention: whatever the script name (ie: test:unit), keeps it consistent over root commands, packages and apps.
> * The use of [yarn workspaces commands](https://yarnpkg.com/features/workspaces) can be replicated in pnpm, nmp7+lerna...

#### Maintaining deps updated

The global commands `yarn deps:check` and `yarn deps:update` will help to maintain the same versions across the entire monorepo. They are based on the excellent [npm-check-updates](https://github.com/raineorshine/npm-check-updates) (see [options](https://github.com/raineorshine/npm-check-updates#options), i.e: `yarn check:deps -t minor`).

> After running `yarn deps:update`, a `yarn install` is required. To prevent having duplicates in the yarn.lock, you can run `yarn dedupe --check` and `yarn dedupe` to apply deduplication. The duplicate check is enforced in the example github actions.
