# TV Home — Apple TV style launcher for Android TV

Ek custom Home screen (launcher) Android TV / Google TV ke liye.

- Glass-style rounded cards, focus par lift + grow + highlight
- Background ka rang focused app ke icon ke hisaab se badalta hai
- Apps row (TV apps pehle) + Quick Settings row (Settings, Network, Display, Sound, Bluetooth, Apps, Date & Time)
- Bada app naam upar, clock + date top-right
- App par OK dabake rakho: Open / App info / Uninstall
- Home button dabane par wapas pehle app par

## APK kaise banega (GitHub Actions)

1. Ye poora folder apne GitHub repo mein push karo (branch `main`).
2. Repo ke **Actions** tab mein "Build APK" chalega (3-5 min). Khud na chale to **Run workflow** dabao.
3. Khatam hone par repo ke **Releases > Latest APK** mein `tv-home-launcher.apk` milegi.
   Direct link: `https://github.com/<user>/<repo>/releases/download/latest/tv-home-launcher.apk`

Local build: Android Studio mein folder kholo, **Build > Build APK(s)**.
Ya terminal mein: `gradle assembleDebug` (JDK 17 + Android SDK chahiye).

## TV par install

**Option A — adb (PC se):**

```bash
adb connect <TV-IP>
adb install -r tv-home-launcher.apk
adb shell cmd package set-home-activity com.tvos.launcher/.MainActivity
```

**Option B — bina PC:** APK ko pendrive mein daalo, ya TV par **Downloader** app mein upar wala GitHub link
daalo. Settings mein us app ko "Install unknown apps" ki permission do.

Install ke baad Home dabao; TV poochhe ki kaunsa launcher chahiye to **TV Home** chuno.
Kuch TV (Sony, Fire TV waghera) mein stock launcher hata nahi sakte, wahan Home button par default badalne ke liye
"Launcher Manager" jaisi app lagti hai.

## Wapas stock launcher

`adb shell pm clear` ki zarurat nahi: Settings > Apps > TV Home > Uninstall, ya
`adb uninstall com.tvos.launcher`.

## Customize

- Card size / spacing: `MainActivity.kt` (`applySizes`) aur `TileAdapter` ke numbers
- Quick Settings ke shortcuts: `AppRepository.shortcuts()`
- Rang aur glow: `AuroraBackground.kt`
- Focus animation: `TileAdapter.kt` mein `setOnFocusChangeListener`
