<p align="center">
  <img src="https://github.com/aximut/jitsi-meet-modbot/raw/master/assets/logo-text.png" alt="ModBot" width="600" />
</p>
<br/>

# ModBot 🗫 📢 🤖 - The All-In-One Moderation and Management Bot for Jitsi Meet

### Simple, effective 🚀

ModBot helps you in all cases where you want to partially or fully automate the moderation of Jitsi Meet conferences or support moderators in their tasks.
ModBot allows you to build a whole virtual conference management system on the basis of Jitsi Meet.
In contrast to other third-party systems, ModBot allows you to do this in a modular manner without any changes to the original [jitsi-meet](https://github.com/jitsi/jitsi-meet) codebase. This means that updates of the jitsi-meet system remain fast, hassle-free and straightforward. ModBot follows the philosophy: Do one thing - and do it well!

You want to open a specific room at a certain time and keep it open until the planned conference ends? Or you want to use a bunch of permanent rooms and have permanent conference links that work all the time? But you also want to effectively prevent strangers or intruders from using your Jitsi Meet server? ModBot is the tool you were looking for!

### Total control over your Jitsi Meet installation 💪

ModBot allows you to freely and granularly manage resources (rooms, passwords, settings) on your Jitsi Meet server in the way YOU want it. Stay in full control. All the time.

In a more sophisticated setup, you can combine ModBot with your own database solution and create permanent conference links, while ModBot ensures that the conference rooms on Jitsi Meet open automatically and admit waiting participants at the scheduled dates. When the conference is over, the room can be closed and all participants can be expelled automatically.

And all of this without requiring a moderator to be present and without the compromise of using a non-secure public domain setup, where everybody can open a room and abuse your Jitsi Meet server. No more complicated passwords when you just want a simple link for your conference to just work, when you want it.

What's more, ModBot runs on Linux, Mac and Windows, so you can decide where and how you want to manage your conferences.

ModBot is tested and developed on Jitsi Meet versions with secure domain setup.

## Features ⚡

- Full [Secure Domain 🔐](https://jitsi.github.io/handbook/docs/devops-guide/secure-domain) support.
- Permanent rooms that remain open all the time.
- Automatic creation of meeting rooms and admission of waiting participants.
- Automatic password protection of meeting rooms.
- Automatic lobby room setup.
- Conference duration support and automatic closure of rooms on end.
- Kicking out all remaining participants.
- Holding meeting rooms open until the first participant enters the room.
- Hiding ModBot from the participants list.
- Automatic detection of Jitsi Meet server settings.
- Support for Linux, Mac and Windows.

## Download 🌐

You can download the recent version of ModBot for Linux, Mac or Windows from the [release section](https://github.com/aximut/jitsi-meet-modbot/releases).

## Usage 📖

This tool is optimized for a server with a secure domain setup. If you have not done so yet, setup your Jitsi Meet server following the [secure domain setup guide](https://jitsi.github.io/handbook/docs/devops-guide/secure-domain).

The tool is used best in conjunction with a time-based scheduler, such as `cron`. Every time a conference is planned, the scheduler is supposed to trigger ModBot with the respective parameters using command line arguments or custom JSON configuration files.

### Command-line usage

```bash
modbot [options ...]
```

### Example

To see ModBot in action, download the [example config file](exampleConfig.json) to the same folder as ModBot.
Then [open this url](https://beta.meet.jit.si/modbotexample) and run the following command:

```bash
modbot -f exampleConfig.json
```

### General options
```
  -h, --help            Show this help message and exit.
  -v, --version         Show product version and exit.
  -f, --file file ...   Load one or multiple config file(s).
                        Config files must be in JSON format and can contain all command line
                        arguments as parameters. If both, files and command line arguments are given,
                        the command line arguments take precedence over the file parameters. If
                        multiple files are specified, the last files take precedence over the first
                        files. This allows to define a base config and override individual
                        parameters.
  -o, --show            Show the resulting config in JSON format and exit.
```
### Server options

  These options define the Jitsi Meet server to which ModBot will establish a
  connection.
```
  -z, --url string   URL of the Jitsi Meet server.
```
### Moderator options

  If these options are present, ModBot will authenticate as a moderator on the
  server.
  This is only required in a secure domain server setup.
```
  -u, --username string   Moderator username.
  -p, --password string   Moderator password.
```
### Room options

  After a server connection has been established, ModBot will create a meeting
  room according to these options.
```
  -r, --room string       Room name.
  -s, --subject string    Room subject.
  -c, --passcode string   Room password.
  -l, --lobbyEnabled      Enable room lobby.
```
### Conference options

  These options define the behavior of ModBot during the conference.
```
  -d, --duration milliseconds   Conference duration.
                                ModBot will automatically leave the conference after this time. If this
                                option is not given, ModBot will only open the room to let waiting
                                participants in and exit directly afterwards. If this option is -1, the room
                                will be created permanently.
  -w, --waitForFirstUser        If this option is given, ModBot will wait and only leave the room after the
                                first participant has joined the conference. In a secure domain setup, this
                                is helpful in case participants join later than the scheduled time.
                                Otherwise, the room that ModBot opens would be immediately closed again if
                                there is no other participant in the room at that time.
  -k, --kickAll                 If this option is given, all participants will be kicked out of the room as
                                soon as ModBot leaves the conference. In secure domain setups, this
                                automatically closes the room and effectively prevents new participants from
                                entering.
  -g, --kickGrace               [Future/Premium] If this option is given, ModBot will gracefully announce the
                                end of the conference before kicking participants out of the room. This
                                option is only available on request in a future version of this product.
  -m, --welcomeMessage string   [Future/Premium] If this option is given, ModBot will send a custom welcome
                                message to all new participants in the chat as they join the conference. This
                                can be used to introduce conference details, usage conditions or additional
                                resources to the participants. This option is only available on request in a
                                future version of this product.
```
### ModBot options

  These options define the appearance of ModBot.
```
  -n, --name string   [Future/Premium] The name under which ModBot will appear in the participants
                      list. This option is only available on request in a future version of this
                      product.
  -i, --icon string   [Future/Premium] The icon under which ModBot will appear in the participants
                      list. This option is only available on request in a future version of this
                      product.
  -x, --hidden        In case the server supports a hiddenDomain, ModBot will try to hide from the
                      participants list.
```

## Bugs 🐞

- Currently, for XMPP communication only the `BOSH` protocol is supported, no websockets.
- The instance [meet.jit.si](https://meet.jit.si) does not work currently. However, we ran successful tests on [beta.meet.jit.si](https://beta.meet.jit.si).

## License ⚖

See the [license file](https://github.com/aximut/jitsi-meet-modbot/raw/master/LICENSE).

## Open Future 🔮

ModBot emerged from the need to have a better management tool for the great Jitsi Meet conferencing solution.
We would love to make this tool open source. However, our development costs and the effort of devising a clever tooling based on modern technologies need to be covered. Also, continued maintenance is required, as the official Jitsi Meet API is likely to introduce breaking changes, making ModBot useless. Given that a lot of companies earn on proprietary conferencing solutions, we think it is only fair to demand compensation for making an already free tool open source. However, we have no plans on this yet. We can think of doing an open collective.
There are various features we would love to incorporate directly into the ModBot, such as a web control frontend, intelligent room generation, email invitations, automated internal schedules with databases, user and role management and improved authentication technologies, to name just a few. Also, external calendar integrators are a possible option, such that the meeting rooms get automatically assigned and opened based on calendar entries.
We can also imagine to develop and maintain this software as a part of the official Jitsi Meet tooling, as we think it could be useful for a broader community.

[Feel free to discuss this with us.](https://github.com/aximut/jitsi-meet-modbot/discussions/1)
