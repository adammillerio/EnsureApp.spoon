# EnsureApp.spoon
Hammerspoon - Utility for providing fast and guaranteed access to app windows during macros.

Example application with usage: [MenuBarApps.spoon](https://github.com/adammillerio/MenuBarApps.spoon)

# Installation

This Spoon depends on another Spoon being installed and loaded, [WindowCache](https://github.com/adammillerio/WindowCache.spoon).

## Automated

MenuBarApps can be automatically installed from my [Spoon Repository](https://github.com/adammillerio/Spoons) via [SpoonInstall](https://www.hammerspoon.org/Spoons/SpoonInstall.html). See the repository README or the SpoonInstall docs for more information.

Example `init.lua` configuration which configures `SpoonInstall` and uses it to install and start EnsureApp:

```lua
hs.loadSpoon("SpoonInstall")

spoon.SpoonInstall.repos.adammillerio = {
    url = "https://github.com/adammillerio/Spoons",
    desc = "adammillerio Personal Spoon repository",
    branch = "main"
}

spoon.SpoonInstall:andUse("WindowCache", {repo = "adammillerio", start = true})

spoon.SpoonInstall:andUse("EnsureApp", {
    repo = "adammillerio",
    start = true,
    config = {
        apps = {
            ["Discord"] = {app = "Discord", action = "maximize"},
            ["Arc"] = {
                app = "Arc",
                action = "maximize",
                spacePrecedence = true,
                newWindowConfig = {
                    menuSection = "File",
                    menuItem = "New Window"
                }
            },
            ["Plexamp"] = {app = "Plexamp", action = "move"},
        }
    }
})
```

Now, when invoked via `EnsureApp:ensureApp()` (`ie EnsureApp:ensureApp("Discord")`), the plugin will look up the app configuration and perform the following steps:
* Discord - Move global Discord window to the current space and maximize if needed.
* Arc - Move or create a space local Arc window in the current space and maximize if needed.
* Plexamp - Move a global Plexamp window to the current space under a certain frameA.
    * Mostly used for [MenuBarApps.spoon](https://github.com/adammillerio/MenuBarApps.spoon)

Refer to Usage section for a link to the hosted documentation, which has more information on app configuration.

## Manual

Download the latest WindowCache release from [here.](https://github.com/adammillerio/Spoons/raw/main/Spoons/MenuBarApps.spoon.zip)

Download the latest EnsureApp release from [here.](https://github.com/adammillerio/Spoons/raw/main/Spoons/EnsureApp.spoon.zip)

Unzip both and either double click to load the Spoons or place the contents manually in `~/.hammerspoon/Spoons`

Then load the Spoons in `~/.hammerspoon/init.lua`:

```lua
hs.loadSpoon("WindowCache")

hs.spoons.use("WindowCache", {start = true})

hs.loadSpoon("EnsureApp")

hs.spoons.use("EnsureApp", {
    config = {
        apps = {
            ["Plexamp"] = {app = "Plexamp", action = "move"},
            ["Discord"] = {app = "Discord", action = "maximize"},
            ["Reminders"] = {app = "Reminders", action = "maximize"},
            ["Settings"] = {app = "Settings", action = "move"},
            ["Arc"] = {
                app = "Arc",
                action = "maximize",
                spacePrecedence = true,
                newWindowConfig = {
                    menuSection = "File",
                    menuItem = "New Window"
                }
            }
        }
    },
    start = true
})
```

# Usage

Refer to the [hosted documentation](https://adammiller.io/EnsureApp/EnsureApp.html) additional for information on usage.
