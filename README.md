# WTelegramServer

WTelegramServer is a Telegram Server written in C#

You can now participate in testing the sample WTelegramServer instance  
→ Start with downloading archive [WTS_Testing.zip](https://tglink-as.azurewebsites.net/WTS_Testing.zip)  
Three methods are available:
1. The fast way (Windows):
   - Extract `Telegram_WTS.exe` from the archive into a new empty folder _(This is the official Telegram Desktop 6.3.1 for Windows, already patched using the methods below)_
   - Run `Telegram_WTS.exe` to start connecting to the WTelegramServer instance
   - Click "Start Messaging", then click SETTINGS in the upper-right corner
   - Disable checkboxes "Show tray icon" and "Update automatically" to prevent annoying behaviors
   - Close the Settings and click on "log in using your phone number"
   - Enter a random phone number (doesn't need to be real but at least 5 digits)
   - Enter 4 random digits code (if the phone number is not already taken), and voila!
2. Using the Patcher (Windows):
   - Extract the archive _(except Telegram_WTS.exe)_ into an empty directory. It contains a patcher project, binary and C# source, so you can check what it does
   - Place a copy of your Telegram Desktop `Telegram.exe` in the directory, and run the Patcher
   - When prompted for the IP address of the server instance, type: `34.73.170.46`
   - The Patcher should now create a Telegram_WTS.exe, copy of your Telegram.exe patched with the public key and IP address of the server instance, and disable auto-updates
   - Follow method 1 recommendations for running the program
   
   _Note: The patcher might work with other Telegram clients but was only tested with Telegram Desktop versions around 6.3.1.  
     WTelegramServer is only compatible with Telegram API layer 218, so it might not be compatible with other versions of Telegram Desktop_
3. Patching a client manually (sources or binary)
   - Identify where the official public encryption key of Telegram is located:
```
MIIBCgKCAQEA6LszBcC1LGzyr992NzE0ieY+BSaOW622Aa9Bd4ZHLl+TuFQ4lo4g
5nKaMBwK/BIb9xUfg0Q29/2mgIR6Zr9krM7HjuIcCzFvDtr+L0GQjae9H0pRB2OO
62cECs5HKhT5DZ98K33vmWiLowc621dQuwKWSQKjWf50XYFw42h21P2KXUGyp2y/
+aEyZ+uVgLLQbRA1dEjSDZ2iGRy12Mk5gpYc397aYp438fsJoHIgJ2lgMv5h7WY9
t6N/byY9Nw9p21Og3AoXSL2q/2IJ1WRUhebgAdGVMlV1fkuOQoEzR7EdpqtQD9Cs
5+bfo3Nhmcyvk5ftB0WkJ9z6bNZ7yxrP8wIDAQAB
```
   - Patch/Replace it with the public key for the sample WTelegramServer instance:
```
MIIBCgKCAQEAmu0N3BJAPxhRclG3NFkuC4qBkZiUVJF3bF2NPYegO7BKNGxGjvsM
UJYofrhSLwsK+2fbyKpHaZg9Dc7IolmOdNhXDje+u8axlkv/onxj6hnMiBQTgkM7
xB7Pkk5n/d7/3umFbepHSCGRUbxbg5m72OpWNdS6Lid+Om3XoMIsyWL7fzBXzann
JdfA01SHqewHOT5q8LKgvhDapmv4YE/H3zZpSwdJrBAlT0oiDpLWPIk3Oig+bktb
pkTJER6gy4/yVs/Ko1zPS8xqs0bBrIxXTP0xwSfGr2g9jmKxR9uZ4aXBVRktOc3+
kxxAWMjold3FNny4ZyDQtiES/fAQnhO+xwIDAQAB
```
   - Identify where the public IP addresses of official Telegram servers are located:  
      ```
      "149.154.175.50", "149.154.167.51", "95.161.76.100", "149.154.175.100", "149.154.167.91",
      "149.154.171.5", "149.154.175.10", "149.154.167.40", "149.154.175.117"
      ```
   - Patch/Replace each of them with the same IP address for the sample WTelegramServer instance:  
      `34.73.170.46` _(you might need to add an extra \0 byte if you're patching binary)_
   - Follow method 1 recommendations for running the program
   
## What is supported?
- SignIn/SignUp (with fake 4-digit SMS, or real 5-digit App code)
- Search box for public users
- Creating basic groups
- Sending messages in private, saved messages & basic groups
- Editing (modifying), deleting messages
- File download/uploads
- Sending/receiving photos & documents (audio/videos/GIFs/files)
- Message entities (text styles)
- Stickers/Stickersets, Custom Emojis, Emojies and their :keywords:
- Sending Dice, VCard contacts, Geo/Venue location (but not tested)
- Sending media behind spoiler, media below text
- Replying to messages (within same chat)
- Basic forwarding of messages
- Changing profile firstname/lastname/username/bio
- User status (online/offline)
- Fetching History/UpdatesDifference
- Management of active dialogs (inbox/outbox checkmarks, unread messages)
- Viewing read-stamp of messages in PM
- List of active sessions
- Modification of Privacy Rules
- Simulate multiple DCs (one real instance for now but highly based on DB with some caching)
- Saving of drafts messages
- Saved Messages (incl forward to saved, with track back)
- Lots of static data (countries, timezone, phone number formats, featured stickers...)
- "Typing" actions and fullscreen interactive animations
- Auto detection of urls, email, mentions, /command, #hash, $CASH entities in messages

Developing a server with all above features was achieved in just one month!!  
_(from scratch, except stuff reused from my open-source WTelegramClient library)_

- Send verification code to existing session if phone number already registered
- Forwards with drop author
- Suggest stickers on emoji
- Leaving group, deleting groups
- Kick/Add user in group (with optional history)
- Invite links
- Chat notifications settings (mute/unmute)

## What is not (yet) supported?
- Supergroups, Channels
- Login via QR-Code
- Enforcement of most personal Privacy Rules (but the logic is ready)
- Stories, Stars, Invoice/Payments, Giveaway, Monoforums
- Replying from another chat
- Reactions
- Archived chats, Chat Folders
- Generating media thumbs server-side (but storage of thumbs is supported)
- Support older API layers below 216
- Secret chats
- Contacts management
- Blocking users, muting notifications
- Account & Message TTL (self-destruct)
- Bots, business stuff, most premium-specific stuff
- Sending photos/documents from URL
- Webpage previews
- @gif bot (and therefore the GIF panel)
- Scheduled messages

## For the tech-savvy
Implemented:
- Multi authentification/sessions 
- Binding temp auth keys (RAM)
- Salts changing every 30 min, Access Hash
- File References (RAM)
- Updates / GetDifference (PTS, SEQ, QTS)
- ShortMessages updates
- Message History
- Dialogs and chat participants
- Outbox Read Dates (RAM)
- Sending messages from system account 777000
- All the MTProto Transport protocols + obfuscation

Not yet implemented:
- TLS handshake
- Protection against API abuse
- InputPeer*FromMessage / InputUserFromMessage

RAM=not stored in DB
