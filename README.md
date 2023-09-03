# Watchtower telegram notifications

This repo is just a simple write-up on how to get telegram notifications from Watchtower, when a container is updated. This version is mostly focused on docker-compose, but should also work with docker run.

## Contents

1. [Installation](#installation)
2. [Complete docker-compose file](#complete-docker-compose-file)
3. [Contributing](#contributing)
4. [Disclaimer](#disclaimer)

## Installation

It's pretty easy to get telegram notifications from Watchtower. You just need to follow these steps:

### 1. Telegram Bot

Firstly, we need to create a new telegram bot. For that open a new chat with [BotFather](https://telegram.me/botfather), type in the command `/newbot` and follow the instructions. In the end you should see a message like this:

![success](https://i.imgur.com/ugOzB1B.png)

### 2. Get your chat id

After creating your bot, you need to get your chat id. For that, open a new chat with your bot, start it and tag `@get_id_bot` in the chat. You should get a message like this:

![chat id](https://i.ibb.co/0GY3cFp/Bild-2023-09-03-230007186.png)

### 3. Setup Watchtower

Now we need to setup Watchtower. For that, you need to add the following environment variables to your docker-compose file:

```yaml
environment:
    - WATCHTOWER_NOTIFICATIONS=shoutrrr
    - WATCHTOWER_NOTIFICATION_URL=telegram://HTTP_API_TOKEN@telegram/?channels=CHAT_ID
```

Replace `HTTP_API_TOKEN` with the token you got from BotFather in step 1. and `CHAT_ID` with the chat id you got from `@get_id_bot` in step 2.

### 4. (Re)start Watchtower

Now you can (re)start Watchtower:

```bash
sudo docker-compose up -d --force-recreate
```

and you should get a message from your bot, that Watchtower is running. The message should look like this:

![watchtower running](https://i.ibb.co/wB2T6vK/Bild-2023-09-03-230440535.png)

You will also get a message, when a container is updated. It should look like this:

![updated](https://i.ibb.co/QkD8ywr/Bild-2023-09-03-231219112.png)

## Complete docker-compose file

If you are still unsure, how your docker-compose file should look like, check out the `docker-compose.yml` file in this repo. Most optional settings are commented, so everything is more understandable. Just remember to replace `HTTP_API_TOKEN` with the token you got from BotFather in step 1. and `CHAT_ID` with the chat id you got from `@get_id_bot` in step 2.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

## Disclaimer
This repository is for research purposes only, the use of this code is your responsibility.

I take NO responsibility and/or liability for how you choose to use any of the source code available here. By using any of the files available in this repository, you understand that you are AGREEING TO USE AT YOUR OWN RISK. Once again, ALL files available here are for EDUCATION and/or RESEARCH purposes ONLY.
