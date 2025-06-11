<script>
    import Icon from '@iconify/svelte';
    import Hexagon from '$lib/Hexagon.svelte';

    let {
        existingDataCenterOn        = $bindable(true),
        existingDataCenterCampusOn  = $bindable(true),
        projectedDataCenterOn       = $bindable(true),
        fiberOn                     = $bindable(true),
        municipalWaterOn            = $bindable(true),
        transmissionOn              = $bindable(true),
        existingDataCenterLoaded    = true,
        fiberLoaded                 = true,
        municipalWaterLoaded        = true,
        transmissionLoaded          = true,
    } = $props();

</script>

<div class="pb-2">
    <button
        class="cursor-pointer flex flex-row gap-1 md:gap-2 items-center w-full h-8"
        onclick={() => { existingDataCenterOn = !existingDataCenterOn }}
        disabled={!existingDataCenterLoaded}
    >
        <Icon
            inline
            class="
                w-4 md:w-6 h-4 md:h-6 shrink-0
                {existingDataCenterLoaded && existingDataCenterOn ? 'text-blue-600' : 'text-gray-500'}
            "
            icon={existingDataCenterLoaded ? (existingDataCenterOn ? "proicons:checkbox-checked" : "proicons:checkbox-unchecked") : "proicons:checkbox-indeterminate" }
        />
        <span
            class="
                text-xs md:text-sm ml-1 md:ml-0
                {existingDataCenterLoaded && existingDataCenterOn ? 'text-black' : 'text-gray-500'}
            "
        >
            Existing Data Centers
        </span>
        {#if !existingDataCenterLoaded}
            <Icon
                inline
                class="text-[#d77900] shrink-0"
                icon="line-md:downloading-loop"
            />
        {/if}
        <div class="ml-auto h-4 md:h-5 w-4 md:w-5 rounded-full bg-[#54278f] border border-solid border-[#3f007d]"></div>
        <div class="h-4 md:h-5 w-6 md:w-8 rounded-xs bg-[#54278f] border border-solid border-[#3f007d] text-white font-semibold text-[0.5rem] md:text-[0.67rem]">Bldg</div>
        <div class="h-4 md:h-5 w-6 md:w-8 rounded-xs bg-[rgb(65,171,93)]/50 border border-solid border-[#41ab5d] text-white font-semibold text-[0.5rem] md:text-[0.67rem]">Land</div>
    </button>
    <button
        class="flex flex-row gap-2 items-center w-full h-8"
        disabled
    >
        <Icon
            inline
            class="
                w-4 md:w-6 h-4 md:h-6 shrink-0
                text-gray-500
            "
            icon="proicons:checkbox-indeterminate"
        />
        <span
            class="
                text-xs md:text-sm
                text-gray-500 italic
            "
        >
            Projected Data Centers <span class="hidden md:inline">(coming soon!)</span><span class="md:hidden inline">(TBD)</span>
        </span>
        <div class="ml-auto h-4 md:h-5 w-4 md:w-5 rounded-full bg-[#acacac]/25 border border-solid border-[#acacac]/50"></div>
        <div class="h-4 md:h-5 w-12 md:w-18 rounded-xs bg-[#acacac]/25 border border-solid border-[#acacac]/50 text-white font-semibold text-[0.5rem] md:text-[0.67rem]"></div>
    </button>
    <button
        class="cursor-pointer flex flex-row gap-2 items-center w-full h-8"
        onclick={() => { municipalWaterOn = !municipalWaterOn }}
        disabled={!municipalWaterLoaded}
    >
        <Icon
            inline
            class="
                w-4 md:w-6 h-4 md:h-6 shrink-0
                {municipalWaterLoaded && municipalWaterOn ? 'text-blue-600' : 'text-gray-500'}
            "
            icon={municipalWaterLoaded ? (municipalWaterOn ? "proicons:checkbox-checked" : "proicons:checkbox-unchecked") : "proicons:checkbox-indeterminate" }
        />
        <span
            class="
                text-xs md:text-sm
                {municipalWaterLoaded && municipalWaterOn ? 'text-black' : 'text-gray-500'}
            "
        >
            Municipal Water <span class="hidden md:inline">Service</span> Areas
        </span>
        {#if !municipalWaterLoaded}
            <Icon
                inline
                class="text-[#d77900] w-4 md:w-6 h-4 md:h-6 shrink-0"
                icon="line-md:downloading-loop"
            />
        {/if}
        <div class="ml-auto h-4 md:h-5 w-18 md:w-25 rounded-xs bg-[#2c7fb8]/25 border border-solid border-[#2c7fb8]/25"></div>
    </button>
    <button
        class="cursor-pointer flex flex-row gap-2 items-center w-full h-8"
        onclick={() => { transmissionOn = !transmissionOn }}
        disabled={!transmissionLoaded}
    >
        <Icon
            inline
            class="
                w-4 md:w-6 h-4 md:h-6 shrink-0
                {transmissionLoaded && transmissionOn ? 'text-blue-600' : 'text-gray-500'}
            "
            icon={transmissionLoaded ? (transmissionOn ? "proicons:checkbox-checked" : "proicons:checkbox-unchecked") : "proicons:checkbox-indeterminate" }
        />
        <span
            class="
                text-xs md:text-sm
                {transmissionLoaded && transmissionOn ? 'text-black' : 'text-gray-500'}
            "
        >
            Transmission Lines
        </span>
        {#if !transmissionLoaded}
            <Icon
                inline
                class="text-[#d77900] w-4 md:w-6 h-4 md:h-6 shrink-0"
                icon="line-md:downloading-loop"
            />
        {/if}
        <div class="ml-auto h-1 w-18 md:w-25 rounded-xs bg-[rgb(254,217,118)]"></div>
    </button>
    <button
        class="cursor-pointer flex flex-row gap-2 items-center w-full h-8"
        onclick={() => { fiberOn = !fiberOn }}
        disabled={!fiberLoaded}
    >
        <Icon
            inline
            class="
                w-4 md:w-6 h-4 md:h-6 shrink-0
                {fiberLoaded && fiberOn ? 'text-blue-600' : 'text-gray-500'}
            "
            icon={fiberLoaded ? (fiberOn ? "proicons:checkbox-checked" : "proicons:checkbox-unchecked") : "proicons:checkbox-indeterminate" }
        />
        <span
            class="
                text-xs md:text-sm
                {fiberLoaded && fiberOn ? 'text-black' : 'text-gray-500'}
            "
        >
            <span class="hidden md:inline">High Speed</span> Fiber Provider Density
        </span>
        {#if !fiberLoaded}
            <Icon
                inline
                class="text-[#d77900] w-4 md:w-6 h-4 md:h-6 shrink-0"
                icon="line-md:downloading-loop"
            />
        {/if}
        <div class="ml-auto flex flex-row items-center">
            <Hexagon
                backgroundColorRGBA="rgba(244, 163, 168, 64)"
            >1</Hexagon>
            <Hexagon
                backgroundColorRGBA="rgba(227, 129, 145, 64)"
                class="mt-4 -ml-1"
            >2</Hexagon>
            <Hexagon
                backgroundColorRGBA="rgba(204,  96, 125, 64)"
                class="-ml-1"
            >5</Hexagon>
            <Hexagon
                backgroundColorRGBA="rgba(173,  70, 108, 64)"
                class="mt-4 -ml-1"
            >10</Hexagon>
            <Hexagon
                backgroundColorRGBA="rgba(139,  48,  88, 64)"
                class="-ml-1"
            >25</Hexagon>
        </div>
    </button>
</div>
