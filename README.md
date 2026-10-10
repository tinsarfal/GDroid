# GDroid

GDroid runs Garry's Mod natively on Android phones and tablets, with touch
controls. Download the APKs from the [Releases](../../releases) page.

Join our community on [Discord](https://discord.gg/hy2Zpm8XHn) for support and
discussion.

The APK does not include the retail game files. You need your own Steam copy of
Garry's Mod and its game content.

## Requirements

- Garry's Mod on Steam.
- Enough free storage for the APK, the game files, and your addons (about 7GB).

## Install or update

Download an APK from the [latest release](../../releases/latest):

| APK | Device |
| --- | --- |
| `GDroid-<version>.apk` | ARM64 (`arm64-v8a`), for most modern phones and tablets |
| `GDroid-<version>-armv7.apk` | 32-bit ARM (`armeabi-v7a`) devices |

Open the APK on your device and allow installation from the browser or file
manager when Android asks. You can also install it with adb:

```sh
adb install -r GDroid-<version>.apk
```

For a 32-bit ARM device, use the `-armv7.apk` file instead.

Install updates over the existing app so Android keeps your saves and settings.
Before updating, you can export your saves with
**Settings & tools → Back up saves**.

Open GDroid and grant the requested file access so it can read and write game
content in shared storage.

### Update from the launcher

The updater is under **Settings & tools → Updates**. When public release access
is available, select **Check now**. The launcher finds the latest stable release
and downloads the APK matching your installed ARM64 or ARMv7 version. Downloads
can be paused and resumed.

Select **Install update**, allow installs from GDroid in Android settings if
asked, then return and select **Install update** again. Confirm Android's
installation prompt. Quit the game and finish content imports or Steam downloads
before installing. Updating in place keeps your saves, settings, and game files.

Automatic checks are off by default. Enable **Check for updates automatically**
to check at most once a day when the launcher opens. Downloads and installation
still start only when you choose them. The updater checks the download checksum,
app identity, signing certificate, and Android build number before installation.

## Add the game files

Choose one of the following methods.

### Download directly from Steam

1. Open **Download from Steam** in the GDroid launcher.
2. Enter your Steam login, select **Garry's Mod**, and choose your language.
3. Select **Download selected game** and complete Steam Guard if requested.
4. Wait for installation to finish, then return to the launcher.

Downloads can be paused and resumed from the same screen. For multiplayer,
enable **Remember Steam sign-in on this device**, use **Sign in for multiplayer**,
and wait for the saved sign-in confirmation. Signing in alone does not download
the game.

### Use an existing Steam installation

In Steam on your computer, open **Garry's Mod → Manage → Browse local files**.
The installation contains three folders you need:

- `garrysmod`
- `sourceengine`
- `platform`

Transfer those folders to your Android device with USB file transfer or another
file-transfer tool. In GDroid, select **Import game files** and choose their
parent folder. Local files are moved into shared storage when possible; the
importer copies them when moving is unavailable. Transfer a copy first if you
want to keep the originals in their current location.

Alternatively, select **Play from a folder** to use an accessible existing
installation without importing it. Choose the parent folder containing the
three game folders. This also works with supported SD card and USB storage.

### Copy the files into shared storage yourself

Copy the three folders to `/sdcard/srceng/`. The result should look like this:

```text
/sdcard/srceng/garrysmod/garrysmod_dir.vpk
/sdcard/srceng/garrysmod/gameinfo.txt
/sdcard/srceng/sourceengine/hl2_misc_dir.vpk
/sdcard/srceng/sourceengine/hl2_textures_dir.vpk
/sdcard/srceng/platform/
```

Keep the complete folders, including every numbered VPK part beside its
`*_dir.vpk` file. Copying just the directory VPK is not enough. PC `bin/` files
are not used by GDroid.

With adb, for example:

```sh
adb shell mkdir -p /sdcard/srceng
adb push "/path/to/GarrysMod/garrysmod" /sdcard/srceng/
adb push "/path/to/GarrysMod/sourceengine" /sdcard/srceng/
adb push "/path/to/GarrysMod/platform" /sdcard/srceng/
```

If complete Half-Life 2 packs are already installed in `/sdcard/srceng/hl2/`,
GDroid can reuse them when the matching packs are absent from `sourceengine/`.

## Play and controls

Wait for the launcher's content check to report ready, then select **Play**.
By default this opens Garry's Mod's main menu. **Play a map…** starts a map
directly; **Settings & tools → Start at** changes the default behavior.

- Drag on the left side of the screen to move and on the right side to look.
- Use the on-screen buttons for the spawn menu, context menu, weapons, jumping,
  crouching, and other actions.
- In menus, tap to select, drag to move controls, or hold an element for about
  half a second to right-click it.
- Use the gear button to edit the touch layout.
  **Settings & tools → Custom buttons** adds keys needed by addons.
- Bluetooth controllers, keyboards, and mice are also supported.

## Addons

Use **Download from Steam** to install a Workshop item or collection by its URL
or ID. Enable or disable installed items in **Mod manager**, then use
**Play Workshop map…** for maps supplied by enabled addons.

You can also place local addon folders or `.gma` files in
`/sdcard/srceng/garrysmod/addons/`. Addons requiring another game's assets need
that content too. PC-only native binary modules need an Android-compatible
version.

## Credits

The engine is based on nillerusr's Android Source work and the touch controls were
provided by IzuIzu.
