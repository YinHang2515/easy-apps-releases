# Windows validation checklist

Automated tests cover schedule boundaries, weekday filtering, duplicate prevention within a day, daylight saving time, lock-screen waiting and catch-up policies, input validation, and JSON persistence. They cannot prove that firmware will wake the device or that a third-party application receives clicks.

## Automated UI smoke test

```powershell
# Use an absolute output path. The test uses isolated settings, sends no mouse clicks, and makes no power requests.
./EasyClick.exe --smoke-test C:\Temp\EasyClickSmoke
```

Check `passed` and the individual results in `smoke-result.json`. Automated verification uses a simulated click interface. The UI smoke test checks module bindings, interface rendering, interactive desktop detection, selection overlay rendering, and cancellation. It does not send real clicks, lock the screen, put the device to sleep, or change power settings. Main-window screenshots render only the app interface. `overlay-local-only.png` is an overlay screenshot for local inspection; it may contain desktop content and should not be uploaded.

The items below are pending checks, not recorded passes. Test real clicks only in a test window where they have no unwanted effects.

## Language and configuration compatibility

- [ ] Select English in the top-right corner. Titles, buttons, weekdays, module actions, region descriptions, status, and help change immediately. Switching back to Chinese also takes effect immediately.
- [ ] Check tray menus, stop messages, run-once messages, region selection prompts and cancellation, and time and delay validation messages in both languages.
- [ ] Switch languages and restart the app. The selected language persists, existing custom module names stay unchanged, and new modules use the default name in the current language.
- [ ] Switch languages while a time or delay entry is incomplete. The language preference is still saved without losing existing module settings.
- [ ] At the default and minimum window sizes and at different display scales, check both languages for overlapping or clipped buttons, weekdays, actions, status, and hints.
- [ ] Start with an older configuration that has no language or action fields. It defaults to Chinese and single click while preserving names, regions, order, delays, and the pending random run time.
- [ ] Save all three actions and restart. Each module retains its action; deleting, reordering, or reselecting one module does not change another module's action.

## Interaction and clicks

- [ ] An empty configuration shows the add-module prompt. New modules default to single click. Names, regions, actions, order, and delays survive a restart.
- [ ] Before region selection, the window hides, the screen freezes, the area outside the selection dims, and the inside retains its original brightness.
- [ ] Drag in all four directions. Esc and right-click cancel; very small selections cancel; coordinates remain accurate when dragging across displays.
- [ ] Cover displays to the left with negative coordinates, vertically arranged displays, mixed 100% / 150% / 225% scaling, and gaps between displays.
- [ ] Run single-click, double-click, and right-click modules in a test window. It receives the corresponding physical left-button click, left-button double-click, and right-button click.
- [ ] Both clicks of a double-click use the same coordinates inside the region. The test window recognizes a double-click, and the module delay begins after the full double-click finishes.
- [ ] Mix all three actions and verify execution in module order, with no extra delay after the last module.
- [ ] Swap the primary mouse button in Windows. Single and double clicks still use the physical left button; right clicks still use the physical right button.
- [ ] The global shortcut, tray stop command, and window stop button all work during the countdown, module delays, and unlock waiting.
- [ ] Click a standard-privilege window from the standard-privilege app. Verify the documented limitation for higher-privilege targets and that failed clicks are not retried.
- [ ] A display layout or system time change stops the schedule instead of continuing with stale coordinates.

## Scheduling, exit, and recovery

- [ ] Include today in the schedule and set a window over the next few minutes. The random time falls inside the window, and the scheduled sequence runs only once that day.
- [ ] Before the scheduled time, stop, exit, restart, and restore the same schedule. The saved random time is reused.
- [ ] Exit between modules and reopen the app. That day's task does not replay automatically; **Run once** is still available.
- [ ] After a completed run, start the schedule again. The next eligible date is scheduled.
- [ ] Invalid time formats, a start time after the end time, no selected weekdays, invalid delay values, and empty module names prevent starting.
- [ ] Closing the window while running hides it in the tray. Exiting from the tray releases wake requests. Closing the window while idle exits the app.

## Lock screen and power (verify on the target device)

- [ ] Default policy: lock at the scheduled time. Unlocking within the window resumes the run; unlocking after it ends skips the run.
- [ ] Enable **Run after unlock, even past end time**. Lock at the scheduled time, then unlock after the end time; the pending run executes.
- [ ] Lock between modules. Later modules do not click the secure desktop. After unlock, the sequence resumes or cancels according to the selected policy.
- [ ] After starting the schedule, `powercfg /requests` shows the keep-awake request. Stopping or exiting releases it.
- [ ] Check standby, hibernation, wake timers, and lid closure for the device's hardware, power plan, and battery state.
- [ ] No clicks occur while Remote Desktop is disconnected; execution resumes after reconnection. Check enterprise lock policies and the UAC secure desktop separately.

A wake request does not guarantee that the hardware will wake. Do not mark device-specific behavior as passed without testing it on the device.
