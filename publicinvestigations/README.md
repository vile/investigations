# Investigation Posts

## Requirements

1. Hugo - [Install Hugo](https://gohugo.io/installation/)

## Creating Posts with Hugo

Create a new markdown post (where `post-title` is the title of your new post):

```bash
hugo new posts/post-title.md
```

## Generating Content

Generate static content:

```bash
hugo
```

## Examine Content Locally

```bash
hugo server
```

## Push Content to Github Pages

Navigate to `public/` and push new content to origin.

```bash
git add .
git commit -m "post: new post"
git push origin main
```
