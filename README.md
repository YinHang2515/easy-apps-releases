# FocusKeeper

A lightweight Windows utility that keeps your system active when idle by simulating a mouse click or keystroke.

## Download

Get the latest Windows 64-bit version from [Releases](https://github.com/YinHang2515/focuskeeper-releases/releases/latest).

1. Download `FocusKeeper-vX.Y.Z-win64.zip`.
2. Extract the entire ZIP into a permanent folder, such as `C:\Tools\FocusKeeper`. Keep `FocusKeeper.exe` and its accompanying files together.
3. Run `FocusKeeper.exe`. No Python installation is required.

## Features

- **Two modes:** click at the current cursor position, or type `a` and delete it.
- **Configurable interval:** 5–300 seconds, used for both the idle threshold and action frequency.
- **Automatic pause:** stop simulated input when the lid closes, the display turns off, Windows sleeps, or the screen locks. Resume only after those conditions clear, then wait a full interval before sending input.
- **Saved settings:** restore your last ON/OFF choice, mode, and interval. First launch defaults to OFF.
- **Start with Windows:** optional startup at sign-in, minimized to the tray. Disabled by default; no administrator rights required.

Automatic pauses preserve your ON/OFF choice. Turning OFF while paused prevents automatic resumption. Windows power settings determine whether the computer actually sleeps when you close the lid. On Modern Standby (S0) laptops, background activity can continue during sleep; FocusKeeper does not change the system's sleep mode.

## Usage

Choose a mode and interval, then select **Turn ON**. Enable **Start with Windows** if you want FocusKeeper to launch at sign-in.

Closing the window minimizes it to the system tray. Right-click the tray icon for **Show**, **Toggle On/Off**, or **Exit**. If FocusKeeper is already running, use **Show** to open its window; launching the executable again does not open another instance.

The tray icon is green when active and red when OFF or paused. The window shows the reason for a pause.

## Updating or Moving the App

Choose **Exit** from the tray before replacing the app files. Download the new ZIP and extract the entire folder. Your settings are retained in `%APPDATA%\FocusKeeper\config.json`.

The window title and tray tooltip show the running version, starting with v1.2.1. Check them after updating to confirm the new copy is running.

If the app's location changes, launch it from the new folder and turn **Start with Windows** off and on again to update its startup path.

This repository hosts public downloads and product information.
