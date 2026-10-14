# SHADOWLANDS: Rift Runner — Early Access

A small Three.js browser adventure prototype. It is free to host on GitHub Pages.

## Publish the polish update

1. Open your existing GitHub repository `shadowlands-game`.
2. Replace `index.html`, `style.css`, and `app.js` with the files from this update.
3. **Keep your existing `firebase-config.js`** — it contains your project's web configuration. Do not replace it with a placeholder copy.
4. Commit the changes to the `main` branch.
5. Open your GitHub Pages URL and hard-refresh (Ctrl+Shift+R on desktop).

## Before sharing publicly

- In Firebase Console, enable Authentication → Sign-in method → Anonymous.
- In Realtime Database → Rules, restrict the `players` path to authenticated users, and each user to their own UID. Never use public read/write rules.
- Test in two browser sessions and check that the player count and remote character presence update.
- Test on Android with mobile data and on desktop with a mouse/keyboard.
- Use your own title art, screenshots and description if you promote the game.
- Keep the word “preview” or “early access” in the description while it is still a prototype.

## Controls

- Desktop: WASD or arrow keys to move; mouse to look; Space to attack; Shift to sprint; E to collect/interact; Esc to pause.
- Android: left joystick to move; drag across the scene to rotate the camera; ⚔ to attack; ↑ to hop; ◎ to interact.

## What online means right now

Firebase synchronizes player presence and positions only. This is not a fully server-authoritative multiplayer game: quest progress, enemies, combat, anti-cheat, moderation and matchmaking are not server validated. Do not describe it as a finished MMO or store sensitive player information.

## Security and privacy

The Firebase web app config is intended for client apps, but database rules are the actual access control. Do not publish service-account JSON files, private keys, passwords, or tokens. If you add analytics, chat, accounts, or personal information later, publish a clear privacy notice and review the relevant platform requirements.

## Technical notes

The game loads Three.js and Firebase SDK modules from their public CDNs, so an internet connection is required. The updated build lowers render pixel ratio and disables real-time shadows on narrow/mobile screens to reduce load.
