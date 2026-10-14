# SHADOWLANDS: Rift Runner

A free, stylized 3D browser action-adventure built with Three.js. Works on modern Android browsers and desktop browsers. GitHub Pages hosts the static game. Optional Firebase Realtime Database shares player positions and presence between people who open the same deployed game.

## Included gameplay
- Third-person 3D forest, ancient portal, glowing crystals and shadow beasts.
- Keyboard + mouse controls on PC; virtual joystick and action buttons on touch screens.
- Collect crystals, fight enemies, health, points, quest progress, pause and completion screens.
- Optional online player presence / shared positions using Firebase anonymous authentication.
- No paid assets. The environment and characters are procedural shapes created in code.

## Publish the game on GitHub Pages
1. On GitHub, create a new **public** repository, for example `shadowlands-game`.
2. Upload these five files to the repository root: `index.html`, `style.css`, `app.js`, `firebase-config.js`, `README.md`.
3. Open repository **Settings → Pages**.
4. Under **Build and deployment**, select **Deploy from a branch**; choose branch `main` and folder `/(root)`, then press **Save**.
5. Wait for GitHub Pages to publish. Open the displayed URL (usually `https://YOUR-USERNAME.github.io/shadowlands-game/`). On Android, use Chrome. On the HP notebook, use Chrome or Edge.
6. If you change files, commit the changes and refresh the published page. If an old version persists, hard-refresh or wait a minute.

## Enable online multiplayer (Firebase setup is required)
The game is playable in solo mode without Firebase. For shared online players, set up a Firebase project:
1. Visit https://console.firebase.google.com/ and create a project.
2. In Project settings, add a **Web app** and copy its config values into `firebase-config.js`. Replace all `PASTE_...` values. Use the exact `databaseURL` Firebase provides.
3. In **Authentication → Sign-in method**, enable **Anonymous**.
4. In **Build → Realtime Database**, create a database. Start in locked/production mode, then configure rules. In the rules editor use the following starter rules (Firebase Authentication is required). These rules let signed-in users read player positions and write only their own record:
```json
{
  "rules": {
    "players": {
      ".read": "auth != null",
      "$uid": {
        ".write": "auth != null && auth.uid === $uid"
      }
    }
  }
}
```
5. Publish the rules. Make sure `databaseURL` matches the created database's URL.
6. Commit the updated `firebase-config.js`, wait for Pages to redeploy, then open the game in two browsers/devices. Enter the game on both; the Players counter should update.

### Security and limitations
This is an early playable foundation, not a commercial MMO. The Firebase rules above restrict each player to their own database record, but this client-authoritative prototype is not cheat-proof. Do not add payments, valuable inventories, private data, or competitive rankings without a trusted server and stricter validation. Firebase usage has free quotas and may require billing setup depending on usage and region; keep an eye on the console. Never publish service-account credentials or private keys. The web config's API key is intended for client apps; protect access with Firebase rules and provider restrictions where appropriate.

## Controls
**Desktop:** WASD / arrow keys move, mouse controls camera, click to lock mouse, Space attacks, Shift sprints, E interacts, Esc pauses. Click the canvas to re-lock the mouse after releasing it.

**Touch:** drag the left virtual joystick to move; drag on the scene to rotate the camera; sword button attacks; up button hops; circle button collects crystals / seals the rift.

## Troubleshooting
- Blank page: open browser developer tools (F12 on desktop) and inspect Console. Check filenames/capitalization and ensure all files are in repository root.
- Game loads but no online players: confirm Firebase config, Anonymous sign-in, Realtime Database URL and rules.
- Low frame rate: close other tabs, disable browser battery saver, and lower browser zoom; this build caps pixel ratio to reduce GPU load.
- ES module/CDN imports require internet access when the page loads.
