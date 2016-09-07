# User Authorization

There are many different authorization scenarios you may encounter when using polis.

Sometimes it doesn't matter if you know who is who.
Sometimes you want to make sure people aren't voting again and again to game the system.
Sometimes you'll want total transparency.
Maybe you already know who your users are.
Maybe you even have your own authorization system.

Polis handles all these cases. Here's how.

#### Optional social login

*default*

By default, participants can write and vote anonymously, but are prompted to sign in using Facbeook and Twitter.
This is low friction for users and encourages voting and writing.

#### Social login required to write

`pol.is/m/55555 >> Config >> User login required to write >> ON`

#### Social login required to vote

`pol.is/m/55555 >> Config >> User login required to vote >> ON`

#### Social login prompts disabled

In this scenario, users who have already validated a social profile will still be shown.
No users will be prompted to connect their social profile

`pol.is/m/55555 >> Config >> User shown social login >> OFF`

#### Completely Anonymous

In this scenario, even users who have already validated a social profile will not be shown.
The visualization is hidden.

`pol.is/m/55555 >> Config >> Total Anonymity for All Users >> ON`

#### Anonymous but verified via social account login

In this scenario, all users are prompted to connect social before voting and / or writing, but the visualization is hidden and no user identities are passed on to you as the owner.
This scenario is ideal if you need to ensure that users are not gaming the system, and possibly collect metadata from the accounts like a restricted geolocation, but ensure that identities remain secret.

`pol.is/m/55555 >> Config >> Anonymous but verified with social account >> ON`

#### Proprietary auth

This scenario is only available if the Polis conversation is instantitaed through an embedded `<iframe/>` on your page.
You'll decide whether or not the user is verified.
You can then use the [per user config](./PerUserConfig.html) data attributes to customize the experience at will.
A nice pattern is to shut off writing and voting for those not logged in, so that users who are not logged in can still consume a read-only version of the conversation by clicking through the visualization.

`data-user-image-url=""`

#### Creating custom URLs for each participant to join

This feature is coming soon.

Let's say you are a business intelligence analyst, and a hospital has hired you to run a survey of its doctors and nurses. Conveniently for the purposes of our example, they've asked you to use Polis.

In this scenario, the hospital has an employee database. They would like to correlate employment data - columns like role, length of employment, age, gender, etc. - with groups that emerge in Polis. You are going to send out pol.is links because the hospital will not be embedding the conversation on its site and has no template and authorization system, but it's not appropriate to have doctors and nurses connect Twitter and Facebook.

In this case, you'll want to create a URL per participant, with a key that you can use to map them back to the data you already have about them. When we make this feature public, we'll fill the rest of this in!
