+++
title = "reme - A simple CLI tool to create slack reminder"
date = 2021-08-03
[taxonomies]
categories = ["code"]
tags = ["Haskell", "Slack", "CLI"]
+++
[kyoheiu/reme](https://github.com/kyoheiu/reme)

[![asciicast](https://asciinema.org/a/fqLCIbepnV9K10YVUrWu5ImjF.svg)](https://asciinema.org/a/fqLCIbepnV9K10YVUrWu5ImjF)

### Installation
```
git clone https://github.com/kyoheiu/reme.git
cd reme
cabal install
```

You need `~/.config/reme.dhall` file to store the slack authentication token.

```dhall
{ slackToken = "xoxp-xxxxxx..."
}
```

If you'd like to change the file path, feel free to replace `path` in Main.hs.

For the token and arguments detail, see [reminders.add method | Slack](https://api.slack.com/methods/reminders.add).
