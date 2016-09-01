# Data Export

Data export allows you to maximize the value of your pol.is conversation data.
See [How to Use](./HowToUse.md) for some ideas about how you might want to use your data exports.

This chapter covers the data you can export, and the process of exporting data through our web interface.


## How to export your data

Data can be exported from the admin page for a conversation.

`pol.is/m/55555 >> Export`

There are a few options you can set when triggering an export.

### Format

The default format is "CSV".
When this is selected, you will download a zip archive with several CSV files containing different parts of the export.

The alternative is "Excel".
This will format your downloaded data as a single "XLSX" file, with multiple sheets corresponding to the different data available.

### Export Time

Leaving this unselected will export the most recent state of the conversation and votes data.
If you would alternatively like to export the state of a conversation at a specific point in time, you may select that time here.

Note: This export has to be recomputed, and due to the nature of the algorithms pol.is employs, guaranteeing results are exactly as seen at the given point in time is not currently possible.
However, the results should be pretty close.
If you need exact exports at various points in the conversation evolution, we recommend you periodically create updates based on the live data, either programmatically via [our API](./ExportAPI.md) or manually.

### Long running exports

For larger scale conversations, exports may take a long time to compute (particularly when Export Time is specified, as this requires a recompute of the conversation state).
When the export takes longer than several seconds, we will notify you that the export is processing but can not be returned immediately.
In this case, an email will be sent to the email address we have on file.


## What data do I get?

Four tables are produced by the export: Summary, Stats History, Participants Votes and Comments.
If Excel format is selected, there will be separate sheets representing each of these tables, named as above.
If CSV formatting is selected, the zip file will contain `summary.csv`, `stats-history.csv`,  `participants-votes.csv` and `comments.csv`.

Note that the data export schema is still considered to be in BETA, and may change in the future.
Once it has stabilized, we will issue an announcement.
In the mean time, if you would like to be notified ahead of changes, [follow us on Twitter](https://twitter.com/usepolis)

### Summary

This is a very high-level summary of the data about the conversation, including:

| Field                | Meaning 
| -------------------- | -------
| **Topic**            |  As specified during conversation creation.
| **URL**              | The url of the conversation.
| **Views**            | The number of unique visitors to the conversation. (Note: this won't necessarily be accurate if people view the conversation with multiple devices but don't log in. For more accurate assessment of this metric, we recommend using Google Analytics on your page).
| **Voters**           | Number of people who voted on at least one comment in the conversation.
| **Voters (in conv)** | Number of people who voted enough to be represented in the conversation view. [\*]
| **Commenters**       | Number of participants that wrote comments.
| **Groups**           | Number of groups in the conversation.
| **Conversation Description** |  As specified during conversation creation.

[\*] Only voters who vote on all the comments present at the time of voting, or at least 7 comments, whichever is less, are represented in the visualization.

This table has a separate row for each field.

### Stats History

This table is meant to give you more detailed information about the growth of the conversation over time.
The 5 columns in this table are:

| Column          | Meaning 
| --------------- | -------
| **Votes**       | Total number of votes in the conversation.
| **Comments**    | Number of comments in the conversation.
| **Visitors**    | Number of visitors to the conversation
| **Voters**      | Number of voters in the conversation [XXX is this (in conv) or not?]
| **Commenters**  | Number of participants that wrote comments.

Each row in this table corresponds to a change in one of these values due to an interaction with some participant (a vote, comment, or visit).
In the future, we may also include a timestamp indicating when that vote occurred.

### Participants Votes

This table provides information about individual participants' voting patterns and opinion group assignment.
Participants remain anonymous in this output, and are referred to by an integer ID unique within the conversation.

Each row of this table corresponds to a particular participant. 
The following columns are included:

| Column          | Meaning 
| --------------- | -------
| **Participant** | The participant identifier; an integer identifier unique within this conversation.
| **Group ID**    | Group ID of the group the participant belongs to.
| **Comments**    | Number of comments written by the participant.
| **Votes**       | Number of votes by the participant.
| **Aggrees**     | Number of agree votes by the participant.
| **Disggrees**   | Number of disagree votes by the participant.

Additionally, for every comment in the conversation, there is a column with that comment's ID as the column name.
For a given participant row and comment column, the entry in this table represents the vote that participant gave on that column.
A vote of 1 represents agree, a vote of -1 represents disagree, and a vote of 0 represents a pass.
If a participant did not vote or pass on the given comment, the corresponding entry is blank.

In the future, we may add a column indicating whether the participant was included as "In conversation" or not (as described above).

### Comments

This table provides summary data for each comment in the conversation.
Each row corresponds to a particular comment, with the following columns:

| Column           | Meaning 
| ---------------- | -------
| **Comment ID**   | The comment identifier; an integer identifier unique within this conversation.
| **Author**       | Participant ID of the comment's author.
| **Agrees**       | Number of agrees on the comment.
| **Disagrees**    | Number of disagrees on the comment.
| **Moderated**    | Moderation status; 1 for allowed, -1 for moderated out, 0 for unmoderated.
| **Comment Body** | The actual body of the comment.

Note that Comment ID and Author Participant ID correspond with the values in the Participants Votes table.


