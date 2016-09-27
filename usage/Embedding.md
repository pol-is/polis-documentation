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


#### Optional fields:
These config variables will be used to init the conversation.
Subsequent loads will not update to these values in our DB.
To change the values after the conversation is created, go to the config tab of ```https://pol.is/m/<conversation_id>```
```

  data-topic="The End of American Football?"
  
  data-auth_needed_to_vote="false" // default false
  
  data-auth_needed_to_write="true" // default true
  
  // Prompt users to auth using Facebook.
  data-auth_opt_fb="true" // default true
  
  // Prompt users to auth using Twitter.
  data-auth_opt_tw="true" // default true
  
  // This is here in case we add other auth providers (Google, etc), you can preemptively disable them by setting this to false.
  // Example: if auth_opt_fb is true, but auth_opt_allow_3rdparty is false, users will not be prompted to auth using Facebook.
  data-auth_opt_allow_3rdparty="true" // default true
  
```
Additional config variables can be set here: [https://docs.pol.is/usage/PerUserConfig.html](https://docs.pol.is/usage/PerUserConfig.html)
