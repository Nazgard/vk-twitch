# Praden Live

Single-page dark layout for watching the VK Video live player together with a custom Twitch chat for `praden`.

Live page: https://nazgard.github.io/vk-twitch/

## Features

- VK Video embedded player.
- Custom Twitch chat connected through Twitch IRC WebSocket.
- 7TV and FFZ emote rendering.
- Tab completion for loaded emote names.
- Clickable chat links, including Twitch clips.
- Resizable chat column.
- Theater mode with only player and chat visible.
- Local-only Twitch OAuth token storage for sending messages.

## Run Locally

```bash
node server.mjs
```

Open:

```text
http://localhost:5173
```

The app is static, so `index.html` is the main artifact. The local server is included for convenient development and for environments that need a real hostname.

## Sending Chat Messages

Reading chat works anonymously. Sending messages requires a Twitch OAuth token with these scopes:

```text
chat:read chat:edit
```

Create a token through Twitch:

1. Open https://dev.twitch.tv/console/apps
2. Create an application.
3. Add this OAuth redirect URL:

```text
http://localhost:5173
```

4. Copy the application's Client ID.
5. Open this URL after replacing `CLIENT_ID`:

```text
https://id.twitch.tv/oauth2/authorize?response_type=token&client_id=CLIENT_ID&redirect_uri=http://localhost:5173&scope=chat:read+chat:edit
```

6. Copy the `access_token` from the redirected URL and paste it into the app as:

```text
oauth:ACCESS_TOKEN
```

The token is stored only in your browser's `localStorage`.

## Notes

- 7TV and FFZ emotes are loaded from their public APIs in the browser.
- The Twitch chat connection uses `wss://irc-ws.chat.twitch.tv:443`.
- VK Video and third-party chat APIs may change independently of this project.
