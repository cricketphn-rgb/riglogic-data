# riglogic-data
hydro

## contours/v1 (2026-10-24)
Packed agency depth surveys for the app, one folder per state: `index.json` (every lake's bounding box, name, size) and one
`<key>.json.gz` per lake (rings at the agency's own levels, deep pocket, hump rings). Cut by `rigology-app/tools/pack_app_contours.py`,
indexed and copied here by `tools/pack_contours_index.py`. Read by the broker (`contour-pack.js`) over raw.githubusercontent.com.
`states.json` lists the states that are live; a state is added only after its licence is cleared and its datum line is written.
2026-10-24 14:25: michigan = all 1,587 lime lakes with compact depth grids (datum: below the lake surface at the MI DNR IFR survey).
2026-10-24 14:40: wisconsin = 230 lakes: 203 lime + 27 white (white = the measured-bottom tier, Decision 24A; added 17:40, Geneva among them), traced WDNR lake maps (written permission 10-04), with depth grids.
2026-10-24 15:10: greatlakes = the five Great Lakes (NOAA NCEI 3 arc-second, feet below Low Water Datum IGLD 1985; Erie includes Lake St. Clair), rings at 20 ft (Erie) / 100 ft steps, grids at ~360 m.
2026-10-24 16:05: umr = the 33 Upper Mississippi / Illinois River pools (USGS UMRR LTRM water-depth surface; feet below the water surface at the flow stated for each pool; grids resampled from UTM to lat/lon). texas = 97 TWDB volumetric surveys (feet below conservation pool).
2026-10-24 16:40: florida 59, ohio 131, pennsylvania 47, washington 219, indiana 104, iowa 109, massachusetts 253, oklahoma 90, kansas 66, connecticut 137, nebraska 109 (each state's agency lines; datum line in every file; probed with tools/probe_contours.mjs before the push).
2026-10-24 16:55: westvirginia 66, cookcounty 162, vermont 26, southdakota 1 (Pactola), northdakota 267.
2026-10-24 17:20: maine 965, montana 729, newhampshire 628. Not packed: minnesota (licence hold), alaska_adfg (agency polygons, no grid: packer path to add), usgs/west/california/caddo (no datum line yet).
2026-10-24 17:30: usgs = Lake Okeechobee FL (USGS DS 1031 soundings, below a 13.0 ft NAVD88 stage; marsh strip not surveyed). The other 37 USGS lakes wait for their own datum lines.
2026-10-24 14:55: illinois = all 39 lime lakes (Illinois DNR lake maps, public domain) with depth grids.
