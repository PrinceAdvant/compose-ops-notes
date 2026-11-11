# Uptime Kuma alert fatigue: tuning retries, intervals and groups

Uptime Kuma is easy to install and easy to over-configure. After a month of false alarms most people mute it, which defeats the point.

## Settings that help

- **Retries.** Set 2 or 3 retries before a monitor is marked down. A single failed check is usually a network hiccup.
- **Interval.** 60 seconds is plenty for most web apps. 20 second checks on 30 monitors add noise and load.
- **Retry interval.** Shorter than the main interval, for example 20 seconds, so confirmation is quick.
- **Groups.** Put an app and its dependencies in a group so one outage sends one alert.
- **Keyword monitors.** Check for a word that only appears when the page rendered correctly, not just HTTP 200.
- **Maintenance windows.** Schedule them for planned deploys so expected restarts do not alert.

## Where to run it

Not on the same server it monitors. A tiny second VPS or a different region is enough.

Installation and persistence are covered in how to [self-host Uptime Kuma](https://peon.sh/blogs/self-host-uptime-kuma). Notes by a contributor to [Peon](https://peon.sh/), an open-source self-hosted deployment platform.
