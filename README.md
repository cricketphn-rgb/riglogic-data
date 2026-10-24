# riglogic-data
hydro

## contours/v1 (2026-10-24)
Packed agency depth surveys for the app, one folder per state: `index.json` (every lake's bounding box, name, size) and one
`<key>.json.gz` per lake (rings at the agency's own levels, deep pocket, hump rings). Cut by `rigology-app/tools/pack_app_contours.py`,
indexed and copied here by `tools/pack_contours_index.py`. Read by the broker (`contour-pack.js`) over raw.githubusercontent.com.
`states.json` lists the states that are live; a state is added only after its licence is cleared and its datum line is written.
2026-10-24: michigan = the Torch Lake pilot (one lake).
