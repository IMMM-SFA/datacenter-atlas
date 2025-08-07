# IM3 Open Source Data Center Atlas

Explore current and future projections of data center locations and supporting infrastructure.

## Developing

Install dependencies with `npm install`.

Start a development server with: `npm run dev`

## Building

Create a production version of the app with: `npm run build`

Preview the production build with: `npm run preview`.

## Deploying

The app is deployed to GitHub Pages automatically on commits to the `main` branch.

## Data Layers

First download the various raw data layers:

Projected data centers: tbd (get from Kendall)

Existing data centers: https://data.msdlive.org/records/65g71-a4731

Fiber density: https://broadbandmap.fcc.gov/home

Municipal water service: https://doi.org/10.5066/P9I22Z24

Transmission lines: https://hifld-geoplatform.hub.arcgis.com/datasets/geoplatform::transmission-lines-1/about

Then use the `datacenters.ipynb` notebook to transform the data into the layers used by the app. Note that the transmission and water supply layers are further transformed into vector tiles using [tippecanoe](https://github.com/felt/tippecanoe). The commands to do this are provided in the notebook. But note the need to slightly alter the resulting `metadata.json` to properly define the tiles (look at this repository history to compare if you regenerate the tiles and need to see an example).
