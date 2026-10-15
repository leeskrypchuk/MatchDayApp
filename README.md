# Eagles Matchday – Android app

The U16 Eagles match-day app (pre-match routine, team selection, live match centre,
history and exports) as an Android app. It runs full screen, works offline, and keeps
all its data on the phone.

## Getting the app on your phone

1. Create a **private** repository on GitHub (for example `eagles-matchday-android`).
   Keep it private: it holds the app's signing key.
2. Upload everything in this folder to the repository and commit to the `main` branch.
   (On github.com: *Add file → Upload files*, drag the whole folder contents in,
   including the hidden `.github` folder. Or use GitHub Desktop or `git push`.)
3. Open the **Actions** tab. The *Build Android app* run starts by itself and takes about
   five minutes. When it shows a green tick, open the **Releases** section on the
   repository's front page.
4. On your Android phone, sign in to GitHub in the browser, open the latest release and
   tap **EaglesMatchday-1.0.N.apk** to download it.
5. Tap the downloaded file. Android will ask you to allow installing apps from your
   browser (or Files app) once – allow it, then tap **Install**.

### Updates

Every push to `main` builds a new release with a higher number. Installing it updates the
app in place, so your squad and matches stay. You can also start a build by hand from
*Actions → Build Android app → Run workflow*.

## What's different from the web version

| | Web version (claude.ai) | Android app |
|---|---|---|
| Data | Synced to Claude, same on phone and laptop | Stored on this phone only |
| Exports | Download prompt | Save to Downloads, or Share (email, Drive, WhatsApp) |
| Copy line-up for G sheet | Clipboard | Clipboard |
| Screen | Browser view | Full screen, screen stays on while the clock runs |
| Backup | – | History tab → Backup & restore |

The first launch loads the squad, plan and the six matches that were in the web version on
15 October 2026. After that the two versions are separate.

**Back up now and then** (History → Backup & restore → Share backup → Google Drive or
email), because uninstalling the app or resetting the phone deletes its data.

## Project notes

- `app/src/main/assets/www/index.html` – the app itself (HTML/CSS/JS), with fonts and
  SheetJS (Apache-2.0, `xlsx-LICENSE.txt`) bundled for offline use. Fonts: Barlow and
  Barlow Condensed (SIL OFL, `fonts/OFL-LICENSE.txt`).
- `app/src/main/assets/www/seed.json` – the data loaded on first launch.
- `MainActivity.java` – a WebView that serves the page from the app's assets and adds a
  small bridge for saving and sharing files, the clipboard, keeping the screen on and the
  back button.
- `app/eagles-matchday.jks` – the signing key (password `eagles-matchday`). Every build is
  signed with it so updates install over the top. If you lose it, the next build won't
  update the installed app; you'd have to back up, uninstall and reinstall.
- Built with Android Gradle Plugin 8.5.2, Gradle 8.9, compile/target SDK 34, min SDK 26
  (Android 8.0+).
- To build on a computer instead: open the folder in Android Studio and choose
  *Build → Build App Bundle(s) / APK(s) → Build APK(s)*.
