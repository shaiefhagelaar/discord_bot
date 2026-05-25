# Installing python 3 on Windows 11

# Setup Guide (Windows)

Follow these steps in order to get a working Python environment and IDE on Windows. The instructions use the **Python Install Manager**, which is the modern tool recommended by the CPython team for installing and managing Python on Windows.

> **Note:** These steps target Windows 10 or newer. Python 3.14+ no longer supports older versions of Windows.

---

## 1. Install the Python Install Manager (from the Microsoft Store)

Install the **Python Install Manager** from the Microsoft Store:

👉 [Python Install Manager — Microsoft Store](https://apps.microsoft.com/detail/9NQ7512CXL7T)

1. Open the link above (or search for *"Python Install Manager"* in the Microsoft Store app).
2. Click **Install**.
3. Wait for the install to finish.

> ⚠️ **Install it from the Store, not via PowerShell.**
> The Store package and the `python.org` MSIX package are subtly different and **cannot be installed at the same time**. Installing the manager manually through PowerShell (e.g. `Add-AppxPackage`) can lead to conflicting installs and broken `python` / `py` commands. The Store install avoids these issues.

### Verify the install

Open a **new** terminal (PowerShell or Command Prompt) and confirm the commands are available:

```powershell
py --version
pymanager --version
```

If `py` reports a *"command not found"* error, open **Start → "Manage app execution aliases"** and make sure the **Python (default)** aliases are enabled. Toggling them off and on again refreshes the commands.

---

## 2. Configure the Python installation with the Install Manager

The Install Manager doesn't ship a Python runtime by itself — you install the version(s) you need with it.

### See what's available

```powershell
py list --online
```

### Install a Python runtime

Install a recent stable release (replace `3.12` with the version you want):

```powershell
py install 3.12
```

> 💡 This project requires **Python 3.5.3 or higher**. A current stable release such as 3.12 is recommended.

### Check what's installed and which is the default

```powershell
py list
```

The default runtime is the one launched when you run `python` or `py` with no version flag. To launch a specific version explicitly:

```powershell
py -V:3.12
```

### (Recommended) Use a virtual environment per project

Keeping dependencies isolated per project is the recommended workflow:

```powershell
# From your project's working directory
py -m venv .venv

# Activate it
.venv\Scripts\activate
```

Once activated, install packages as usual. For example, to install the Discord library on Windows:

```powershell
py -3 -m pip install -U discord.py
```

---

## 3. Install the JetBrains PyCharm IDE

1. Go to the official download page: 👉 [JetBrains PyCharm](https://www.jetbrains.com/pycharm/download/)
2. Choose an edition:
   - **PyCharm Community Edition** — free and open source, sufficient for most Python work.
   - **PyCharm Professional** — paid, adds web/scientific tooling (free for students via the [JetBrains student license](https://www.jetbrains.com/community/education/)).
3. Run the installer and follow the prompts. The defaults are fine for most users; optionally enable the **"Add bin folder to the PATH"** and **".py" file association** checkboxes during setup.
4. Launch PyCharm and **open your project folder**.

### Point PyCharm at your Python interpreter

So PyCharm uses the runtime you installed via the Install Manager:

1. Go to **File → Settings → Project: \<name\> → Python Interpreter**.
2. Click **Add Interpreter → Add Local Interpreter**.
3. Either:
   - Select **Existing** and browse to the virtual environment's `python.exe` (e.g. `.venv\Scripts\python.exe`), **or**
   - Choose to create a new **Virtualenv** environment and let PyCharm point its *base interpreter* at the runtime installed by the Python Install Manager.
4. Apply the changes. PyCharm will index the interpreter and its packages.

---

## Troubleshooting

| Symptom | Fix |
| --- | --- |
| `python` / `py` not recognized | Open **Start → "Manage app execution aliases"** and enable the **Python (default)** aliases. Toggle off/on to refresh. |
| `py` gives a *"can't open file"* error | A legacy Python launcher may be taking priority. Uninstall *"Python launcher"* via **Start → "Installed apps"**. |
| `pip` command not found | Activate your virtual environment first (`.venv\Scripts\activate`), or use `py -m pip ...`. |
| `python` and `py` launch different runtimes | In **Installed apps**, remove or modify other Python installs that modified `PATH`. |

---

## References

- [Using Python on Windows — Python docs](https://docs.python.org/3/using/windows.html)
- [discord.py — Prerequisites](https://discordpy-redfork.readthedocs.io/en/latest/intro.html#prerequisites)
- [Python Install Manager — Microsoft Store](https://apps.microsoft.com/detail/9NQ7512CXL7T)
- [JetBrains PyCharm](https://www.jetbrains.com/pycharm/download/)
