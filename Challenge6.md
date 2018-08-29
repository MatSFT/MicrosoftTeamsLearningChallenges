# Challenge 6 - My Service Record Tab

## Background

We've touched before on the topic of personal and team scoped apps. The app we built so far spans team and personal experiences to provide a fun game. We used a personal chat (via proactive messages) to request a user's game choice in private, while aggregating the results in the team context. This is where the true power of Teams comes to life. Bridging collaborative and personal experiences to provide a cohesive workspace.

Let's build on this notion a bit more and add a proper personal experience in the form of a static tab. Static tabs got their name from the fact that there should be nothing to configure for them. Each user gets the same set of static tabs, and these tabs can gain enough context to provide a tailored experience.

## Challenge

Add a static tab to your app. This tab should display the user's service record. Since the record has very little data, lets also add some more. When a match is finished, add the match to a list of completed matches for the user in their service record. This will give us a complete history of every match the user has played in as well as their outcome.

Since this is not an exersize in website development, feel free to use any technologies you are familiar with. The tab does not have to look pretty.

## Success Criteria

- Your team must build a static tab that displays the user's service record with history.

## Important Notes

- You can grab the context for the tab using the Teams JavaScript tab SDK. This will give you the user's details to pull the right data.

- **MOST IMPORTANT NOTE** In this challenge we are not considering any sort of authentication. This means that if a malicious user loads the tab and passes the context of a different user the tab will happily return this data. Please only treat this as a starter to static tabs. To be truly secure a static tab must somehow authenticate the user (using AAD or other authentication provider) before returning their data.

## Hints

- It will probably be easiest to host the tab from within the existing bot project since you can get direct access to the data.

- Tabs will not get the same id as we have been using so far in the bot. You will need to update your service record to also store the AAD object Id. There is a handy function called AsTeamsChannelAccount() that is implemented on top of the ChannelAccount object that will give you this extra data.

## References

- [Develop tabs for Microsoft Teams](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/tabs/tabs-overview)

- [Developing Static Tabs in Microsoft Teams](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/tabs/tabs-static)

- [Get context for your Microsoft Teams tab](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/tabs/tabs-context)

- [Authenticate a user in your Microsoft Teams tab](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/authentication)