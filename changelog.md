# Discordie changelog

## 2016-04-14, Version 0.5.2

#### Fixes:

  - Fixed audio subsystem breaking (not buffering data) when using
    [PM2](http://pm2.keymetrics.io/) (process manager);

## 2016-04-13, Version 0.5.1

#### Fixes:

  - Rate limited file uploads with streams now resend data correctly;

#### Performance:

  - Minor performance improvement for audio mixing without volume set.

## 2016-04-12, Version 0.5.0

#### New:

  - High level audio streams (`AudioEncoderStream`, `FFmpegEncoder`,
   `OggOpusPlayer`, `WebmOpusPlayer`),
    instantiated using `IVoiceConnection.createExternalEncoder`
    and `IVoiceConnection.getEncoderStream`.

## 2016-04-09, Version 0.4.4

#### New:

  - Rate limit handling for messages. All messages are now put in a queue
    and sent sequentially;
  - Low level audio API extensions (`AudioEncoder`) -
    new methods `.enqueueMultiple` and `.clearQueue`;
  - Event `GUILD_CREATE` now has a parameter `becameAvailable` to
    discriminate between joined and unavailable guilds.

#### Fixes:

  - Normal precision scheduling now processes packet queue correctly;
  - AudioEncoder queue changed to pause after 1 second of inactivity;
  - V4 READY timeout changed to reset after each `GUILD_CREATE`;
  - Fixed voice disconnecting after resuming gateway connection;

## 2016-04-06, Version 0.4.2

#### New:

  - Gateway V4 support;
  - Exposed `GATEWAY_RESUMED` event;
  - Bans now can be added without member object - `IGuild.ban(user)`.

## 2016-03-25, Version 0.4.0

#### Notable changes:

  - Fully migrated to bot multiserver voice API (user accounts no longer can
    connect to more than one guild concurrently);
  - Improved voice disconnect handling logic: more info in `VOICE_DISCONNECTED`
    event docs (no breaking changes);
  - Presence updates for friend lists are no longer dispatched over
    `PRESENCE_UPDATE` event;
  - *(Discord-side)* `Invites.accept` no longer works on bot accounts.

#### New:

  - Exposed `user.bot` boolean property;
  - Implemented offline guild members requesting:
   `Users.fetchMembers(singleGuildOrGuildsArray)`;
  - Alternative methods for deleting/editing messages by id:
    - `Messages.editMessage(content, messageId, channelId)`;
    - `Messages.deleteMessage(messageId, channelId)`;
  - Pending voice connections can now be cancelled with `.leave()` on the same
    channel.

#### Fixes:

  - `GUILD_MEMBER_REMOVE` is now handled correctly and actually removes
    members from cache;
  - Fixed `IGuild.getPruneEstimate()` and `IGuild.pruneMembers()`;
  - Encoder states are no longer created in proxy mode;
  - Voice connections now properly disconnect on `GUILD_UNAVAILABLE`;
  - Fixed `IVoiceChannel.joined` reporting incorrect state for pending
    connections.

#### Performance:

  - Improved performance for voice encryption and RTP muxing.

## 2016-03-09, Version 0.3.0

#### Notable changes:

  - Memory and CPU usage has been reduced greatly;
  - Implemented caching of member interfaces;
  - Messages are sorted on insertion using binary sort, sorting after fetching
    is removed;
  - `JSON.stringify` on interfaces returns a copy of raw model data instead
    of stringifying models recursively;
  - Interfaces can now be properly formatted (inspected) using `console.log`
    and `util.inspect`;

#### Fixes:

  - Fix voice state tracking on `READY` for clients in multiple servers;
  - Cache voice server address on connect and no longer attempt to resolve
    hostname during UDP packet send calls;
  - Fix `DirectMessageChannels.getOrOpen(recipient)` crashing on node 5.7.0;


## 2016-02-27, Version 0.2.1

#### Performance:

  - Improve performance of `<Collection>.get`;

#### Fixes:

  - Fix voice leave or disconnect crashing the library when called for voice
    connections on secondary gateways;
