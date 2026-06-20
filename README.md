# Battery Monitor (FullBat.vbs)

A tiny Windows script that watches your laptop's battery and pops up a notification when it's charging and crosses **95%**. Useful if you want a reminder to unplug and protect battery health.

No installation needed — it uses a built-in Windows scripting engine (VBScript) and Windows Management Instrumentation (WMI) to read battery data.

---

## 1. What you need

- A **Windows laptop** (this won't work on desktops without a battery, or on Mac/Linux)
- That's it. VBScript comes pre-installed on every Windows version (7, 8, 10, 11)

---

## 2. Get the script onto your PC

1. Copy the entire code block you have (the one starting with `set oLocator = ...`)
2. Open **Notepad** (search "Notepad" in the Start menu)
3. Paste the code into Notepad
4. Click **File → Save As**
5. In the Save dialog:
   - Set **"Save as type"** to **All Files**
   - Set the filename to: `FullBat.vbs`
   - Choose a folder you'll remember, e.g. `C:\Scripts\`
6. Click **Save**

> ⚠️ The `.vbs` extension is critical. If you save it as `FullBat.vbs.txt`, Windows will treat it as a text file, not a script.

---

## 3. Run it for the first time

1. Go to the folder where you saved `FullBat.vbs`
2. **Double-click** the file
3. Nothing visible will happen — that's normal. The script runs silently in the background
4. Plug in your charger and wait until the battery passes 95% — a popup titled **"Battery monitor"** should appear

To confirm it's actually running:
- Open **Task Manager** (`Ctrl + Shift + Esc`)
- Go to the **Details** tab
- Look for a process called **`wscript.exe`** — if it's there, the script is alive

To **stop** it: find `wscript.exe` in Task Manager, click it, and select **End Task**.

---

## 4. Make it run automatically (optional but recommended)

So you don't have to double-click it every time you log in:

1. Press `Win + R`, type `shell:startup`, hit Enter — this opens your Startup folder
2. Right-click inside that folder → **New → Shortcut**
3. Browse to your `FullBat.vbs` file and select it
4. Click **Next**, then **Finish**

Now the script will start automatically every time you log into Windows.

---

## 5. How it works (in plain English)

- The script asks Windows (via WMI) two things, repeatedly: *"What's the battery's full capacity?"* and *"What's the current remaining capacity, and is it charging?"*
- It calculates the percentage: `(remaining ÷ full) × 100`
- Every **30 seconds**, it checks: *is the laptop charging AND is the battery above 95%?*
- If yes, it shows a popup message box

---

## 6. Troubleshooting

| Problem | Fix |
|---|---|
| Nothing happens at all | Make sure the file extension is really `.vbs`, not `.txt` (enable "File name extensions" in File Explorer's View tab to check) |
| "Windows Script Host access is disabled" error | Your IT admin or antivirus may have disabled WSH. You'll need their help or admin rights to re-enable it |
| Popup never appears | Double-check you're actually charging and the battery is above 95% — it only triggers in that combination |
| Script won't close | Use Task Manager → Details tab → end the `wscript.exe` process |
| Want to change the threshold | Open the file in Notepad, find the line with `iPercent > 95`, and change `95` to whatever percentage you want |
| Want a faster/slower check interval | Find `wscript.sleep 30000` — this is in milliseconds (30000 = 30 seconds). Change the number to adjust how often it checks |

---

## 7. Uninstall / Remove

1. Delete `FullBat.vbs` from wherever you saved it
2. If you added it to Startup, also delete the shortcut from the Startup folder (`Win + R` → `shell:startup`)
3. End the `wscript.exe` process in Task Manager if it's still running

---

## Notes

- This script only works while you're logged into Windows — it stops if you log off, restart, or shut down (unless re-added to Startup).
- It uses no internet connection and collects no data — everything stays local to your PC.

---

## Author

**Rajesh Vatluri**
GitHub: [@i-vrajesh](https://github.com/i-vrajesh)

---

## License

This project is intended for **educational and learning** purposes only.
