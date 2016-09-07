# Embedding

You can embed polis on your site or in your app the way you would a YouTube video or a comment system. The process is simple: add a script tag which loads an `<iframe/>` asynchronously.

There are two options: manually creating embedded conversations or having Polis create them automatically in your templates.

#### Creating each conversation manually:

1. In the [inbox](https://pol.is/inbox), click [+new](https://pol.is/conversation/create)
2. Give your conversation a topic and description (*default none*)
3. Decide what flavor of [moderation](./CommentModeration.md) you'd like, lazy or strict (*default lazy*)
4. Click create
5. Copy out the script tag
6. Paste it into the HTML of your site where you'd like the `<iframe/>` to appear.

#### Creating conversations automatically:

Copy and paste this into a template (blog posts, news articles, etc).

```
<div
  class="polis"
  data-page_id="PAGE_ID"
  data-site_id="polis_site_id">
</div>
<script async="true" src="https://pol.is/embed.js"></script>
```

When this embed code loads, it will either create a new conversation (if one doesn't already exist) or load an existing conversation.
Your job is to replace `PAGE_ID` in your template.
`PAGE_ID` is the lookup Polis uses to keep track of what conversations belongs on what page.

