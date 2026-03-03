<script>
	import { base } from '$app/paths';
	import MapLibre from 'svelte-maplibre/MapLibre.svelte';
	import DeckGlLayer from 'svelte-maplibre/DeckGlLayer.svelte';
	import { GeoJsonLayer } from '@deck.gl/layers';
	import { MVTLayer, H3HexagonLayer } from '@deck.gl/geo-layers';
	import Icon from '@iconify/svelte';
	import Ack from '$lib/Ack.svelte';
	import Link from '$lib/Link.svelte';

	import About from '$lib/About.svelte';
	import Expando from '$lib/Expando.svelte';
	import Legend from '$lib/Legend.svelte';
	import PopRock from '$lib/PopRock.svelte';

	const projectedScenarios = ['low_growth', 'moderate_growth', 'high_growth', 'higher_growth'];

	const projectedGravities = [0, 25, 50, 75, 100];

	const fiberColors = (d) => {
		const domain = [1, 2, 5, 10, 25];
		const colors = [
			[233, 7, 108, 64],
			[233, 7, 108, 84],
			[233, 7, 108, 104],
			[233, 7, 108, 124],
			[233, 7, 108, 144],
			[233, 7, 108, 164]
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

	let aboutExpanded = $state(false);
	let layersExpanded = $state(true);
	let getDataExpanded = $state(true);

	let existingDataCenterOn = $state(true);
	let projectedDataCenterOn = $state(true);
	let municipalWaterOn = $state(true);
	let fiberOn = $state(true);
	let transmissionOn = $state(true);

	let existingDataCenterLoaded = $state(false);
	let projectedDataCenterLoaded = $state(false);
	let municipalWaterLoaded = $state(false);
	let fiberLoaded = $state(false);
	let transmissionLoaded = $state(false);

	let projectedScenario = $state(projectedScenarios[1]);
	let projectedGravity = $state(projectedGravities[2]);
</script>

<div class="relative h-screen max-h-screen w-screen overflow-hidden">
	<div
		class="absolute top-0 left-0 z-10 max-h-screen w-80 overflow-auto py-1 pr-2 pl-1 md:w-[28rem] md:py-2 md:pr-3 md:pl-2"
	>
		<div
			class="w-full rounded bg-black/60 pt-1 shadow backdrop-blur-sm md:pt-2"
			style="box-shadow: 1px 1px 6px 0px #FFFFFF40;"
		>
			<div class="flex flex-row items-center justify-between px-2 md:px-4">
				<h1 class="text-base font-semibold text-white md:text-xl">
					<a
						href="https://im3.pnnl.gov"
						target="_blank"
						rel="noreferrer"
						class="font-montserrat mr-0.5 text-lg text-sky-400 md:mr-1 md:text-2xl"
						>IM<sub>3</sub></a
					> Open Source Data Center Atlas
				</h1>
			</div>
			<div class="mt-1 mb-2 px-2 md:mt-2 md:mb-4 md:px-4">
				<p class="text-xs leading-tight text-white md:text-sm">
					Explore current and future projections of data center locations and supporting
					infrastructure.
				</p>
			</div>
			<Expando label="Layers" bind:expanded={layersExpanded}>
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
			<Expando label="About" bind:expanded={aboutExpanded}>
				<About />
			</Expando>
			<Expando label="Get the data" bind:expanded={getDataExpanded}>
				<div
					class="
                        flex w-full flex-row items-center px-4 py-2
                        text-start text-base font-bold text-gray-200 uppercase
                    "
				>
					<div class="flex flex-1 flex-row items-center justify-around pl-2 text-xs md:text-sm">
						<Link href="https://doi.org/10.57931/3017294">
							<Icon class="mr-1 inline-block" inline icon="carbon:data-center"></Icon>Existing
						</Link>
						<Link href="https://doi.org/10.57931/3020186">
							<Icon class="mr-1 inline-block" inline icon="ph:chart-line-up"></Icon>Projected
						</Link>
					</div>
				</div>
			</Expando>
		</div>
	</div>

	<div class="h-full w-full">
		<MapLibre
			style="https://basemaps.cartocdn.com/gl/dark-matter-gl-style/style.json"
			class="h-full w-full"
			maxBounds={[
				[-170, 15],
				[-40, 60]
			]}
			dragRotate={false}
			pitchWithRotate={false}
			standardControls="bottom-right"
		>
			<DeckGlLayer
				id="transmission_lines"
				visible={transmissionOn}
				type={MVTLayer}
				data={`${base}/tiles/transmission/metadata.json`}
				getLineColor={[254, 217, 118]}
				getLineWidth={0.25}
				lineWidthUnits="pixels"
				tileSize={256}
				minZoom={0}
				maxZoom={8}
				maxzoom={10}
				extent={[-159.779336, 13.447581, 144.823499, 65.01721]}
				parameters={{ depthTest: false }}
				onDataLoad={() => {
					transmissionLoaded = true;
				}}
			>
				<PopRock />
			</DeckGlLayer>
			<DeckGlLayer
				id="transmission_lines"
				visible={transmissionOn}
				type={MVTLayer}
				data={`${base}/tiles/transmission/metadata.json`}
				getLineColor={[254, 217, 118]}
				getLineWidth={1}
				lineWidthUnits="pixels"
				tileSize={256}
				minZoom={0}
				maxZoom={8}
				minzoom={10}
				extent={[-159.779336, 13.447581, 144.823499, 65.01721]}
				parameters={{ depthTest: false }}
				onDataLoad={() => {
					transmissionLoaded = true;
				}}
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
				lineWidthUnits="pixels"
				parameters={{ depthTest: false }}
				onDataLoad={() => {
					fiberLoaded = true;
				}}
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
				extent={[-124.513131, 24.544502, -66.980034, 49.002403]}
				parameters={{ depthTest: false }}
				onDataLoad={() => {
					municipalWaterLoaded = true;
				}}
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
					lineWidthUnits="pixels"
					pointRadiusUnits="pixels"
					maxzoom={11}
					parameters={{ depthTest: false }}
					onDataLoad={() => {
						existingDataCenterLoaded = true;
					}}
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
					lineWidthUnits="pixels"
					pointRadiusUnits="pixels"
					maxzoom={11}
					parameters={{ depthTest: false }}
					onDataLoad={() => {
						projectedDataCenterLoaded = true;
					}}
				>
					<PopRock />
				</DeckGlLayer>
				<DeckGlLayer
					id="data_center_footprints"
					visible={existingDataCenterOn}
					type={GeoJsonLayer}
					data={`${base}/im3_datacenter_footprints.geojson`}
					getLineColor={(d) =>
						d?.properties?.type === 'campus' ? [209, 178, 0, 180] : [3, 160, 139]}
					getFillColor={(d) =>
						d?.properties?.type === 'campus' ? [255, 226, 63, 180] : [5, 230, 201]}
					getPointRadius={4}
					getLineWidth={1}
					lineWidthUnits="pixels"
					pointRadiusUnits="pixels"
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
					lineWidthUnits="pixels"
					pointRadiusUnits="pixels"
					minzoom={11}
					parameters={{ depthTest: false }}
				>
					<PopRock />
				</DeckGlLayer>
			{/if}
			<DeckGlLayer
				id="state_boundaries"
				type={GeoJsonLayer}
				data={`${base}/conus_state_boundary.geojson`}
				stroked={true}
				filled={false}
				getLineColor={[255, 255, 255, 200]}
				getLineWidth={1}
				lineWidthUnits="pixels"
				parameters={{ depthTest: false }}
			>
				<PopRock />
			</DeckGlLayer>
		</MapLibre>
	</div>

	{#if showAck}
		<Ack bind:show={showAck} />
	{/if}
</div>
