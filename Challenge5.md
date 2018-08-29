# Challenge 5 - Service Record Messaging Extension

## Background

Games tend to get very competitive; winners like to brag about winning and losers want to beat the winners. No game would be complete without a way to search and share your "service record" with your friends. The service record is essentially your global gameplay statistics. The three outcomes in "rock", "paper", "scissors" are win, tie, and loss so the service record should contain these three totals.

Messaging Extensions are a great way to share data between users.

## Challenge

Add a messaging extension to your bot. This messaging extension must allow users to share their service records with their friends in the chat. This must be a global tally that can be updated and maintained whenever a match has been completed (all users have chosen).

Users may also want to share their team member's service records. Your messaging extension should return a card for every user in the current chat.

## Success Criteria

- Your app must provide a messaging extension that queries the users of the current chat by name and returns their service records.

## Important Notes

- If your app is not installed in a team and you try to query the roster for that team, you will get an UnauthorizedAccessException. This is expected and you should catch and handle this exception. You still get a reference to the current user and should be able to return the one record for the current user.

## Hints

- You have probably used the BotBuilder storage to store the wins and losses from the previous challenges. It is probably not a good idea to store the global service record in the BotBuilder storage since you want it to span conversations and be easily queriable by user Id. Feel free to create your own in-memory storage that stores and updates the service records. It can look something like this (notice the static dictionary):
```csharp
public class InMemoryServiceRecordStorage
{
    private static Dictionary<string, ServiceRecord> ServiceRecords = new Dictionary<string, ServiceRecord> { };

    public ServiceRecord GetServiceRecordForUserId(string userId)
    {
        if (userId == null)
        {
            throw new ArgumentNullException(nameof(userId));
        }

        ServiceRecords.TryGetValue(userId, out ServiceRecord value);
        return value;
    }

    public void SetServiceRecordForUserId(string userId, ServiceRecord record)
    {
        if (userId == null)
        {
            throw new ArgumentNullException(nameof(userId));
        }
        if (record == null)
        {
            throw new ArgumentNullException(nameof(record));
        }
        ServiceRecords.Add(userId, record);
    }
}
```

## References

- [Messaging Extensions documentation](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/messaging-extensions)