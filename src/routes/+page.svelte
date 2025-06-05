<script>
    import { base } from '$app/paths';
    import MapLibre from 'svelte-maplibre/MapLibre.svelte';
    import DeckGlLayer from 'svelte-maplibre/DeckGlLayer.svelte';
    import { GeoJsonLayer } from '@deck.gl/layers';
    import { MVTLayer, H3HexagonLayer } from '@deck.gl/geo-layers';
    import Icon from "@iconify/svelte";
    import Ack from '$lib/Ack.svelte';

    import About from '$lib/About.svelte';
    import Expando from '$lib/Expando.svelte';
    import Legend from '$lib/Legend.svelte';
    import PopRock from '$lib/PopRock.svelte';

    const fiberColors = (d) => {
        const domain = [1, 2, 5, 10, 25];
        const colors = [
            [255, 198, 196, 64],
            [244, 163, 168, 64],
            [227, 129, 145, 64],
            [204,  96, 125, 64],
            [173,  70, 108, 64],
            [139,  48,  88, 64],
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

    let existingDataCenterOn        = $state(true);
    let projectedDataCenterOn       = false;
    let municipalWaterOn            = $state(true);
    let fiberOn                     = $state(true);
    let transmissionOn              = $state(true);

    let existingDataCenterLoaded    = $state(false);
    let municipalWaterLoaded        = $state(false);
    let fiberLoaded                 = $state(false);
    let transmissionLoaded          = $state(false);

</script>

<div
    class="w-screen h-screen max-h-screen overflow-hidden relative"
>

    <div
        class="absolute top-0 left-0 overflow-auto max-h-screen py-2 pl-2 pr-3 w-[31rem] z-10"
    >
        <div
            class="bg-white rounded shadow w-full pt-2 border border-gray-200"
        >
            <div
                class="flex flex-row items-center justify-between px-4"
            >
                <h1
                    class="font-semibold text-xl text-black"
                >
                    <span class="font-montserrat text-2xl mr-1">IM<sub>3</sub></span> Open Source Data Center Atlas
                </h1>
            </div>
            <div class="mt-2 mb-4 px-4">
                <span class="text-base text-black">
                    Explore data center locations and supporting infrastructure.
                </span>
            </div>
            <Expando label='Layers' bind:expanded={layersExpanded}>
                <Legend
                    bind:existingDataCenterOn
                    {projectedDataCenterOn}
                    bind:municipalWaterOn
                    bind:fiberOn
                    bind:transmissionOn
                    {existingDataCenterLoaded}
                    {municipalWaterLoaded}
                    {fiberLoaded}
                    {transmissionLoaded}
                />
            </Expando>
            <Expando label='About' bind:expanded={aboutExpanded}>
                <About />
            </Expando>
            <Expando downloado />
        </div>
    </div>

    <div class="w-full h-full">
        <MapLibre
            style="https://basemaps.cartocdn.com/gl/positron-gl-style/style.json"
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
                getLineWidth={1}
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
                getLineWidth={2}
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
                getFillColor={[44,127,184,64]}
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
                getLineColor={[63,0,125]}
                getFillColor={[84,39,143]}
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
            {/if}
            <DeckGlLayer
                id="data_center_footprints"
                visible={existingDataCenterOn}
                type={GeoJsonLayer}
                data={`${base}/im3_datacenter_footprints.geojson`}
                getLineColor={d => d?.properties?.type === 'campus' ? [35,132,67] : [63,0,125]}
                getFillColor={d => d?.properties?.type === 'campus' ? [65,171,93,128] : [84,39,143]}
                getPointRadius={4}
                getLineWidth={1}
                lineWidthUnits='pixels'
                pointRadiusUnits='pixels'
                minzoom={11}
                parameters={{ depthTest: false }}
            >
                <PopRock />
            </DeckGlLayer>
        </MapLibre>
    </div>

    {#if showAck}
        <Ack
            bind:show={showAck}
        />
    {/if}

</div>
