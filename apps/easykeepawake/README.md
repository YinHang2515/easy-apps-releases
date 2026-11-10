# EasyKeepAwake

A lightweight Windows utility that keeps your system active when idle by simulating mouse clicks or keystrokes, useful during long reads or meetings.

## Features

- **Two keep-alive modes**:
  - **Click mode**: Sends a left-click at the current cursor position
  - **Keystroke mode**: Types `a` then deletes it (visible feedback)
- **Configurable timing**: One interval controls the idle threshold and action frequency (5-300 seconds)
- **System tray**: Close button minimizes to tray, doesn't exit
- **On/Off toggle**: From the main window or tray menu
- **Power-aware pause**: By default, pauses simulated input on lid close, display off, sleep, or lock; preserves your ON/OFF choice
- **Media-aware pause**: Pauses simulated input during reported playback, with an exception for NetEase CloudMusic's music sessions
- **Keep awake with lid closed**: Optional system and display wake requests with temporary Windows lid settings, active only while the main switch is ON
- **Resizable window**: Controls fit at the default size, and the main window can be resized
- **Optional coffee tip**: The small coffee icon beside Details opens the Stripe support page in your browser
- **Compact details**: Open **Details** for status, lid mode, idle time, and action count
- **Start with Windows**: Optional launch at sign-in, minimized to the tray, with your saved ON/OFF state, mode, and interval
- **Persistent settings**: Config saved to `%APPDATA%/FocusKeeper/config.json`
- **Portable Windows package**: The executable and bundled `_internal` runtime are distributed together; no Python installation is required

## Download

Visit the [EasyKeepAwake website](https://mango-forest-003c80100.4.azurestaticapps.net) for the latest verified download:

1. Download [EasyKeepAwake-v1.5.4-win64.zip](https://mango-forest-003c80100.4.azurestaticapps.net/downloads/EasyKeepAwake-v1.5.4-win64.zip)
2. Extract the entire ZIP to a permanent location (e.g. `C:\Tools`)
3. Open the extracted `EasyKeepAwake` folder and run `EasyKeepAwake.exe`

Keep `EasyKeepAwake.exe` and its `_internal` folder together whenever moving the app. The package retains required dependency license notices and omits the product README; usage documentation remains in this repository.

The [v1.5.4 GitHub release](https://github.com/YinHang2515/easy-apps-releases/releases/tag/easykeepawake-v1.5.4) also provides the verified ZIP. Previous releases remain available in the shared download repository.

The v1.4.1 single-file build could be blocked by Windows Application Control. This folder package remains subject to device policy; if startup is blocked, contact your device administrator to confirm an approved deployment method.

## Usage

1. Launch the app — first launch starts **OFF**; later launches restore the saved state
2. Pick your **Keep-Alive Mode** (click or keystroke)
3. Set **Interval** (seconds of inactivity required after your latest mouse or keyboard input, and the minimum time between actions)
4. Click **Turn ON**
5. Optionally check **Start with Windows** (off by default; no administrator rights needed)
6. Close the window — it minimizes to the system tray; right-click the tray icon for Show / Toggle / Exit

Automatic pauses preserve your ON/OFF preference. With the lid option disabled, an app that was ON resumes once the lid is open, the display is on, and Windows is awake and unlocked, then waits a full configured interval before sending input. An app that was OFF stays OFF. You can turn it OFF while paused to prevent automatic resumption. The main window shows **PAUSED**; open **Details** for the reason and live statistics. The tray icon is red while paused and green when active.

Reported playback also pauses simulated input, including muted or background playback. **Details** shows **Media playing**. PotPlayer and browsers may report video as music or omit its type, so EasyKeepAwake pauses for their playing or changing sessions regardless of that label. Once all blocking playback pauses or stops and other pause conditions clear, the app waits a full interval before acting; new mouse or keyboard activity restarts that wait.

NetEase CloudMusic is the supported music exception: a session with the exact app ID `cloudmusic.exe` (case-insensitive) and type `Music` does not pause input. An explicit video or unknown type still pauses, even from this app. Music in PotPlayer, a browser, or another unlisted app also pauses because Windows does not reliably distinguish it from video. This exception cannot identify a music video that CloudMusic itself incorrectly labels as music. Apps and websites that publish no Windows media session cannot be detected. If media monitoring is unavailable, input stays paused and **Details** shows **Media monitoring unavailable**.

For Terminal / PowerShell, EasyKeepAwake must have the same or higher Windows privileges as the target window. If the terminal was opened with **Run as administrator**, choose **Exit** from the EasyKeepAwake tray menu, then right-click `EasyKeepAwake.exe` and choose **Run as administrator** too. Ordinary terminals work with an ordinary launch. **Start with Windows** launches with ordinary user privileges; it does not automatically elevate the app.

If Windows rejects input, the main window shows **INPUT BLOCKED**, **Details** explains how to resolve it, and the failed action is not added to **Actions Sent**. The app retries at the configured interval and clears the error after a successful send. Click mode clicks at the cursor; a console may show no visible response to a click. Keystroke mode needs an interactive input prompt to show `a` and Backspace, and a foreground program may interpret those keys differently.

To keep Windows awake with the lid closed, check **Keep awake with lid closed** and turn the main switch ON. EasyKeepAwake requests that Windows keep the system and display awake, and temporarily sets the current power plan's lid action to **Do nothing** for both battery and plugged-in use. Unchecking the option, turning the main switch OFF, or choosing **Exit** restores the previous lid actions. If a previous run ended unexpectedly, EasyKeepAwake recovers its saved original settings on the next launch before applying the current choice.

The built-in display may still turn off when the lid closes because of hardware or firmware behavior. The option does not override an explicit sleep command or prevent input from pausing on session lock. On Modern Standby (S0) laptops, sleep can include background activity; EasyKeepAwake does not change the system's sleep mode.

The Details window can be closed and reopened independently. Hiding the main window also hides Details. **Details** stays concise: current status and pause reason, lid mode ON/OFF, idle time, and action count.

Keep the complete app folder in a permanent location when enabling **Start with Windows**. If you move it, keep the executable and `_internal` together, run it from the new location, and turn the option off and on again. Sign-in launch uses `--startup` and stays in the tray. A manual launch opens the window if the app is not already running; otherwise, use **Show** from its tray menu.

## Updating

EasyKeepAwake was formerly named EasyKeepFocus, and earlier FocusKeeper. Choose **Exit** from the existing tray icon before updating. Download and fully extract the new ZIP, then run `EasyKeepAwake.exe` from its complete app folder. The new app cannot start while an older copy is still running. Check the window title or tray tooltip to confirm the new version is running.

All installations retain the legacy `%APPDATA%\FocusKeeper` data folder. Settings and lid-policy recovery records stay in place.

On the first launch after upgrading, an existing **Start with Windows** registration for EasyKeepFocus or FocusKeeper is updated to launch the new app. Startup that was disabled stays disabled.

