# Single Studio demo

A working broadcast studio built on [Single Studio](https://github.com/FourCourtJester/Single-Studio),
and the thing to look at before starting one of your own.

Live: **https://fourcourtjester.github.io/Single-Studio-Demo/#/**

```bash
npm install
npm run dev
```

Any package manager works — this is an ordinary Vite app depending on two published
packages. npm is used here only because it comes with Node.

Open the printed URL to get the operator's board. The header menu lists every
graphic's browser-source URL with a copy button, which is what you paste into OBS.

## The show

It is modelled on a squad-based RTS broadcast, because that show happens to use
every component at once: two drafts, a map, an army composition, and all three
kinds of clock running together.

| Route                                                                                                      | What it is                           |
| ---------------------------------------------------------------------------------------------------------- | ------------------------------------ |
| `#/`                                                                                                       | The operator's board                 |
| `#/source/match`                                                                                           | The whole show in one browser source |
| `#/source/scoreboard`, `#/source/lower-third`, `#/source/standings`, `#/source/sponsor`, `#/source/ticker` | Single-purpose graphics              |
| `#/source/lower-thirds/guest`                                                                              | A nested key, grouped under a folder |

`#/source/match` is the one to look at first. Everything inside it is switched on
and off from the board, which is how a small production actually runs: one browser
source in OBS, not fifteen.

## The art is a placeholder

Every image under `public/factions`, `public/commanders`, `public/units` and
`public/maps` is generated — see `scripts/placeholders.mjs`. Nothing here is anyone's
intellectual property, and all of it is meant to be overwritten.

To use your own, drop files with the same names into the same folders. To change the
names, edit `src/roster.js` and regenerate:

```bash
node scripts/placeholders.mjs
```

Nothing else changes. The control writes a slug and the scene templates a file path
off it (`./units/:value:.svg`), so the roster is the only place the names live.

## Starting your own

Do not fork this. Use the
[template](https://github.com/FourCourtJester/Single-Studio-Template) — it is the
same framework with one graphic instead of seven, and a no-op mutation waiting to be
filled in.

- [Getting started](https://github.com/FourCourtJester/Single-Studio/blob/main/docs/getting-started.md)
- [Component reference](https://github.com/FourCourtJester/Single-Studio/blob/main/docs/api.md)
- [Your own data](https://github.com/FourCourtJester/Single-Studio/blob/main/docs/data.md)

## Tests

```bash
npm run build && npm run preview   # in one shell
npm run e2e                        # in another
```

`e2e/smoke.mjs` drives a real browser: SharedWorker startup, BroadcastChannel
fan-out between tabs, IndexedDB persistence, transition timing, and the clocks. It
runs against whatever version of the framework is installed, so a green run here is
a statement about the published packages rather than about a working copy.
