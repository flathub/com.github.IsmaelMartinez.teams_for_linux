# Teams for Linux Flatpak packaging

This repository holds the Flathub packaging for [Teams for Linux](https://github.com/IsmaelMartinez/teams-for-linux). It repacks the deb that upstream publishes on each release, so the application code is identical to the other Linux packages.

Issues here are only for the build environment, meaning the manifest, the sandbox permissions (finish-args), the base runtime and anything else specific to the Flatpak build. Anything about the application itself, such as sign in, calls, notifications, crashes or feature requests, belongs in the [upstream tracker](https://github.com/IsmaelMartinez/teams-for-linux/issues). If in doubt, open it upstream.

Version updates are automated. A bot opens a pull request for every upstream release and the Flathub buildbot builds it. Every pull request gets an installable test bundle, so testing those bundles is the most useful way to help.
