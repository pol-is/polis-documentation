
# Data Export API

All of the options available for data export via the UI is also available via our HTTPS API.

For most exports, only a single endpoint is required.
This endpoint is structured like so:

```
https://pol.is/api/v3/dataExport?conversation_id=<your-conversation_id>
```

If your conversation has the URL `https://pol.is/7xyzqp`, `<your-conversation_id>` would be `7xyzqp`.

Additional available query parameters:

| Param | Example | Description
| ----- | ------- | -----------
| `format` | GET `https://pol.is/api/v3/dataExport?conversation_id=7xyzqp&format=csv` | Exports data in separate CSV files, gathered in a `.zip` archive. Alternate option `excel` produces an Excel file as a response.
| `email` | GET `https://pol.is/api/v3/dataExport?conversation_id=7xyzqp&email=abc@foo.com` | Exports the data and send an email notification to the given email when complete.
| `at-date` | GET `https://pol.is/api/v3/dataExport?conversation_id=7xyzqp&at-date=23434333` | Exports the data recomputed at time 23434333, as a number of ms since epoch. *

[\*] Note this computation isn't necessarily exactly what was seen at that point in the pol.is conversations.
Due to the nature of the analyses used, it is difficult to recompute the conversation "exactly" as it was at a given point in time.
It's possible that this could be amended in the future, so get in touch with us if this feature would be important to you.


## For long running requests

For large conversations, especially when passing the `at-date` parameter where lots has to be recomputed, the export can take much longer to create than would be good for a normal request handler.
If an export takes longer than [XXX insert] seconds, instead of returning a 200 response, we return a 202.

The 202 response (see [http spec](http://www.w3.org/Protocols/rfc2616/rfc2616.txt)) indicates that the request has been received and is being handled, but cannot respond now.
In the `Location` header of this response will be a URL pointing to a status link.
This status link should look like:

```
https://pol.is/api/v3/dataExport/status?conversation_id=7xyzqp&filename=<somelongfilename>
```

When a GET request is made to the status URL, it will return 200 if the data is not ready yet, and 201 when it is ready.
In the case of a 201, the `Location` header will contain a download URL, keyed similarly to the status URL, but with a different path:

```
https://pol.is/api/v3/dataExport/results?conversation_id=7xyzqp&filename=<somelongfilename>
```

This link will return a response with the export file as body.


## Lifecycle recommendation

We recommend that your request cycle look something like this:

* Request `export/get`
* Check status:
  * If 200: do stuff with your data
  * If 202:
    * Every N seconds check `export/status` (increment N to reduce request overhead):
      * When status is 200: pass
      * When status is 201: fetch data at the Location URL

Long running exports should take under a day to recompute, even for very large conversations.
If for whatever reason, you're finding results that take longer, please get in touch with us.


## Authentication

[@mike: Insert stuff on auth... Simple auth?]


