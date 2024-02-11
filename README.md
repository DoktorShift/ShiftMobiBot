##### This is a Fork of SatsMobiBot, Thanks Massimo for Sharing.

# @Shift.mobiBot

A Telegram Lightning ⚡️ Bitcoin wallet.

This repository contains everything you need to set up and run your own Tip bot and POS facility. If you simply want to use this bot in your group chat without having to install anything just start a conversation with [@ShiftMobibot](https://t.me/ShiftMobibot) and invite it into your group chat.

The system automatically creates a POS facility connected to your user. Getting payments in Lightning is immediate and requires no additional software installed and no externa APPs.

The system now provides also Scrub service. This service can be activated and deactivated realtime. This makes possible to automatic forward all incoming payments to an external Lightning Address. You can always change this address whenever you want or disable the service at all.

## Setting up the Bot

### Installation

This Bot adds features from @LightningTipBot. It has been created by massmux to become a suite together to NFC Cards and other services connected. Being an open source project you are welcome to PR or to install yourself. This Bot by default is created with docker and runs a postgreSQL instance as database backend. I marked the Sqlite version as deprecated.

To build the bot from source, clone the repository and compile the source code.

``` 
 git clone https://github.com/DoktorShift/ShiftMobiBot.git
``` 
``` 
 cd LightningTipBot
``` 
``` 
 export CGO_ENABLED=1
``` 
``` 
 go build .
``` 
``` 
 cp config.yaml.example config.yaml
```
After the configuration (see below), start it using the command
``` 
./LightningTipBot
``` 

### Configuration

You need to edit config.yaml before you can start the bot.

#### Create a Telegram bot

First, create a new Telegram bot by starting a conversation with the [@BotFather](https://core.telegram.org/bots#6-botfather). After you have created your bot, you will get an **Api Token** which you need to add to `telegram_api_key` in config.yaml accordingly.

#### Set up LNbits

You can either use your own LNbits instance (recommended) or create an account at timecatcher.lnbits.de to use their custodial service (easy).

1) Create a wallet in LNbits (reachable by the bot via lnbits_url).
2) Get the Admin key in the API Info tab of your user (lnbits_admin_key).
3) Enable the User Manager extension.
4) Get the Admin ID of the User Manager (lnbits_admin_id).

![lnbits_setup](https://github.com/DoktorShift/ShiftMobiBot/assets/106493492/53ab010c-e761-44b7-8e26-89d629b3974f)


Copy&Paste these information into config.yaml


## Create Systemd Service

When your Bot is gracefully running, create a systemd job to run it 24/7

```
sudo nano /etc/systemd/system/shiftmobi.service
```

Copy&Paste this into and crtl+X ENTER to save

```
[Unit]
Description=shift.mobi

[Service]
User=UserName
WorkingDirectory=Path_to_working_directory
ExecStart=Path_to_working_directory/LightningTipBot
Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target
```
Edit _User, WorkingDirectory, ExecStart regarding_ to your settings.


## Made with

- [LNbits](https://github.com/lnbits/lnbits) – Free and open-source lightning-network wallet/accounts system.
- [telebot](https://github.com/tucnak/telebot) – A Telegram bot framework in Go.
- [gozxing](https://github.com/makiuchi-d/gozxing) – barcode image processing library in Go.
- [ln-decodepay](https://github.com/fiatjaf/ln-decodepay) – Lightning Network BOLT11 invoice decoder.
- [go-lnurl](https://github.com/fiatjaf/go-lnurl) - Helpers for building lnurl support into services.

## What this Bot can do

This is a Lightning Wallet into a Telegram Bot, but more functionalities have been added:

- Integrated full POS service
- POS Link generation for executing POS on an external device
- Scrub service for forwarding all incoming payments to an external address, making the POS actually not custodial if activated

## Feature coming soon
- Activation of the NFC Card can be asked (Feature coming soon)
- Notifications of Cards activations
- /casback command to show a code to get a CashBack from a shop owner. In this case the amount is received and can be spent using the NFC Card connected to the Bot

You can give the use of this Bot to your community. For example a physical shop manager can use this Bot + the NFC Cards + POS facility, all together. They can give the cards to their clients and send cashback for each purchase, thanks to the cashback command. The client will be able to spend the money just using his card everywhere.

