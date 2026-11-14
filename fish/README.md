# fish/ — which fish each lake offers (read by the app's server, `rigology-app/fish-ledger.js`, as `/api/fish`)

Owner 2026-11-13: fish lists come FROM THE SERVER, so a lake's list gets better with a data push here: no app build, no store wait.
Built by `rigology-app/tools/species/build_fish_data.py`. Do not edit by hand. Nothing else in this repository is touched by the fish work.

## v1/
- `meta.json` what is here, when it was built, which fish the USGS range table covers.
- `lakes.json.gz` every mapped lake: key, box, the 8-digit watersheds its box touches, flags (1 = has a ledger, 2 = found by key only), name.
- `lake/<key>.json` THE LEDGER of one lake: per fish, every piece of evidence held, each with its kind and source.
  Kinds: `agency` (an agency's LIST for this lake: `p` 1 present / 0 absent), and the harvested kinds, which only add:
  `park` and `stock` (strong: the fish is on the lake; `stock` alone is shown as STOCKED), `report`, `site`, `wiki` (weak: offered
  where the engine's own test of the water allows). Markers: `ag: 1` the source is an agency page (a page that names some of a
  lake's fish is not a list of the lake: it is written `park`, and takes nothing off); `stk: 1` the source's word was "stocked";
  `y` a year. A cold-water fish known only by stocking is `report` (no stocking season is held: no trout on a hot lake in July).
  `cover` (on the ledger, 11-14): how far the lake's own sources cover it: `survey` (the agency's inventory or survey catches),
  `searched` (an agency page naming four or more fish AND a search of other sources), `page` (the page alone). The server's rule
  2b reads it: a GAME fish (walleye, pike, smallmouth, trout) no piece names is not offered under `survey` / `searched`, held back
  under `page`, and held back, never off, where a living record of the last fifteen years puts it on the water.
  **THE STACK (11-14, the server's rule 2c, build 87b):** a lake's records stack in its file and the newer weighs more. A piece
  may carry `y` (the last year the record saw the fish: a strong piece more than 25 years old is OLD: alone it holds a game fish
  back and keeps an everyday fish on; anything newer or undated beats it), `y0` (first year), `n` (how many surveys of the lake
  found it), `sy` (the last year a dated survey saw a fish the source's standing list also names). The ledger may carry `sv`
  (what was surveyed: per source and method the count and years) and `coverBy` (the cover fish by fish: a source's silence takes
  off only the fish its own test passes for). `scorecard.json` beside `meta.json`: every source's test and what the server
  states per state, written by `rigology-app/tools/species/scorecard.py` on every build.
  **Only an agency list takes a fish off. Present on any agency source = present.** A list that marks no fish present is not a list and is not here.
- `huc/<huc8>.json` one watershed: `r` the USGS native-range origin per fish (N native / I introduced), `s` USGS NAS record counts per fish
  `[records, living, last year, last living year]`, `p` the living records `[lat, lon, year, stocked, real point, locality]`.

## Sources
Agency lake lists (Wisconsin DNR survey maps and current lake pages; AZGFD; NPS; NDOW; CDFW; state and federal Great Lakes lists);
harvested pages per lake (11-14: 121 big-name lakes; agency, park, stocking, Wikipedia and site pages, each with its address in
`rigology-app/research/harvest/`);
**Ontario Ministry of Natural Resources, Aquatic Resource Area fish lists per lake** (11-14: 2,441 of our Ontario lakes; source `ontario.ca`;
read from the province's open data, layer LIO_Open07 / 2, by `rigology-app/tools/species/ontario_to_evidence.py`). **Contains information
licensed under the Open Government Licence - Ontario.** It is NOT a lake's whole list (checked against the province's own angler
surveys: a fish anglers report is missing from it 15 times in 100; 5 in 100 on lists of 13 or more fish): what it names is asserted
(`park` + `ag: 1`), its silence takes nothing off, and only a list of 13 or more fish carries `cover: page` (567 lakes: a game fish it
does not name is held back). The layer's SURVEY POINTS (LIO_Open07 / 0) are read too: a lake the province netted (Broad-scale
Monitoring) in two or more years carries `cover: searched` (139 lakes: a game fish neither the list nor any survey names is not
offered; against the anglers' reports 0 of 264 such verdicts were wrong), netted in one year `cover: page` (0.7% wrong: held back);
**North Dakota Game and Fish Department, Fishing Waters service (ND GIS Hub)** (11-14: 269 lakes; source `gf.nd.gov`; the department's
sport-fish list, its netting catches 2015-2025 and its stocking 2016-2026, read together by `northdakota_to_evidence.py`): what they
name is asserted; on the 222 lakes netted in five or more years `cover: searched` (a GAME fish none of the three names is not offered:
checked on a hold-out, about 0.5 in 100 such removals is a fish the nets later brought up); everyday fish are never taken off; lakes
netted less carry `cover: page`;
**Wisconsin DNR public map services** (11-14: 454 lakes; source `dnr.wisconsin.gov`; walleye, musky and sturgeon waters, annual stocking
2010-2026, by `wisconsin_layers_to_evidence.py`): these only add (a stocking of the last ten years or of three or more years is a
strong add; an older one-off is `report`; stocked trout are strong only where the state's own lake class is cold water);
USGS "Native ranges of freshwater fishes of North America" (Daniel and Neilson, doi 10.5066/P9C4N10N, ver. 2.0, 2022);
USGS Nonindigenous Aquatic Species database; USGS Watershed Boundary Dataset.

## The rules are not here
They are in `fish-ledger.js` on the server and are held to the scorecard (`rigology-app/tools/species/score_table.py`).
