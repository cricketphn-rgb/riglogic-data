# fish/ — which fish each lake offers (read by the app's server, `rigology-app/fish-ledger.js`, as `/api/fish`)

Owner 2026-11-13: fish lists come FROM THE SERVER, so a lake's list gets better with a data push here: no app build, no store wait.
Built by `rigology-app/tools/species/build_fish_data.py`. Do not edit by hand. Nothing else in this repository is touched by the fish work.

## v1/
- `meta.json` what is here, when it was built, which fish the USGS range table covers.
- `lakes.json.gz` every mapped lake: key, box, the 8-digit watersheds its box touches, flags (1 = has a ledger, 2 = found by key only), name.
- `lake/<key>.json` THE LEDGER of one lake: per fish, every piece of evidence held, each with its kind and source.
  Kinds: `agency` (an agency's list for this lake: `p` 1 present / 0 absent), and, as they are harvested, `stock`, `park`, `site`, `wiki` (these only add).
  **Only an agency list takes a fish off. Present on any agency source = present.** A list that marks no fish present is not a list and is not here.
- `huc/<huc8>.json` one watershed: `r` the USGS native-range origin per fish (N native / I introduced), `s` USGS NAS record counts per fish
  `[records, living, last year, last living year]`, `p` the living records `[lat, lon, year, stocked, real point, locality]`.

## Sources
Agency lake lists (Wisconsin DNR survey maps and current lake pages; AZGFD; NPS; NDOW; CDFW; state and federal Great Lakes lists);
USGS "Native ranges of freshwater fishes of North America" (Daniel and Neilson, doi 10.5066/P9C4N10N, ver. 2.0, 2022);
USGS Nonindigenous Aquatic Species database; USGS Watershed Boundary Dataset.

## The rules are not here
They are in `fish-ledger.js` on the server and are held to the scorecard (`rigology-app/tools/species/score_table.py`).
