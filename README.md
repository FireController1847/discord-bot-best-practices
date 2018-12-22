# Discord Bots Best Practices
*These guidelines are intended for public bots running on public guilds. If
your bot is restricted to private guilds, this document most likely does not
apply to you.*

*If you have an idea for an addition or change to this document, please make a
pull request and we can discuss it.*

#### 1. Commands should be explicitly invoked.
Bots should not be activated during a normal conversation. Instead, they should
use a command prefix and/or respond when the bot is directly mentioned.

#### 2. Use unique prefixes.
Single-character prefixes, such as `!`, `$`, and `.`, are commonplace for activating
commands and can overlap with other bots. Should you opt to use a prefix for your bot,
consider using words (`owl`) or use unique Unicode characters (`"`). Avoid using `#`,
`@`, or `:` as prefixes since they are used for Discord-specific actions like mentioning
a user. Ideally, a bot's prefix should be configurable on a guild-by-guild basis so that
a guild owner can ensure every bot has its own unique prefix.

#### 3. Do not be greedy.
Restrict yourself to a small number of prefixes, preferably one, to avoid the risk of
colliding with others.

#### 4. Do not overuse mentions.
Try your best to avoid mentioning the user when replying to a command. Doing this can
lead to bot reply loops. If a long-running command is executed, mentions are generally
acceptable; however, private messages are preferred in this case.

#### 5. Have an `info` command.
Info commands should provide information about the bot, such as what framework it is
using and its version. It should also include any `help` commands, and, most importantly,
who made it.

#### 6. Do not reply with an invalid command prompt.
If a user attempts to use a command that does not exist, do not reply with anything.
Let the command fail silently, and avoid things like "invalid command." If there is
more than one bot in a server that shares a prefix, this can result in very obnoxious
usage. Although, if the user ran a correct command but the arguments are wrong, then
it is okay to reply with "invalid argument(s)." If your bot's prefix is configurable,
this rule can be most likely be safely disregarded, however we still recommend following it.

#### 7. Be respectful of Discord's API.
Bots that abuse and misuse the Discord API ruin things for everyone. Consider adding
things like rate-limiting and backoff, and be intelligent about using the API. If you
are unsure about the correct way to implement things, ask for help.

#### 8. Ignore both your own and other bots' messages.
This helps prevent infinite self-loops and potential security exploits. Using a zero
width space such as `\u200B` and `\u180E` at the beginning of each message also prevents
your bot from triggering other bots' commands. The Discord API also tells you if a user
is a bot (`bot` property on `User` objects -
[see the reference](https://discordapp.com/developers/docs/resources/user#user-object)).

#### 9. Keep NSFW features in NSFW channels.
All NSFW commands or features should only work in Discord's NSFW-marked channels.
If these commands can be activated outside of these channels, it can cause your
bot to quickly be banned as that is against the Discord Terms of Service.

#### 10. Make usage clear to a new user.
Allow users to mention the bot as an alternative to using prefixes ("@MyBot help").
This will help users who are new to your bot get started. Make sure that, however,
places to ask for help can easily be found. One of the best ways to do this is using
a bot's presence. Mentioning is truly the most unique prefix of all.

#### 11. Escape mentions.
Whenever a bot responds to anything, ensure that it escapes mentions
(particularly `@everyone` and `@here`). While the user may not have permission to mention
`@everyone`, your bot might, which can result in "mention injection."

* **Note:** Some libraries do this automatically for you by default, but others will
require you to enable it or implement it by yourself. You can do this by inserting
a zero-width space (`\u200B`) after each `@`.
