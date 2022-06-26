---
title: TheActionDev - v3
published: false
description: v3 Release notes for 'TheActionDev' GitHub Action
series: TheActionDev
tags:
  - showdev
  - beginners
  - productivity
  - githubactions
cover_image: https://imgur.com/SqplOeR.png
canonical_url: https://github.com/ful1e5/dev.to/blob/main/docs/TheActionDev/v3-Notes.md
---

<!-- Tweet -->

{% twitter 1539205426902106112 %}

## What's TheActionDev?

**TheActionDev** is Github Action that allows you to write & upsert [dev.to] **articles** without touching the `dev.to` UI. This action is initiated in **[ActionsHackathon]** and using **[forem API]**.

The main goal of TheActionDev is that we can write articles in favorite text editor, make articles collaborative like open source software and, to have version control system for article as software .

###### Check On GitHub Marketplace

https://github.com/marketplace/actions/theactiondev

### Migrating to v3

There is nothing new in v3 but minor changes have been made to the development workflow, Mainly releases tags and branches. Now release tags follow semantic versions with the `v` prefix. This release pattern allows us to point to a specific version tag and also helps us to merge commits into release branches from `main` without re-creating the already released version. You can view all changes of v3 in the project's [git history](https://github.com/ful1e5/TheActionDev/commits/main).

The main reason behind this release is **native YAML support** in front-matter thanks to [js-yaml] library. This means you have to assign the `tags` key as [yaml arrays] otherwise, Action will throw an error or ignore the assigned tags.

```diff
---
...
- tags: typescript, javascript, github
+ tags:
+   - typescript
+   - javascript
+   - github
...
---

...
```

Other than that, You will find the updated notice in the [README#Notice] section as we'll introduce any kind of breaking changes or deprecations.

## Getting Started

- [Setup](#setup)
- [Front-Matter](#front-matter)
- [Article Example](#article-example)
- [Track Sync](#track-sync)
- [Something Missing?](#something-missing?)

### Setup

1. You'll first need to create a YAML file to describe the workflow in your project (e.g. .github/workflows/TheActionDev.yml).
2. Generate dev.to `apiKey` by following [Forem API Docs]
3. Add your `apiKey` to GitHub Secret `DEVTO_API_KEY` by following [GitHub Docs]

#### TheActionDev.yml

```yaml
name: TheActionDev Sync
on:
  push:
    branches:
      - main # your default branch

jobs:
  operations:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v2

      - name: Sycing Article to dev.to
        uses: ful1e5/TheActionDev@v3
        with:
          api-key: ${{ secrets.DEVTO_API_KEY }} # Store your 'api-key' in Github Secret
          directory: ./articles # Your article directory
          ignore: Development.md, Production.md # Markdown file you wan't to ignore. Multple files separated by ,(comma)
```

### Front-Matter

Custom variables set for each post, located between the triple-dashed lines in your editor Here is a list of possibilities:

- **published:** boolean that determines whether or not your article is published
- **description:** description area in Twitter cards and open graph cards
- **tags:** max of four tags, needs to be comma-separated
- **canonical_url:** link for the canonical version of the content
- **cover_image:** cover image for post, accepts a URL. The best size is 1000 x 420.
- **series:** post series name.

#### Front Matter `default` value

| tag           | value   | required |
| :------------ | :------ | :------- |
| title         | `null`  | **yes**  |
| published     | `false` | **no**   |
| description   | `null`  | **no**   |
| tags          | `[]`    | **no**   |
| canonical_url | `null`  | **no**   |
| cover_image   | `null`  | **no**   |
| series        | `null`  | **no**   |

### Article Example

- Use [YAML](https://yaml.org/) to write and format article's [front-matter](#front-matter).
- Follow [dev.to editor guide](https://dev.to/p/editor_guide) for write and format article body.
- You can also use [Liquid tags](https://docs.dev.to/frontend/liquid-tags/) to add rich content such as Tweets,
  YouTube videos, etc.

```
---
title: Hello from TheActionDev
description: Hello World
published: false
tags:
  - showdev
  - github
series: foo
---

Just Setup **TheActionDev** for writing dev.to artcles.

{% github ful1e5/TheActionDev %}
```

### Track Sync

You're able track your article status in **Actions** tab.

![Action Tab](https://imgur.com/tNARvOg.png)

### Something Missing?

If something is missing in the documentation or if you found some part confusing, please file an issue on the repository with your suggestions for improvement, or tweet at the [@ful1e5] account. I love hearing from you!

**Support my work with $1 or more on [GitHub Sponsors](https://github.com/sponsors/ful1e5).**

{% github ful1e5/TheActionDev %}

<!-- Links -->

[readme#notice]: https://github.com/ful1e5/TheActionDev#notice
[dev.to]: https://dev.to/
[forem api]: https://developers.forem.com/api/
[js-yaml]: https://github.com/nodeca/js-yaml
[yaml arrays]: https://www.w3schools.io/file/yaml-arrays/
[actionshackathon]: https://dev.to/devteam/announcing-the-github-actions-hackathon-on-dev-3ljn
[forem api docs]: https://developers.forem.com/api/#section/Authentication/api_key
[github docs]: https://docs.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets
[@ful1e5]: https://twitter.com/ful1e5
