# Aurus plugins

The signed plugin catalogue that Aurus players read
(`https://raw.githubusercontent.com/Aurus-audio/plugins/main/catalog.txt`),
and the packages it points to.

Nothing here has to be trusted: `catalog.txt` is signed with the Aurus key
(`AURUSCAT1.` envelope), every `.aurusplugin` is signed with it too, and a
player also checks that each download hashes to what the catalogue says.
A catalogue with a lower sequence number than one a player has already seen
is refused. See `docs/plugin-catalog.md` in the player's repository.

| plugin | version | what |
|---|---|---|
| Lyrics | 1.0.1 | words to what is playing, line by line (engine, uses the internet — lrclib.net) |
| Listening Stats | 1.0.1 | top artists and tracks by day / week / month (engine, reads what you play, no network) |
| Track Info | 1.1.0 | format, rate, depth, file and signal path of the current track |

Publishing (on the machine with the signing key):

```sh
scripts/aurus-license.py plugin-pack examples/plugins/<id> --out <id>-<version>.aurusplugin
# keep the older files too — a device may hold a cached catalogue that names them;
# catalog-build offers the newest version of each plugin
scripts/aurus-license.py catalog-build . \
    --base-url https://raw.githubusercontent.com/Aurus-audio/plugins/main --out catalog.txt
git add -A && git commit && git push
```
