# sts2-ios-launcher-public-mods

Mods that the STS2 Mobile iPhone app (sts2-ios-launcher) builds in. Its `./setup.sh` downloads these files and
checks each one against the SHA-256 pinned in the launcher, so a file that changes here is refused until the
launcher pins the new one. You do not need to download anything from here yourself.

## QuickMatch 0.3.0

Random co-op matchmaking for Slay the Spire 2: pick 2, 3 or 4 players and get grouped with other players who
are searching. Everyone in a match needs this version (0.3.0 players only match each other). Includes voice chat.

| File | SHA-256 |
| --- | --- |
| `QuickMatch/QuickMatch.dll` | `594f9385c1723982af8207e93e0af229a235d8698b8e29b7261d591332e35408` |
| `QuickMatch/QuickMatch.json` | `6042f9e77c6c3028f3da8c9770876d51043c6c50de87c519601a65673e24b62c` |

### Is it safe?

- **It sends no stats, analytics or tracking.** It finds matches through Steam lobbies, on your own Steam
  connection, and sends game moves only to the other players in your match.
- **No relay is included.** Without one, matches go over Steam lobby chat. A relay is chosen by whoever builds
  the iPhone app (`QUICKMATCH_RELAY=wss://<host> ./setup.sh --install`, or `.local/QuickMatchRelay.cfg` with
  `relay = https://<host>`). On the iPhone the app lets QuickMatch reach only that one host, only during a
  match, and never with your Steam sign-in. The relay sees your IP address, Steam ID, and the timing and size of
  the encrypted messages.
- **The microphone is used only for voice chat**, only while you have your mic turned on in a match.
- **You can check it.** QuickMatch's source is the sts2-quickmatch repository. Building it there with
  `dotnet build -c Release -p:ModsPath=` in `mod/QuickMatch` (with the .NET SDK its `global.json` pins) against
  Slay the Spire 2 v0.111.0 gives this exact DLL, byte for byte
  (a deterministic build with no local paths or git commit in it, so any clone gives the same bytes).

## On desktop

Copy the `QuickMatch` folder into the game's `mods` folder (on macOS inside the app bundle, at
`SlayTheSpire2.app/Contents/MacOS/mods`; on Windows, the `mods` folder of the game's install) and turn mods
on in the game. Voice chat and the relay also need the Quick Match Relay companion (in the source repository)
and a relay; without them, matches use Steam lobby chat.

## License

QuickMatch is under the MIT license (`LICENSE`). It includes Concentus, a C# port of the Opus codec, under its own
license (`licenses/Concentus-LICENSE.txt`).

Slay the Spire 2 is made by Mega Crit. These mods are not made or endorsed by Mega Crit or Valve.
