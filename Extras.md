# Extras

## Background

Unfortunately, we didn't get to cover everything there is in Microsoft Teams. This final page should serve as a reference for how you can learn more about the remaining topics.

## Configurable Tabs

- [Develop tabs for Microsoft Teams](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/tabs/tabs-overview)

- [Configuration pages](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/tabs/tabs-configuration)

- [Content pages](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/tabs/tabs-content)


## Localization

While you cannot currently localize your application's manifest, your tabs and bots can respond in the user's set locale.

For a bot you just have to set the locale right for the activity like this [reference](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/controllers/MessagesController.cs#L40). The locale is based on the team configuration.

Tabs have access to the locale from the [context](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/tabs/tabs-context).

## Authentication

Authentication is a huge topic on its own and not something we can focus on in this learning session. [Here](https://techcommunity.microsoft.com/t5/Microsoft-Teams-Blog/Authentication-SSO-and-Microsoft-Graph-in-Microsoft-Teams-Tabs/ba-p/125366) is a good blog post on Authentication with AAD and requesting graph permissions.

[This documentation](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/authentication/authentication) has a full write-up of authentication in teams. Including links to more references and documentation.

## Connectors

These are quickly falling out of style in favor of Bots. Bots are much more flexible and most apps can benefit from having a bot rather than a connector.

The documentation for connectors is [here](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/connectors/connectors).

## App Distribution

Apps can be distributed in 3 different ways. The one we used in these challenges is called sideloading.

Users can also deploy their apps via:
1. [Public store submission](https://docs.microsoft.com/en-us/microsoftteams/platform/publishing/apps-publish)
2. [Tenant-wide (LOB) distribution](https://docs.microsoft.com/en-us/microsoftteams/tenant-apps-catalog-teams)

Sideloading should be mainly used for development purposes.