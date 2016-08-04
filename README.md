# Telegram Bot
---

Starting project: [telegram-bot-bootstrap](http://kengz.me/telegram-bot-bootstrap/) by [Wah Loon Keng](https://github.com/kengz)

## Installation
- new project folder
- `cd` into it
- run `npm install telegram-bot-bootstrap`

## Usage

### Local
<pre>
  // testbot.js
  var bot = require('telegram-bot-bootstrap');
  var fs = require('fs');

  var myBot = new bot(your-token);

  myBot.getUpdates().then(console.log)
  // → you'll see an update message. Look for your user_id in "message.from.id"

  // Once you get your id to message yourself, you may:
  myBot.sendMessage(your-id, "Hello there")
  // → you'll receive a message from Alice.
  .then(console.log)
  // → optional, will log the successful message sent over HTTP
</pre>

##### Messages Examples
<pre>
  myBot.sendMessage(86953862, 'Hey wanna see some cool art?');

  myBot.sendPhoto(86953862, fs.createReadStream( __dirname + '/image.jpg' ), 'Image subtitle').then(console.log)
</pre>

![Message Example](/docs/demo-pic.jpg "Example 1")

### Custom Keyboard Example
<pre>
  var kb = {
          keyboard: [
              ['one'],
              ['two', 'three'],
              ['four', 'five', 'six']
          ],
          one_time_keyboard: true
      };
  myBot.sendMessage(86953862, "Choose a lucky number", undefined, undefined, kb)
</pre>

![Keyboard Example](/docs/demo-kb.jpg "Example 2")

### Bootstrapped, Deployable Bot

See `index.js` for deployable app, and `bot.js` to customize bot commands.

We distinguish the bot from the API: `bot.js` extends `API.js`, and will be the deployed component.

This whole project is bootstrapped and deploy-ready: all the details of HTTP and server stuff taken care of for you. I deploy this git project onto my Heroku and voila, my bot is alive.

#### Setup

In addition to the token, you'll need a webhookUrl. If you deploy your Node app to Heroku, then the webhookUrl is simply your Heroku site url. Set both of them in the .env file:

<pre>PORT=8443
TOKEN=your-Telegram-bot-token
WEBHOOK=your-webhook-url</pre>
The sample available is an echo-bot. To make your bot do interesting stuff, head over to bot.js, under the handle method, start writing your own from below the Extend from here comment.

The bot inherits all the API methods, so you can simply call them for example by this.sendMessage.

#### Deployment

The server is deployed in `index.js`, and a bot is constructed to handle all HTTP POST calls from Telegram.

I use Heroku. This shall work for any other services too. Once I'm done setting up, I do:

<pre>git push heroku master</pre>
And done. Start talking to the bot.
