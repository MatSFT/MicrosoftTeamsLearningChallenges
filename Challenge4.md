# Challenge 4 - Adaptive Cards and Message Updates

## Background

Finally in Challenge 4 we can start building the proper "rock", "paper", "scissors" app. Let's start by adding some results within our team and converting our current "Greetings! (I have greeted you # times)" message into a rich AdaptiveCard with buttons.

## Challenge

Add a new dialog or copy the greetings dialog and name it something similar to "GameMatchDialog". This dialog should be triggered when a user in the team says "begin match". Upon receiving "begin match" the bot should:
1. Respond to the team chat with an AdaptiveCard that lists all of the members of the team and whether they have responded or not. You must save a reference to this card and update it when a new response is entered. Once everyone has responded you may update this card with a final result card that displays winners and losers.
2. Send a proactive message to every user (including the sender) with a card that contains three buttons or a dropdown so that they may choose "rock", "paper", or "scissors". This card does not have to be Adaptive but you should be most familiar with these now.

Feel free to explore the various ways of displaying and sending data using AdaptiveCards. There is no "right" way to build your cards in this challenge.

## Success Criteria

- Your bot must process the command "begin match".

- Your bot must display an adaptive card in the team with all members of the team and whether they have responded to the match or not.

- Your bot must update the adaptive card in the team whenever someone responds to the match.

- Your bot must send a proactive message to each user to allow them to respond to the match with either "rock", "paper", or "scissors".

- When every user has responded to the match, the bot should update the team card with the results of the match.

- A user should only be able to respond to the match one time (you should update the message that the user clicks on to a thank you for playing message).

## Hints

- Adaptive card actions flow into teams as Message activities with a null text field but a populated value field.

- When a user says begin match, you will want to store some sort of match model for the conversation. You will also want to pass handles to this match model to all adaptive cards that you proactively send so that you can route their responses. A set of objects like this might be helpful:
```csharp
public class Match
{
    // Session Id is a randomly generated GUID per match. This might not be necessary if you just store the MessageId.
    public Guid SessionId { get; set; }

    // Array of results for the match.
    public MatchResult[] Results { get; set; }

    // The Id of the message that was created in the team chat. You will need this to be able to update the message later.
    public string MessageId { get; set; }
}

public class MatchResult
{
    // The user that this result belongs to.
    public ChannelAccount User { get; set; }
    // The choice that user made. Default this to None.
    public Choices Choice { get; set; }
}

public enum Choices
{
    None = 0,
    Rock = 1,
    Paper = 2,
    Scissors = 3
}

public static class ChoicesExtensions
{
    // A naive and helpful method to figure out if one choice beats another.
    public static bool Beats(this Choices choice, Choices other)
    {
        if (choice == Choices.None || other == Choices.None)
        {
            return false;
        } 

        return (choice == Choices.Paper && other == Choices.Rock) ||
              (choice == Choices.Rock && other == Choices.Scissors) ||
              (choice == Choices.Scissors && other == Choices.Paper);
    }
}
```

- If you choose to use the built-in BotBuilder storage, you can load a particular conversation's storage record from outside of the context of that conversation using code like this:
```csharp
using (var scope = DialogModule.BeginLifetimeScope(Conversation.Container, activity))
{
    // Use some DI to get the data store factory and built the address using the current activity and various parameters.
    var botDataStore = scope.Resolve<IBotDataStore<BotData>>();
    var address = new Address(activity.Recipient.Id, activity.ChannelId, activity.From.Id, activity.Conversation.Id, activity.ServiceUrl);

    // Loads that data storage
    var data = await botDataStore.LoadAsync(address, BotStoreType.BotConversationData, CancellationToken.None);

    // Gets a data record out of this storage
    var dataRecord = data.GetProperty<DataRecordType>(key);

    // Sets a data record inside of this storage
    data.SetProperty(key, dataRecord);

    // Saves and flushes the data storage
    await botDataStore.SaveAsync(address, BotStoreType.BotConversationData, data, CancellationToken.None);
    await botDataStore.FlushAsync(address, CancellationToken.None);
}
```

- It is sometimes helpful to organize your card responses into builders. Something like this is a good template.
```csharp
public class MatchCard
{
    // You will want to send the conversationId in the message so that you can load the data for the conversation later.
    private string conversationId;

    // This could be replaced with the messageId from the Match class in the hint above.
    private Guid sessionId;

    public MatchCard(string conversationId, Guid sessionId)
    {
        this.conversationId = conversationId;
        this.sessionId = sessionId;
    }

    // Cards are sent as Attachments so its helpful to generate the attachment this way. You can then always replace the implementation with any other type of card.
    public Attachment ToAttachment()
    {
        var card = new AdaptiveCard
        {
            Body = new List<AdaptiveElement>
            {
                new AdaptiveTextBlock
                {
                    Text = "Choose your action:"
                },
                new AdaptiveChoiceSetInput
                {
                    Id = "GameChoice",
                    Choices = new List<AdaptiveChoice>
                    {
                        new AdaptiveChoice
                        {
                            Title = "Rock",
                            Value = "Rock"
                        },
                        new AdaptiveChoice
                        {
                            Title = "Paper",
                            Value = "Paper"
                        },
                        new AdaptiveChoice
                        {
                            Title = "Scissors",
                            Value = "Scissors"
                        }
                    }
                }
            },
            Actions = new List<AdaptiveAction>
            {
                new AdaptiveSubmitAction
                {
                    Data = new Dictionary<string, object> { {"sessionId", sessionId.ToString() }, { "conversationId", conversationId } },
                    Title = "Submit"
                }
            }
            
        };

        return new Attachment
        {
            ContentType = AdaptiveCard.ContentType,
            Content = card
        };
    }
}
```

## Important Notes

Keep in mind this [fantastic template sample app found here](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp). Almost everything you need to do has already been implemented there.

## References

- [AdaptiveCard reference](http://adaptivecards.io/)

- [fantastic template sample app](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

- [Conversation data storage in .NET BotBuilder](https://docs.microsoft.com/en-us/azure/bot-service/dotnet/bot-builder-dotnet-state?view=azure-bot-service-3.0)