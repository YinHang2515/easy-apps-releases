# EasyKeepFocus

A lightweight Windows utility that keeps your system active when idle by simulating a mouse click or keystroke.

## Download

Get the latest Windows 64-bit version from [Releases](https://github.com/YinHang2515/easykeepfocus-releases/releases/latest).

1. Download `EasyKeepFocus-vX.Y.Z-win64.zip`.
2. Extract the entire ZIP into a permanent folder, such as `C:\Tools\EasyKeepFocus`. Keep `EasyKeepFocus.exe` and its accompanying files together.
3. Run `EasyKeepFocus.exe`. No Python installation is required.

## Features

- **Two modes:** click at the current cursor position, or type `a` and delete it.
- **Configurable interval:** 5–300 seconds, used for both the idle threshold and action frequency.
- **Automatic pause:** by default, stop simulated input when the lid closes, the display turns off, Windows sleeps, or the screen locks. Resume after the pause conditions clear and a full interval elapses.
- **Keep awake with lid closed:** optional Windows system/display wake requests and a temporary **Do nothing** lid action while the main switch is ON.
- **Daily schedule:** select a local time to enable the lid option every day, without changing the main ON/OFF switch.
- **Compact window:** open **Details…** for pause reasons, idle time, action count, and schedule status.
- **Saved settings:** restore your last ON/OFF choice, mode, and interval. First launch defaults to OFF.
- **Start with Windows:** optional startup at sign-in, minimized to the tray. Disabled by default; no administrator rights required.

Automatic pauses preserve your ON/OFF choice. Turning OFF while paused prevents automatic resumption. With lid mode disabled, Windows keeps its existing lid and sleep behavior. Modern Standby (S0) can include background activity; EasyKeepFocus does not change the system's sleep mode.

## Usage

Choose a mode and interval, then select **Turn ON**. Enable **Start with Windows** if you want EasyKeepFocus to launch at sign-in.

Check **Keep awake with lid closed** to request system/display wakefulness and temporarily set both plugged-in and battery lid actions to **Do nothing**. Turning this option off, turning the main switch OFF, or exiting restores the previous lid actions. If the app stops unexpectedly, it retries restoration on the next launch. Some laptop firmware still turns off the built-in panel when the lid closes; this option cannot guarantee that physical panel stays lit. Actual sleep and session lock still pause simulated input.

Open **Schedule…**, enter a daily time as `HH:MM` (24-hour, this PC's local time), and save. The schedule enables only the lid option; a main switch that was OFF stays OFF. It does not wake the computer. If the time is missed during sleep or while the app is closed, it applies once after wake or launch. **Clear schedule** removes the plan without changing the current switches.

Closing the window minimizes it to the system tray. Right-click the tray icon for **Show**, **Toggle On/Off**, or **Exit**. If EasyKeepFocus is already running, use **Show** to open its window; launching the executable again does not open another instance.

The tray icon is green when active and red when OFF or paused. **Details…** shows the reason for a pause and live statistics.

## Updating or Moving the App

EasyKeepFocus was formerly named FocusKeeper. Choose **Exit** from the existing tray icon before replacing the app files. Download the new ZIP, extract the entire folder, and run `EasyKeepFocus.exe`. The new app cannot start while an older copy is still running.

All installations retain the legacy `%APPDATA%\FocusKeeper` data folder for compatibility. Your settings, daily schedules, and lid-policy recovery records are preserved, including when returning to an older version.

The first launch after upgrading updates an existing **Start with Windows** registration to launch the new app. Startup that was disabled stays disabled.

The window title and tray tooltip show the running version, starting with v1.2.1. Check them after updating to confirm the new copy is running.

If the app's location changes, launch it from the new folder and turn **Start with Windows** off and on again to update its startup path.

This repository hosts public downloads and product information.
