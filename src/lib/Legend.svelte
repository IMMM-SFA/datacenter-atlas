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
        class="cursor-pointer flex flex-row gap-2 items-center w-full h-8"
        onclick={() => { existingDataCenterOn = !existingDataCenterOn }}
        disabled={!existingDataCenterLoaded}
    >
        <Icon
            inline
            class="
                {existingDataCenterLoaded && existingDataCenterOn ? 'text-blue-600' : 'text-gray-500'}
            "
            width={24}
            height={24}
            icon={existingDataCenterLoaded ? (existingDataCenterOn ? "proicons:checkbox-checked" : "proicons:checkbox-unchecked") : "proicons:checkbox-indeterminate" }
        />
        <span
            class="
                text-sm
                {existingDataCenterLoaded && existingDataCenterOn ? 'text-black' : 'text-gray-500'}
            "
        >
            Existing Data Centers
        </span>
        {#if !existingDataCenterLoaded}
            <Icon
                inline
                class="text-[#d77900]"
                width={24}
                height={24}
                icon="line-md:downloading-loop"
            />
        {/if}
        <div class="ml-auto h-5 w-5 rounded-full bg-[#54278f] border border-solid border-[#3f007d]"></div>
        <div class="h-5 w-8 rounded-xs bg-[#54278f] border border-solid border-[#3f007d] text-white font-semibold text-[0.67rem]">Bldg</div>
        <div class="h-5 w-8 rounded-xs bg-[rgb(65,171,93)]/50 border border-solid border-[#41ab5d] text-white font-semibold text-[0.67rem]">Land</div>
    </button>
    <button
        class="flex flex-row gap-2 items-center w-full h-8"
        disabled
    >
        <Icon
            inline
            class="
                text-gray-500
            "
            width={24}
            height={24}
            icon="proicons:checkbox-indeterminate"
        />
        <span
            class="
                text-sm
                text-gray-500 italic
            "
        >
            Projected Data Centers (coming soon!)
        </span>
        <div class="ml-auto h-5 w-5 rounded-full bg-[#acacac]/25 border border-solid border-[#acacac]/50"></div>
        <div class="h-5 w-18 rounded-xs bg-[#acacac]/25 border border-solid border-[#acacac]/50 text-white font-semibold text-[0.67rem]"></div>
    </button>
    <button
        class="cursor-pointer flex flex-row gap-2 items-center w-full h-8"
        onclick={() => { municipalWaterOn = !municipalWaterOn }}
        disabled={!municipalWaterLoaded}
    >
        <Icon
            inline
            class="
                {municipalWaterLoaded && municipalWaterOn ? 'text-blue-600' : 'text-gray-500'}
            "
            width={24}
            height={24}
            icon={municipalWaterLoaded ? (municipalWaterOn ? "proicons:checkbox-checked" : "proicons:checkbox-unchecked") : "proicons:checkbox-indeterminate" }
        />
        <span
            class="
                text-sm
                {municipalWaterLoaded && municipalWaterOn ? 'text-black' : 'text-gray-500'}
            "
        >
            Municipal Water Service Areas
        </span>
        {#if !municipalWaterLoaded}
            <Icon
                inline
                class="text-[#d77900]"
                width={24}
                height={24}
                icon="line-md:downloading-loop"
            />
        {/if}
        <div class="ml-auto h-5 w-25 rounded-xs bg-[#2c7fb8]/25 border border-solid border-[#2c7fb8]/25"></div>
    </button>
    <button
        class="cursor-pointer flex flex-row gap-2 items-center w-full h-8"
        onclick={() => { transmissionOn = !transmissionOn }}
        disabled={!transmissionLoaded}
    >
        <Icon
            inline
            class="
                {transmissionLoaded && transmissionOn ? 'text-blue-600' : 'text-gray-500'}
            "
            width={24}
            height={24}
            icon={transmissionLoaded ? (transmissionOn ? "proicons:checkbox-checked" : "proicons:checkbox-unchecked") : "proicons:checkbox-indeterminate" }
        />
        <span
            class="
                text-sm
                {transmissionLoaded && transmissionOn ? 'text-black' : 'text-gray-500'}
            "
        >
            Transmission Lines
        </span>
        {#if !transmissionLoaded}
            <Icon
                inline
                class="text-[#d77900]"
                width={24}
                height={24}
                icon="line-md:downloading-loop"
            />
        {/if}
        <div class="ml-auto h-1 w-25 rounded-xs bg-[rgb(254,217,118)]"></div>
    </button>
    <button
        class="cursor-pointer flex flex-row gap-2 items-center w-full h-8"
        onclick={() => { fiberOn = !fiberOn }}
        disabled={!fiberLoaded}
    >
        <Icon
            inline
            class="
                {fiberLoaded && fiberOn ? 'text-blue-600' : 'text-gray-500'}
            "
            width={24}
            height={24}
            icon={fiberLoaded ? (fiberOn ? "proicons:checkbox-checked" : "proicons:checkbox-unchecked") : "proicons:checkbox-indeterminate" }
        />
        <span
            class="
                text-sm
                {fiberLoaded && fiberOn ? 'text-black' : 'text-gray-500'}
            "
        >
            High Speed Fiber Provider Density
        </span>
        {#if !fiberLoaded}
            <Icon
                inline
                class="text-[#d77900]"
                width={24}
                height={24}
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
