# [🚀 CI: Generate a SVG Websitecarbon Badge](https://gitlab.com/davidhund/svg-carbonbadge-ci/)

Your webpages have an impact on carbon emissions 🌳 😕 

You can measure this through [WebsiteCarbon.com](https://www.websitecarbon.com/). It provides a summary as a [badge](https://www.websitecarbon.com/badge/) to embed in e.g. your footer. 

The badge is a small JavaScript embed that populates an HTML element on your page.
There are a couple of ways to embed this JavaScript/HTML badge:

- The original [.wc-badge](https://www.websitecarbon.com/badge/) JS/HTML Embed
- A [svelte-carbonbadge](https://www.npmjs.com/package/svelte-carbonbadge) component
- A [vue-carbonbadge](https://www.npmjs.com/package/vue-carbonbadge) component
- A [react-carbonbadge](https://www.npmjs.com/package/react-carbonbadge) component

These JavaScript based embeds do have a performance impact of themselves 😕

> Would it not be neat to have an ✨SVG or image✨ and not have to rely on JavaScript at all?!

## With [svg-carbonbadge.netlify.app](https://svg-carbonbadge.netlify.app/)✨ you can!

The [Web App](https://svg-carbonbadge.netlify.app/) allows you to manually:

- Create a badge in `SVG`, `HTML` or `Text` (soon: PNG, WebP!)
- Customize it with your page's **accent-color**
- Download the image or render example `svg`, `html` or `img` markup

> One small image or SVG has less performance overhead, is more easily cached and can be shared easily on e.g. Social Media etc. 💯

## "But: are static images not outdated?!"

Glad you asked! Yes: we would not want to show outdated data. And manually re-generating the image can be a pain.

**With [svg-carbonbadge-ci](https://gitlab.com/davidhund/svg-carbonbadge-ci/) you dont have to!**

Using GitLab CI or GitHub Actions (WIP) you can *update your svg badge when your website is built*. You can also update the badge *periodically* with "Scheduled Pipeline Jobs"

The [.gitlab-ci.yml](https://gitlab.com/davidhund/svg-carbonbadge-ci/-/blob/master/.gitlab-ci.yml) and [.github/workflows](https://github.com/davidhund/svg-carbonbadge-ci/) in this repository give you examples of how to do this.

:sparkles: As a matter of eating ones own dog-food: the *example* `.gitlab-ci.yml` file in this repo does run periodically and update the badge for [this repo's GitLab Pages website](https://davidhund.gitlab.io/svg-carbonbadge-ci)! :sparkles: ([GitHub Pages](https://davidhund.github.io/svg-carbonbadge-ci/))

---
![svg-carbon-badge](https://gitlab.com/davidhund/svg-carbonbadge-ci/-/raw/main/website-carbon-badge.svg)
---

## 🤖 Automatically re-generate your badge

### GitLab CI

Your badge can be configured through **Environment Variables**. You can hard-code them in your `.gitlab-ci.yml`, but better is to pass them to CI jobs on-demand. Best is to configure them in the Pipeline settings. E.g. in GitLab CI Schedules at `/-/pipeline_schedules` 

| Variable name | Value | Default | Notes |
|--------------|-----------|------------|------------|
| `CI_PERSONAL_ACCESS_TOKEN`* | Your PAT | `undefined` | Make `masked` |
| `URL` | URL to create badge for | `svg-carbonbadge.netlify.app` | Does not need `http[s]://` |
| `COLOR` | Badge accent color | `669900` | Hexadecimal, 6-digit color **without `#`!** |
| `FILENAME` | Badge SVG file-name | `website-carbon-badge` | *May* contain sub-folder (`src/badge`) **without `.svg`!** |
| `COMMIT_MESSAGE` | CI commit message | `[carbonbadge ci] Updated Carbon Badge` | Timestamp is added! |

> All variables **except for** `CI_PERSONAL_ACCESS_TOKEN` are optional...

#### *`CI_PERSONAL_ACCESS_TOKEN`

Git cannot push to your own repository when running in a GitLab CI runner image. You need to set up a *Personal Access Token* at: [/-/profile/personal_access_tokens](https://gitlab.com/-/profile/personal_access_tokens)

- Give the token a descriptive `name` (e.g. `site-name-pat-ci`) and **Copy** its value
- **Paste** the value in your CI `CI_PERSONAL_ACCESS_TOKEN` variable and make it at least `masked`

### Run your jobs

When your Pipeline gets triggered (manual, through a Schedule or Merge request), CI should make an API call and commit the `$FILENAME.svg` to your project on the default branch.

For Jamstack sites, this push often rebuilds the website and e.g. deploys it to e.g. Netlify etc. The result is that your badge is updated automatically

### GitHub Actions

- Look at `.github/workflows/svg-carbonbadge-ci.yml` for an example of a GitHub Action workflow!
- Page at [davidhund.github.io/svg-carbonbadge-ci/](https://davidhund.github.io/svg-carbonbadge-ci/)
