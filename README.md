# 🤣 punput_shaping

Open-API powered comedy for your printer — now shaping for maximum comedic resonance.

**Punput Shaping periodically fetches jokes from an API and sends them to your Klipper console.**

[View example output](example.png)

> ⚠️ **Requires** [Kalico](https://docs.kalico.gg/G-Code_Shell_Command.html?h=gcode_shell_command#passing-parameters) or Klipper with [`gcode_shell_command`](https://github.com/dw-0/kiauh/blob/master/docs/gcode_shell_command.md) extension installed.

---

## 📦 Installation

- Clone the repository into your Klipper config folder:

```bash
git clone https://github.com/IdleStep/punput_shaping.git ~/printer_data/config/punput_shaping
```

- Add this line to your `printer.cfg` to include the repo’s macros and configs:

```ini
[include punput_shaping/punput_shaper.cfg]
```

- **(Optional)** Add a console filter to Mainsail and hide command logs:

  - Navigate to **Settings → Console → Filters → Add Filter**
  - **Name**: `PunputShaper`
  - **Regex**: `.*Command \{punput.*\}.*`


- Restart Klipper.

---

### ⚙️ Configuration

To reconfigure settings, copy this macro into your `printer.cfg`:

``` ini
[gcode_macro PunputShaping]
variable_api: "local"                                            # API options: icanhazdadjoke, official, norris, jokeapi, local
variable_punputshaping_loop_duration: 900                        # 15 minutes default
variable_punputshaping_loop_drift: 30                            # 30 seconds default
variable_only_while_printing: True                               # Execute only during state of Printing
variable_start_at_boot: True                                     # Begin punput shaping at print start
```

| Variable | Purpose | Default | Notes |
| --- | --- | --- | --- |
| `variable_api` | Selects joke source from supported APIs | `local` | Options: icanhazdadjoke, official, norris, jokeapi, local |
| `variable_punputshaping_loop_duration` | Time between jokes (seconds) | `900` | 900 = every 15 minutes <br> ⚠️ **Be cautious of overusing Open API calls!** |
| `variable_punputshaping_loop_drift` | Random timing variation (± seconds) | `30` | Prevents perfectly fixed intervals |
| `variable_only_while_printing` | Runs only during active prints | `True` | Disabled when printer is idle |
| `variable_start_at_boot` | Starts loop automatically | `True` | Otherwise execute `PunputShaping` manually or from another macro |




---

## 💡 Tips

### Configure Moonraker

Append the following to your moonraker.conf to enable updates:

```ini
[update_manager punput_shaping]
type: git_repo
origin: https://github.com/IdleStep/punput_shaping.git
path: ~/printer_data/config/punput_shaping
primary_branch: main
is_system_service: False
managed_services: klipper
```

### 🛠️ Missing Python Library?

You may be missing a required library. Install it with:

```bash
sudo apt install python3-requests  # Debian/Ubuntu-based distros
```
