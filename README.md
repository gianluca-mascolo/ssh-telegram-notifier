# ssh-telegram-notifier
Small sshrc to notify logins to a telegram bot
## Scope
This script allow you to get notified on telegram everytime someone login to a server via ssh
## How it works
Every time an user login, /etc/ssh/sshrc is executed (see man ssh). This sshrc will curl a message to your custom bot with basic information about login.
## Screenshot
![sshnotify](https://user-images.githubusercontent.com/20320073/36080019-23c03c16-0f8a-11e8-8fb1-2079dab1de15.png)
## Setup
- Contact @BotFather and create a new bot.
- Write down your token and use it in variable TELEGRAM_BOT_TOKEN
- Open the bot you created and start conversation
- Retrieve you chat id and use it in variable TELEGRAM_CHAT_ID
```bash
curl --silent "https://api.telegram.org/bot${TELEGRAM_BOT_TOKEN}/getUpdates" | jq .
```
- modify sshrc with TELEGRAM_BOT_TOKEN and TELEGRAM_CHAT_ID
- copy it to /etc/ssh
```bash
cp sshrc /etc/ssh/sshrc
chown root:root /etc/ssh/sshrc
chmod 0755 /etc/ssh/sshrc
```
- if you are logged into server via ssh, leave the current shell open and test the script making a new login
- enjoy!
## Possible improvements
The sshrc can be read by every user on the system, exposing you telegram bot password.
It will be better if one can have a separate daemon running by a private user that accept an incoming message from sshrc and write to your bot.
## Thanks to
https://github.com/lazyfrosch/icinga2-telegram
https://metzlog.srcbox.net/2016/01/monitoring-notifications-via-telegram/
## Follow me!
Do you like it? Follow me on telegram: http://t.me/linuxcheatsheet
