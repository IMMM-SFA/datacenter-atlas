<script>
    import { base } from '$app/paths';
    import MapLibre from 'svelte-maplibre/MapLibre.svelte';
    import DeckGlLayer from 'svelte-maplibre/DeckGlLayer.svelte';
    import { GeoJsonLayer } from '@deck.gl/layers';
    import { MVTLayer, H3HexagonLayer } from '@deck.gl/geo-layers';
    import Icon from "@iconify/svelte";
    import Ack from '$lib/Ack.svelte';
    import Link from '$lib/Link.svelte';

    import About from '$lib/About.svelte';
    import Expando from '$lib/Expando.svelte';
    import Legend from '$lib/Legend.svelte';
    import PopRock from '$lib/PopRock.svelte';

    const projectedScenarios = [
         'low_growth', 'moderate_growth', 'high_growth', 'higher_growth',
    ];

    const projectedGravities = [
        0, 25, 50, 75, 100,
    ];

    const fiberColors = (d) => {
        const domain = [1, 2, 5, 10, 25];
        const colors = [
            [233, 7, 108,  64],
            [233, 7, 108,  84],
            [233, 7, 108, 104],
            [233, 7, 108, 124],
            [233, 7, 108, 144],
            [233, 7, 108, 164],
        ];
        const v = d.provider_count;
        let c = colors[colors.length - 1];
        domain.some((d, i) => {
            if (v < d) {
                c = colors[i];
                return true;
            }
            return false;
        });
        return c;
    };

    let showAck = $state(true);

    let aboutExpanded  = $state(false);
    let layersExpanded = $state(true);
    let getDataExpanded = $state(true);

    let existingDataCenterOn        = $state(true);
    let projectedDataCenterOn       = $state(true);
    let municipalWaterOn            = $state(true);
    let fiberOn                     = $state(true);
    let transmissionOn              = $state(true);

    let existingDataCenterLoaded    = $state(false);
    let projectedDataCenterLoaded   = $state(false);
    let municipalWaterLoaded        = $state(false);
    let fiberLoaded                 = $state(false);
    let transmissionLoaded          = $state(false);

    let projectedScenario           = $state(projectedScenarios[1]);
    let projectedGravity            = $state(projectedGravities[2]);

</script>

<div
    class="w-screen h-screen max-h-screen overflow-hidden relative"
>

    <div
        class="absolute top-0 left-0 overflow-auto max-h-screen py-1 md:py-2 pl-1 md:pl-2 pr-2 md:pr-3 w-80 md:w-[28rem] z-10"
    >
        <div
            class="bg-black/60 backdrop-blur-sm rounded shadow w-full pt-1 md:pt-2"
            style="box-shadow: 1px 1px 6px 0px #FFFFFF40;"
        >
            <div
                class="flex flex-row items-center justify-between px-2 md:px-4"
            >
                <h1
                    class="font-semibold text-base md:text-xl text-white"
                >
                    <a href="https://im3.pnnl.gov" target="_blank" rel="noreferrer" class="font-montserrat text-lg md:text-2xl mr-0.5 md:mr-1 text-sky-400">IM<sub>3</sub></a> Open Source Data Center Atlas
                </h1>
            </div>
            <div class="mt-1 md:mt-2 mb-2 md:mb-4 px-2 md:px-4">
                <p class="text-xs md:text-sm text-white leading-tight">
                    Explore current and future projections of data center locations and supporting infrastructure.
                </p>
            </div>
            <Expando label='Layers' bind:expanded={layersExpanded}>
                <Legend
                    bind:existingDataCenterOn
                    bind:projectedDataCenterOn
                    bind:projectedScenario
                    bind:projectedGravity
                    bind:municipalWaterOn
                    bind:fiberOn
                    bind:transmissionOn
                    {existingDataCenterLoaded}
                    {projectedDataCenterLoaded}
                    {projectedScenarios}
                    {projectedGravities}
                    {municipalWaterLoaded}
                    {fiberLoaded}
                    {transmissionLoaded}
                />
            </Expando>
            <Expando label='About' bind:expanded={aboutExpanded}>
                <About />
            </Expando>
            <Expando label='Get the data' bind:expanded={getDataExpanded}>
                <div
                    class="
                        flex flex-row items-center font-bold text-base text-gray-200 
                        px-4 py-2 uppercase w-full text-start
                    "
                >
                    <div class="flex-1 flex flex-row items-center justify-around text-xs md:text-sm pl-2">
                        <Link href=https://doi.org/10.57931/2550666>
                            <Icon class="inline-block mr-1" inline icon="carbon:data-center"></Icon>Existing
                        </Link>
                        <Link href=https://doi.org/10.57931/2571680>
                            <Icon class="inline-block mr-1" inline icon="ph:chart-line-up"></Icon>Projected
                        </Link>
                    </div>
                </div>
            </Expando>
        </div>
    </div>

    <div class="w-full h-full">
        <MapLibre
            style="https://basemaps.cartocdn.com/gl/dark-matter-gl-style/style.json"
            class="w-full h-full"
            maxBounds={[
                [-170, 15],
                [-40, 60]
            ]}
            dragRotate={false}
            pitchWithRotate={false}
            standardControls='bottom-right'
        >
            <DeckGlLayer
                id="transmission_lines"
                visible={transmissionOn}
                type={MVTLayer}
                data={`${base}/tiles/transmission/metadata.json`}
                getLineColor={[254,217,118]}
                getLineWidth={0.25}
                lineWidthUnits='pixels'
                tileSize={256}
                minZoom={0}
                maxZoom={8}
                maxzoom={10}
                extent={[-159.779336,13.447581,144.823499,65.017210]}
                parameters={{ depthTest: false }}
                onDataLoad={() => { transmissionLoaded = true }}
            >
                <PopRock />
            </DeckGlLayer>
            <DeckGlLayer
                id="transmission_lines"
                visible={transmissionOn}
                type={MVTLayer}
                data={`${base}/tiles/transmission/metadata.json`}
                getLineColor={[254,217,118]}
                getLineWidth={1}
                lineWidthUnits='pixels'
                tileSize={256}
                minZoom={0}
                maxZoom={8}
                minzoom={10}
                extent={[-159.779336,13.447581,144.823499,65.017210]}
                parameters={{ depthTest: false }}
                onDataLoad={() => { transmissionLoaded = true }}
                beforeLayerType="symbol"
                beforeId="data_center_points"
            >
                <PopRock />
            </DeckGlLayer>
            <DeckGlLayer
                id="fiber_providers"
                visible={fiberOn}
                stroked={false}
                filled={true}
                extruded={false}
                type={H3HexagonLayer}
                data={`${base}/fiber_providers_commercial_h3.json`}
                getLineColor={fiberColors}
                getFillColor={fiberColors}
                getLineWidth={1}
                lineWidthUnits='pixels'
                parameters={{ depthTest: false }}
                onDataLoad={() => { fiberLoaded = true }}
                
            >
                <PopRock />
            </DeckGlLayer>
            <DeckGlLayer
                id="water_providers"
                visible={municipalWaterOn}
                stroked={false}
                type={MVTLayer}
                data={`${base}/tiles/usgs_water_supply/metadata.json`}
                getFillColor={[0, 174, 239, 128]}
                tileSize={256}
                minZoom={0}
                maxZoom={11}
                extent={[-124.513131,24.544502,-66.980034,49.002403]}
                parameters={{ depthTest: false }}
                onDataLoad={() => { municipalWaterLoaded = true }}
            >
                <PopRock />
            </DeckGlLayer>
            {#if transmissionLoaded}
                <DeckGlLayer
                    id="data_center_points"
                    visible={existingDataCenterOn}
                    type={GeoJsonLayer}
                    data={`${base}/im3_datacenter_centroids.geojson`}
                    getLineColor={[3, 160, 139]}
                    getFillColor={[5, 230, 201]}
                    getLineWidth={1}
                    getPointRadius={4}
                    lineWidthUnits='pixels'
                    pointRadiusUnits='pixels'
                    maxzoom={11}
                    parameters={{ depthTest: false }}
                    onDataLoad={() => { existingDataCenterLoaded = true }}
                >
                    <PopRock />
                </DeckGlLayer>
                <DeckGlLayer
                    id="projected_data_center_points"
                    visible={projectedDataCenterOn}
                    type={GeoJsonLayer}
                    data={`${base}/projected/${projectedScenario}_${projectedGravity}_market_gravity_epsg4326_centroids.geojson`}
                    getLineColor={[140, 221, 53, 200]}
                    getFillColor={[140, 221, 53, 200]}
                    getLineWidth={1}
                    getPointRadius={4}
                    lineWidthUnits='pixels'
                    pointRadiusUnits='pixels'
                    maxzoom={11}
                    parameters={{ depthTest: false }}
                    onDataLoad={() => { projectedDataCenterLoaded = true }}
                >
                    <PopRock />
                </DeckGlLayer>
                <DeckGlLayer
                    id="data_center_footprints"
                    visible={existingDataCenterOn}
                    type={GeoJsonLayer}
                    data={`${base}/im3_datacenter_footprints.geojson`}
                    getLineColor={d => d?.properties?.type === 'campus' ? [209, 178, 0, 180] : [3, 160, 139]}
                    getFillColor={d => d?.properties?.type === 'campus' ? [255, 226, 63, 180] : [5, 230, 201]}
                    getPointRadius={4}
                    getLineWidth={1}
                    lineWidthUnits='pixels'
                    pointRadiusUnits='pixels'
                    minzoom={11}
                    parameters={{ depthTest: false }}
                >
                    <PopRock />
                </DeckGlLayer>
                <DeckGlLayer
                    id="projected_data_center_footprints"
                    visible={projectedDataCenterOn}
                    type={GeoJsonLayer}
                    data={`${base}/projected/${projectedScenario}_${projectedGravity}_market_gravity_epsg4326.geojson`}
                    getLineColor={[140, 221, 53, 200]}
                    getFillColor={[140, 221, 53, 200]}
                    getPointRadius={4}
                    getLineWidth={1}
                    lineWidthUnits='pixels'
                    pointRadiusUnits='pixels'
                    minzoom={11}
                    parameters={{ depthTest: false }}
                >
                    <PopRock />
                </DeckGlLayer>
            {/if}
        </MapLibre>
    </div>

    {#if showAck}
        <Ack
            bind:show={showAck}
        />
    {/if}

</div>
