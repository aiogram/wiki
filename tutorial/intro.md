---
title: Introduction | Tutorial
description: 
published: true
date: 2020-05-05T19:20:23.099Z
tags: tutorial
---

# Introduction
Hello and welcome to aiogram tutorial! We'll learn how to create our first bot step-by-step with examples and explanations. So, **let's start!**

> In this tutorial we assume you know how to write basic code in Python, what is async and how does it work.
{.is-success}

# Installation
Before we start, we need to install aiogram. There are several ways of doing this.

> aiogram v3.0, which is used in this tutorial, is still in development. Use it with caution.
{.is-warning}

## From private PyPI
```
pip install --extra-index-url https://dev-docs.aiogram.dev/simple --pre aiogram
```
> Only the latest successful build is available in this index. All previous builds are removed before uploading a new one. All unit-tests are guaranteed to pass before publishing package.
{.is-info}


## From sources
Requirements: `git`, `pip`
```
git clone https://github.com/aiogram/aiogram
cd aiogram
git checkout dev-3.x
pip install .
```

# Quickstart
Let's begin our tutorial with a simple echo bot.

## Code

```python
from aiogram import Bot, Dispatcher
from aiogram.api.types import Message

bot = Bot("your-bot-token")
dp = Dispatcher()


@dp.message_handler()
async def echo(msg: Message):
    await msg.reply(msg.text)

if __name__ == "__main__":
    dp.run_polling(bot)
```

To check this out, follow these steps:
1. Copy this and paste it to a new file, e.g. `main.py`
1. Replace `"your-bot-token"` with your bot's actual token, which can be received from [@BotFather](https://t.me/BotFather)
1. Then run it by typing `python main.py` (assuming `python` is Python 3.7 or newer).

Interested? So, read further for line-by-line explanation!

## Explanation
Firstly, we have to import everything we need from `aiogram` package:
```python
from aiogram import Bot, Dispatcher
from aiogram.api.types import Message
```

Then, we're declaring our bot:
```python
bot = Bot("your-bot-token")
```

... and dispatcher (aka root router):
```python
dp = Dispatcher()
```

Then we create a very simple text message handler. Firstly, we register it:
```python
@dp.message_handler()
```

..., we define it:
```python
async def echo(msg: Message):
```

> Why we wrote `msg: Message` and what does it mean in Python? `Message` is an optional _type hint_, which helps your linter or IDE check the code and give suggestions on methods and fields for `msg` parameter.
{.is-info}

..., make our handler reply (`msg.reply`) to just received message with a text of the latter (`msg.text`):
```python
    await msg.reply(msg.text)
```
> `msg.reply` is a shortcut for getting current bot instance and executing `send_message` on it with already filled `chat_id` and `reply_to_message_id` parameters.
{.is-info}


And finally, start long-polling to get updates:
```python
if __name__ == "__main__":
    dp.run_polling(bot)
```

> Webhook mode is under development
{.is-warning}

> `if __name__ == "__main__"` is a well-known "guard" that prevents running some code when the module was imported ([more info](https://stackoverflow.com/questions/419163/what-does-if-name-main-do)).
{.is-info}

# What's next?
In the next section we will start writing our own bot, which uses the most common aiogram features.

[Next >>](/en/tutorial/handlers)