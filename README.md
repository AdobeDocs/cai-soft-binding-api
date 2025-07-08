## General instructions

This repo was created from the template <https://github.com/AdobeDocs/dev-docs-template>.

EDS is similar to Gatsby with some caveats; see [wiki](https://wiki.corp.adobe.com/x/rYfvxg#DeveloperWebsite--63309052) (Best Practices for Migration).


To test the site:

1. Create a branch called `stage`.
1. Test that branch by deploying to stage: Go to **Actions > Deployment > Run workflow** and select stage branch and env.
1. Wiew at <https://developer-stage.adobe.com/cai-soft-binding-api>.
1. If stage looks good merge to `main`.
1. Deploy `main` to prod.

## Git config

```
git config core.ignorecase false
```

## How to set navigation

Create a directory hierarchy in `src/pages/config.md`.

## Local development

This is not possible at the moment (we're still working on it)

## Launching a deploy

Go to **Actions > Deployment > Run workflow**.

## URL

- Stage: <developer-stage.adobe.com/cai-soft-binding-api>
- Prod: <developer.adobe.com/cai-soft-binding-api>

## Where to ask for help

The slack channel #adobe-developer-website is our main point of contact for help. Feel free to join the channel and ask any questions.
