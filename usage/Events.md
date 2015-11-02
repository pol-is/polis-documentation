# Events

The Polis embed code and `<iframe/>` are configured to emit a "vote" event each time a participant votes.
You can subscribe to those events on the page that instantiates the `<iframe/>` like this:

```
 window.addEventListener("message", function(event) {
  var data = event.data||{};
  if (!event.origin.match(/pol.is$/)) {
    return;
  }
  if (data.name === "vote") {
    alert("vote!");
  }
```
