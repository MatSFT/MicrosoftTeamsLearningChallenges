# Challenge 3 - Sending Proactive Messages

## Approximate time: 45 minutes

## Background

The rock-paper-scissors game will work by pitting every team member against each other and then calculating the total # of wins + losses for each person. Each session will start from within the Team by any user messaging the bot "Begin match!". The bot will then message each user in the team individually to ask for their choice, "rock", "paper", or "scissors".

In Challenge 3, you will implement a basic proactive message that will be sent to every member of the team except yourself (you will remove this constraint in a future challenge).

## Challenge

Take a deep-dive through the code that you got running in the previous challenge. A bot in Bot Framework is nothing but a web server that accepts an event via HTTP POST to an endpoint and performs some action. The code is built using ASP.NET WebApi 2.2 and the entry point for your bot is in the MessagesController. Once you have a good understanding of how the data is flowing through your code, proceed with the challenge.

Upon receiving the message "greet everyone" from a user in the team, the bot must send a proactive message to each user (except the sender) with the text "Greetings! (I have greeted you # times)" where # is the number of times the bot has sent this user a greetings message.

## Success Criteria

- Your bot accepts the message "greet everyone" ONLY within the team (not personally).

- Your bot messages every team member except the sender with the greetings message.

- Your bot keeps track of how many times it has greeted each user and sends that number upon each greetings message.

## Important Notes

Sending a proactive message isn't quite as easy as it sounds. Not sure where to start? Try talking to the helpful bot found within App Studio.

This is also a very good moment to introduce our [fantastic template sample app found here](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp). This app has implemented pretty much everything that you can do in teams and is fairly well organized. We often refer to it during partner meetings to get down to the details of how to implement something.

## Hints

- The BotBuilder SDK that we are using has a notion of conversation state that you can utilize to store how many greetings have been sent.

## References

- [Handle bot events in Microsoft Teams](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/bots/bots-notifications#team-member-or-bot-addition)

- [Get context and the roster for your Microsoft Teams bot](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/bots/bots-context)

- [Dialogs in .NET BotBuilder](https://docs.microsoft.com/en-us/bot-framework/dotnet/bot-builder-dotnet-dialogs)

- [Conversation data storage in .NET BotBuilder](https://docs.microsoft.com/en-us/azure/bot-service/dotnet/bot-builder-dotnet-state?view=azure-bot-service-3.0)

- [Local debugging a bot in Microsoft Teams with ngrok](https://docs.microsoft.com/en-us/microsoftteams/platform/resources/general/debug#locally-hosted)

- [Quickly develop apps with App Studio for Microsoft Teams](https://docs.microsoft.com/en-us/microsoftteams/platform/get-started/get-started-app-studio)

- [Bot Framework quickstart for .NET](https://docs.microsoft.com/en-us/bot-framework/dotnet/bot-builder-dotnet-quickstart)

- [Bot Framework - Design and control conversation flow (Dialogs)](https://docs.microsoft.com/en-us/bot-framework/bot-service-design-conversation-flow)
