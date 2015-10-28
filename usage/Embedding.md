Using polis on your site is as easy as dropping in a script tag. The biggest consideration is whether you want to use polis in a template system like Wordpress across your entire site, in which polis creates the conversations automatically based on the URL of the page they are embedded on, or drop it in here and there and create each conversation manually.

Creating each conversation manually:

If you're going to create each conversation manually, click +new from the inbox and add your topic and description. Then grab the script tag and put it wherever you like on your site.

Creating conversations automatically:

Copy and paste this into the template for your pages (blog posts, news articles, etc)

When this embed code loads on your website, it will either create a new conversation (if one doesn't already exist) or load an existing conversation. It keeps track of what conversations belongs on what pages via the data-page_id HTML attribute. Simply replace "PAGE_ID", either manually or in your templates, to create new conversations and load existing ones in the right place.

```
<div
  class="polis"
  data-page_id="PAGE_ID"
  data-site_id="polis_site_id">
</div>
<script async="true" src="https://pol.is/embed.js"></script>
```
