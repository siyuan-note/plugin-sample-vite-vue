# SiYuan Plugin Template - Vite & Vue3

[简体中文](./README.zh-CN.md)

> Consistent with [siyuan/plugin-sample](https://github.com/siyuan-note/plugin-sample).

1. Use Vite for packaging
2. Use Vue3 for development
3. Provides a github action template to automatically generate package.zip and upload to new release
4. Provides a script to auto create tag and release. [link](#release-script)

> [!NOTE]
>
> Before your start, you need install [NodeJS](https://nodejs.org/en/download) and [pnpm](https://pnpm.io/installation) first.

> [!WARNING]
>
> For your first attempt, please do not modify anything. Load the plugin template in Siyuan as described below before making any changes.
>
> For example, when renaming README.zh-CN.md, update the `readme` field in `plugin.json` and the documentation links to match.

## Get started

1. Use the `Use this template` button to make a copy of this repo as a template
> [!WARNING]
>
> That the repository name should match the plugin name, and the default branch must be `main`.


2. Use `git clone` to clone the copied repo to your computer.
3. Use `pnpm i` to install the dependencies.

4. Copy the `.env.example` file as `.env`, set the `VITE_SIYUAN_WORKSPACE_PATH` to your SiYuan workspace.


> [!TIP]
>
> If you prefer not to package the project directly into the workspace, you can use a `symbolic link` instead.
>
> Writing directly into the Siyuan workspace allows you to sync via Siyuan's sync feature to other devices, while using a symbolic link will not be included in the sync.
>
> This template does not provide specific details about symbolic links. For related information, please refer to [plugin-sample-vite-svelte](https://github.com/siyuan-note/plugin-sample-vite-svelte).

5. Use `pnpm dev` to run the project, you will see info like below

  ```

  > plugin-sample-vite-vue@0.0.1 dev /path/to/your/plugin-sample-vite-vue
  > vite build --watch

  mode=> production
  env=> {
    VITE_SIYUAN_WORKSPACE_PATH: '/path/to/siyuan/workspace',
    VITE_DEV_DIST_DIR: ''
  }

  Siyuan workspace path is set:
  /path/to/siyuan/workspace

  Plugin will build to:
  # ✅ the plugin will build into here
  /path/to/siyuan/workspace/data/plugins/plugin-sample-vite-vue

  isWatch=> true
  distDir=> /path/to/siyuan/workspace/data/plugins/plugin-sample-vite-vue
  vite v6.3.5 building for production...

  watching for file changes...

  build started...
  ✓ 26 modules transformed.
  rendering chunks (1)...LiveReload enabled
  ../../Siyuan-plugin/data/plugins/plugin-sample-vite-vue/index.css    1.08 kB │ gzip:  0.41 kB
  ../../Siyuan-plugin/data/plugins/plugin-sample-vite-vue/index.js   198.60 kB │ gzip: 46.59 kB
  [vite-plugin-static-copy] Copied 7 items.
  built in 502ms.
  ```


   If successed, restart your siyuan, and you will find the plugin in `Siyuan - Settings - Marketplace`, named as `plugin-sample-vite-vue`.
6. Enable the plugin, and check the `App.vue` file to start your development.
   
   This file contains some example codes.


> [!TIP]
>
> More plugin code examples, please check [siyuan/plugin-sample/src/index.ts](https://github.com/siyuan-note/plugin-sample/blob/main/src/index.ts)

## Marketplace package resources

The optional `icon` and `preview` fields in `plugin.json` declare image filenames at the package root. PNG, JPEG, WebP, and AVIF are supported; SVG is unsupported. Icons are limited to 64 KiB and previews to 512 KiB. To omit an image, remove its field and the legacy `icon.png` or `preview.png`; an empty field value is invalid.

Relative README images are loaded from `package.zip` when present; otherwise the online marketplace falls back to the matching GitHub Release. This template packages `asset/*` so its README images remain available offline. Labeled sponsorship links can be declared with `funding.links` entries containing `label` and `url`; `funding.custom` remains compatible.


## List on the Marketplace

### Use Github Action

1. You can create a new tag, use your new version number as the `Tag version` in your local.
2. Then push the tag to Github. The Github Action will create a new Release for you.

> [!TIP]
>
> <div id="release-script"></div>This template provided a script to auto create tag and release. You can use `pnpm release` to create a patch version.
>
> You can add `--mode=manual|patch|minor|major` arg to set release mode, or run with arg like `pnpm release:manual`. 
> 
> All the scripts please see the `package.json` file.

The github action is included in this sample, you can use it to publish your new realse to marketplace automatically:

1. In your repo setting page `https://github.com/OWNER/REPO/settings/actions`, down to Workflow Permissions and open the configuration like this:

![img](./asset/action.png)

2. Push a tag in the format `v*` and github will automatically create a new release with new bulit package.zip
3. The workflow publishes a regular Release because the marketplace reads GitHub's Latest Release and ignores pre-releases.

```yaml
- name: Release
    uses: ncipollo/release-action@v1
    with:
        allowUpdates: true
        artifactErrorsFailBuild: true
        artifacts: 'package.zip'
        token: ${{ secrets.GITHUB_TOKEN }}
        prerelease: false
```

### Manual

1. Use `pnpm build` to generate `package.zip`
2. Create a new Github release using your new version number as the "Tag version". See here for an example: https://github.com/siyuan-note/plugin-sample/releases
3. Upload the file package.zip as binary attachments
4. Publish the release

For the first release, fork the [community bazaar repository](https://github.com/siyuan-note/bazaar), add one `owner/repo` line to `plugins.txt` in its root, and open a PR against `main`. Use one repository per line without commas or empty lines, and add only one new package per PR. See [Submitting a bazaar package](https://github.com/siyuan-note/bazaar#submitting-a-bazaar-package) for the full process and review rules.

After the PR is merged, the bazaar updates its index automatically. For subsequent updates, increase `version` in the package manifest and publish a regular GitHub Release containing `package.zip`; no additional listing PR is needed. See [Updating a bazaar package](https://github.com/siyuan-note/bazaar#updating-a-bazaar-package) for update timing and troubleshooting, and check deployment status in the [Stage workflow](https://github.com/siyuan-note/bazaar/actions/workflows/stage.yml).


---

More other plugin info, please check in [siyuan/plugin-sample](https://github.com/siyuan-note/plugin-sample).
