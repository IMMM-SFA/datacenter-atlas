<script>
	import Icon from '@iconify/svelte';
	import Hexagon from '$lib/Hexagon.svelte';

	function toTitleCase(str) {
		const outStr = str.replace('_', ' ');
		return outStr.replace(
			/\w\S*/g,
			(text) => text.charAt(0).toUpperCase() + text.substring(1).toLowerCase()
		);
	}

	let {
		existingDataCenterOn = $bindable(true),
		projectedDataCenterOn = $bindable(true),
		projectedScenario = $bindable(),
		projectedGravity = $bindable(),
		fiberOn = $bindable(true),
		municipalWaterOn = $bindable(true),
		transmissionOn = $bindable(true),
		existingDataCenterLoaded = true,
		projectedDataCenterLoaded = true,
		fiberLoaded = true,
		municipalWaterLoaded = true,
		transmissionLoaded = true,
		projectedScenarios = [],
		projectedGravities = []
	} = $props();
</script>

<div class="pb-2">
	<button
		class="flex min-h-[2.75rem] w-full cursor-pointer items-start gap-1 md:gap-2"
		onclick={() => {
			existingDataCenterOn = !existingDataCenterOn;
		}}
		disabled={!existingDataCenterLoaded}
	>
		<Icon
			inline
			class="
                h-4 w-4 shrink-0 text-[#85BFE5] md:h-6 md:w-6
            "
			icon={existingDataCenterLoaded
				? existingDataCenterOn
					? 'proicons:checkbox-checked'
					: 'proicons:checkbox-unchecked'
				: 'proicons:checkbox-indeterminate'}
		/>
		
		<div class="flex flex-col">
	<span class="text-xs text-white md:text-sm leading-tight md:-ml-[1.5rem]">
		Existing Data Centers
	</span>
	<span class="text-[0.7rem] italic text-gray-300 leading-tight md:text-xs">
		(Last Updated Feb 09, 2026)
	</span>
</div>

		
		{#if !existingDataCenterLoaded}
			<Icon inline class="shrink-0 text-[#d77900]" icon="line-md:downloading-loop" />
		{/if}
		<div
			class="ml-auto h-4 w-4 rounded-full border border-solid border-[#03A08B] bg-[#05e6c9] md:h-5 md:w-5"
		></div>
		<div
			class="h-4 w-6 rounded-xs border border-solid border-[#03A08B] bg-[#05e6c9] text-[0.5rem] font-semibold text-white md:h-5 md:w-8 md:text-[0.67rem]"
		>
			Bldg
		</div>
		<div
			class="h-4 w-6 rounded-xs border border-solid border-[#D1B200]/70 bg-[#ffe23f]/70 text-[0.5rem] font-semibold text-white md:h-5 md:w-8 md:text-[0.67rem]"
		>
			Land
		</div>
	</button>
	<button
		class="flex h-8 w-full flex-row items-center gap-1 md:gap-2"
		onclick={() => {
			projectedDataCenterOn = !projectedDataCenterOn;
		}}
		disabled={!projectedDataCenterLoaded}
	>
		<Icon
			inline
			class="
                h-4 w-4 shrink-0 text-[#85BFE5] md:h-6 md:w-6
            "
			icon={projectedDataCenterLoaded
				? projectedDataCenterOn
					? 'proicons:checkbox-checked'
					: 'proicons:checkbox-unchecked'
				: 'proicons:checkbox-indeterminate'}
		/>
		<span
			class="
                ml-1 text-xs text-white md:ml-0 md:text-sm
            "
		>
			Projected Data Centers (2035)
		</span>
		{#if !projectedDataCenterLoaded}
			<Icon inline class="shrink-0 text-[#d77900]" icon="line-md:downloading-loop" />
		{/if}
		<div
			class="ml-auto h-4 w-4 rounded-full border border-solid border-[#8cdd35]/85 bg-[#8cdd35]/85 md:h-5 md:w-5"
		></div>
		<div
			class="h-4 w-6 rounded-xs border border-solid border-[#8cdd35]/85 bg-[#8cdd35]/85 text-[0.5rem] font-semibold text-white md:h-5 md:w-18 md:text-[0.67rem]"
		></div>
	</button>
	<div class="-mt-1 mb-2 flex flex-row gap-4 pl-6 md:pl-8">
		<div
			class="
                flex flex-col text-xs text-white
            "
		>
			<label for="projectedScenario"> Scenario: </label>
			<select
				bind:value={projectedScenario}
				disabled={!projectedDataCenterOn}
				id="projectedScenario"
				class="appearance-none rounded-sm border border-white bg-black text-white"
			>
				{#each projectedScenarios as s}
					<option
						style="background-color: black !important; color: white !important;"
						class="bg-black text-white"
						value={s}
					>
						{toTitleCase(s)}
					</option>
				{/each}
			</select>
		</div>
		<div
			class="
                flex flex-col text-xs text-white
            "
		>
			<label for="projectedGravity"> Market Gravity: </label>
			<select
				bind:value={projectedGravity}
				disabled={!projectedDataCenterOn}
				id="projectedGravity"
				class="appearance-none rounded-sm border border-white bg-black text-white"
			>
				{#each projectedGravities as g}
					<option
						style="background-color: black !important; color: white !important;"
						class=""
						value={g}
					>
						{g}%
					</option>
				{/each}
			</select>
		</div>
	</div>
	<button
		class="flex h-8 w-full cursor-pointer flex-row items-center gap-2"
		onclick={() => {
			municipalWaterOn = !municipalWaterOn;
		}}
		disabled={!municipalWaterLoaded}
	>
		<Icon
			inline
			class="
                h-4 w-4 shrink-0 text-[#85BFE5] md:h-6 md:w-6
            "
			icon={municipalWaterLoaded
				? municipalWaterOn
					? 'proicons:checkbox-checked'
					: 'proicons:checkbox-unchecked'
				: 'proicons:checkbox-indeterminate'}
		/>
		<span
			class="
                text-xs text-white md:text-sm
            "
		>
			Municipal Water <span class="hidden md:inline">Service</span> Areas
		</span>
		{#if !municipalWaterLoaded}
			<Icon
				inline
				class="h-4 w-4 shrink-0 text-[#d77900] md:h-6 md:w-6"
				icon="line-md:downloading-loop"
			/>
		{/if}
		<div
			class="ml-auto h-4 w-18 rounded-xs border border-solid border-[#00aeef]/50 bg-[#00aeef]/50 md:h-5 md:w-25"
		></div>
	</button>
	<button
		class="flex h-8 w-full cursor-pointer flex-row items-center gap-2"
		onclick={() => {
			transmissionOn = !transmissionOn;
		}}
		disabled={!transmissionLoaded}
	>
		<Icon
			inline
			class="
                h-4 w-4 shrink-0 text-[#85BFE5] md:h-6 md:w-6
            "
			icon={transmissionLoaded
				? transmissionOn
					? 'proicons:checkbox-checked'
					: 'proicons:checkbox-unchecked'
				: 'proicons:checkbox-indeterminate'}
		/>
		<span
			class="
                text-xs text-white md:text-sm
            "
		>
			Transmission Lines
		</span>
		{#if !transmissionLoaded}
			<Icon
				inline
				class="h-4 w-4 shrink-0 text-[#d77900] md:h-6 md:w-6"
				icon="line-md:downloading-loop"
			/>
		{/if}
		<div class="ml-auto h-1 w-18 rounded-xs bg-[rgb(254,217,118)] md:w-25"></div>
	</button>
	<button
		class="flex h-8 w-full cursor-pointer flex-row items-center gap-2"
		onclick={() => {
			fiberOn = !fiberOn;
		}}
		disabled={!fiberLoaded}
	>
		<Icon
			inline
			class="
                h-4 w-4 shrink-0 text-[#85BFE5] md:h-6 md:w-6
            "
			icon={fiberLoaded
				? fiberOn
					? 'proicons:checkbox-checked'
					: 'proicons:checkbox-unchecked'
				: 'proicons:checkbox-indeterminate'}
		/>
		<span
			class="
                text-xs text-white md:text-sm
            "
		>
			<span class="hidden md:inline">High Speed</span> Fiber Provider Density
		</span>
		{#if !fiberLoaded}
			<Icon
				inline
				class="h-4 w-4 shrink-0 text-[#d77900] md:h-6 md:w-6"
				icon="line-md:downloading-loop"
			/>
		{/if}
		<div class="ml-auto flex flex-row items-center">
			<Hexagon backgroundColorRGBA="rgba(233, 7, 108, 0.25)">1</Hexagon>
			<Hexagon backgroundColorRGBA="rgba(233, 7, 108, 0.35)" class="mt-4 -ml-1">2</Hexagon>
			<Hexagon backgroundColorRGBA="rgba(233, 7, 108, 0.45)" class="-ml-1">5</Hexagon>
			<Hexagon backgroundColorRGBA="rgba(233, 7, 108, 0.55)" class="mt-4 -ml-1">10</Hexagon>
			<Hexagon backgroundColorRGBA="rgba(233, 7, 108, 0.65)" class="-ml-1">25</Hexagon>
		</div>
	</button>
</div>

<style>
	select {
		background-color: black;
		color: white;
		border: 1px solid white;
	}
	option {
		background-color: black !important;
		color: white !important;
	}
</style>
