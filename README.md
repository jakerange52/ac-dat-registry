# AC DAT Registry

- This is a community-maintained registry of custom DAT file sets required by certain Asheron's Call emulated servers.
- It is consumed by [ShadowLauncher](https://github.com/Elrek/ShadowLauncher) to automatically download and configure the correct DAT files when a player connects to a server that needs them.
- To add, update, or remove a DAT set, submit a pull request.

## Disclaimer

This project is for educational and non-commercial purposes only.

- Asheron's Call was a registered trademark of Turbine, Inc. and WB Games Inc which has since expired.
- ACResources is not associated or affiliated in any way with Turbine, Inc. or WB Games Inc.

## Template

- [Sample](https://raw.githubusercontent.com/acresources/serverslist/master/DatRegistry.xml)

## DatSet Template Fields

- `<DatSet id="">` — Stable, lowercase, hyphenated identifier. Never change this once published — it is used as the local cache folder name on player machines.
- `<DatSet name="">` — Human-readable display name shown in the launcher UI.
- `<DatSet version="">` — Semantic version (e.g. `1.0`). Bump this when files change so launchers know to re-download.
- `<Description>` — Brief description of what this DAT set is and which servers require it. (Optional)
- `<Servers>` — One or more `<Server name=""/>` entries listing server names (case-insensitive) that require this DAT set. The launcher uses this to auto-configure players when they add a matching server.
- `<Zip url="" sha256="" size="">` — Direct URL to a zip archive containing all DAT files. The launcher downloads and extracts this automatically. `sha256` and `size` are optional but recommended. Omit the element entirely if no zip is available.
- `<File name="" url="" sha256="" size="">` — Individual DAT file entry. Used as a fallback if no `<Zip>` url is provided, and to declare which files are expected. Files with an empty `url` must be placed manually by the player. `sha256` and `size` are optional.

## Known DAT Filenames

These are the filenames `acclient.exe` looks for in its working directory:

| File | Description |
|---|---|
| `client_portal.dat` | Primary asset database (models, textures, sounds, spells) |
| `client_cell_1.dat` | World geometry and landblock data |
| `client_local_English.dat` | Locale strings and UI data |
| `client_highres.dat` | High-resolution texture pack (not present in all installs) |
| `acclient.exe` | The game client binary (include if your server requires an older era client) |

## FAQ

#### Does the servers list (Servers.xml) need to change to support this?

No. The mapping between server names and DAT sets lives entirely in this file via `<Server name=""/>` entries. The `Servers.xml` file does not need any new fields.

#### When should I bump the version?

When the content of the DAT files changes — e.g. a server updates their custom assets. Players with a cached copy will be prompted to re-download.

#### Can a DAT set be used by multiple servers?

Yes. Add multiple `<Server name=""/>` entries inside the `<Servers>` block.

#### Can a zip contain extra files?

Yes. The launcher only extracts filenames it recognises from the `<File>` entries. Everything else in the zip is ignored.

#### Who can submit changes?

Anyone. Submit a pull request with your new or updated `<DatSet>` entry.

## Other Resources

- [ShadowLauncher](https://github.com/jakerange52/ShadowLauncher)
- [ACEmulator](https://github.com/ACEmulator/ACE)
- [GDLEnhanced](https://gitlab.com/Scribble/gdlenhanced)
- [AC Servers List](https://github.com/acresources/serverslist)
