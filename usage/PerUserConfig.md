The data-ucw (user can write) tag toggles writing, and is only relevant for that user for that session.

The data-ucv (user can vote) tag toggles voting, and is only relevant for that user for that session.

The data-show_vis causes the vis to be enabled or disabled when the conversation initializes. This is a one-time setting which is picked up and stored in our db the first time someone loads this script. If you later change this value, it won't have any effect. To change that value, you can load the config tab of the admin page for that conversation (the button for the conversation's admin page should appear in preprod.pol.is/inbox )

```
<div
   class="polis"
   data-page_id="your_pageid_1234"
   data-site_id="polis_site_id_your_site_id_goes_here"
   data-ucv="true"
   data-ucw="false"
   data-show_vis="true"
>
</div>
<script async="true" src="https://preprod.pol.is/embed.js"></script>
```

Also, I added code to emit a "vote" event each time a participant votes.
You can subscribe to that like this:

```
 window.addEventListener("message", function(event) {
      var data = event.data||{};
      if (!event.origin.match(/pol.is$/)) {
        return;
      }
      if (data.name === "vote") {
        alert("vote!");
      }
    });
```