# Help Needed !

See: https://github.com/espressif/arduino-esp32/discussions/10039

Add these in an existing project:
```
[env:pioarduino-esp32dev]
platform = https://github.com/pioarduino/platform-espressif32/releases/download/51.03.03/platform-espressif32.zip
board = esp32dev

[env:pioarduino-esp32-s2]
platform = https://github.com/pioarduino/platform-espressif32/releases/download/51.03.03/platform-espressif32.zip
board = esp32-s2-saola-1

[env:pioarduino-esp32-s3]
platform = https://github.com/pioarduino/platform-espressif32/releases/download/51.03.03/platform-espressif32.zip
board = esp32-s3-devkitc-1

[env:pioarduino-esp32-c3]
platform = https://github.com/pioarduino/platform-espressif32/releases/download/51.03.03/platform-espressif32.zip
board = esp32-c3-devkitc-02

[env:pioarduino-esp32-c6]
platform = https://github.com/pioarduino/platform-espressif32/releases/download/51.03.03/platform-espressif32.zip
board = esp32-c6-devkitc-1
```

Then run:

```bash
# cleanup existing packages
rm ~/.platformio/packages
# build
for e in `pio project config --json-output | jq -cr '.[][0] | select(startswith("env:pioarduino-")) | .[4:]'`; do pio run -e $e; done;
# compress
cd ~/.platformio/packages
ls | grep -v framework | grep -v zip | xargs -n1 -I {} zip -s 100m -r {}.zip {}
# double check your architecture:
uname -a
```

Fork this repo.

Then move all the generated zip and zxx files inside your fork, in the right folder.
Push, PR, :+1:

As an example, this accounts for about 750Mb for macos_arm64.
