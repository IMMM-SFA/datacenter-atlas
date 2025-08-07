<script>
    import Icon from '@iconify/svelte';
    import Hexagon from '$lib/Hexagon.svelte';

    function toTitleCase(str) {
        const outStr = str.replace('_', ' ');
        return outStr.replace(
            /\w\S*/g,
            text => text.charAt(0).toUpperCase() + text.substring(1).toLowerCase()
        );
    }

    let {
        existingDataCenterOn        = $bindable(true),
        projectedDataCenterOn       = $bindable(true),
        projectedScenario           = $bindable(),
        projectedGravity            = $bindable(),
        fiberOn                     = $bindable(true),
        municipalWaterOn            = $bindable(true),
        transmissionOn              = $bindable(true),
        existingDataCenterLoaded    = true,
        projectedDataCenterLoaded   = true,
        fiberLoaded                 = true,
        municipalWaterLoaded        = true,
        transmissionLoaded          = true,
        projectedScenarios          = [],
        projectedGravities          = [],
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
                w-4 md:w-6 h-4 md:h-6 shrink-0 text-[#85BFE5]
            "
            icon={existingDataCenterLoaded ? (existingDataCenterOn ? "proicons:checkbox-checked" : "proicons:checkbox-unchecked") : "proicons:checkbox-indeterminate" }
        />
        <span
            class="
                text-xs md:text-sm ml-1 md:ml-0 text-white
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
        <div class="ml-auto h-4 md:h-5 w-4 md:w-5 rounded-full bg-[#05e6c9] border border-solid border-[#03A08B]"></div>
        <div class="h-4 md:h-5 w-6 md:w-8 rounded-xs bg-[#05e6c9] border border-solid border-[#03A08B] text-white font-semibold text-[0.5rem] md:text-[0.67rem]">Bldg</div>
        <div class="h-4 md:h-5 w-6 md:w-8 rounded-xs bg-[#ffe23f]/70 border border-solid border-[#D1B200]/70 text-white font-semibold text-[0.5rem] md:text-[0.67rem]">Land</div>
    </button>
    <button
        class="flex flex-row gap-1 md:gap-2 items-center w-full h-8"
        onclick={() => { projectedDataCenterOn = !projectedDataCenterOn }}
        disabled={!projectedDataCenterLoaded}
    >
        <Icon
            inline
            class="
                w-4 md:w-6 h-4 md:h-6 shrink-0 text-[#85BFE5]
            "
            icon={projectedDataCenterLoaded ? (projectedDataCenterOn ? "proicons:checkbox-checked" : "proicons:checkbox-unchecked") : "proicons:checkbox-indeterminate" }
        />
        <span
            class="
                text-xs md:text-sm ml-1 md:ml-0 text-white
            "
        >
            Projected Data Centers (2035)
        </span>
        {#if !projectedDataCenterLoaded}
            <Icon
                inline
                class="text-[#d77900] shrink-0"
                icon="line-md:downloading-loop"
            />
        {/if}
        <div class="ml-auto h-4 md:h-5 w-4 md:w-5 rounded-full bg-[#8cdd35]/85 border border-solid border-[#8cdd35]/85"></div>
        <div class="h-4 md:h-5 w-6 md:w-18 rounded-xs bg-[#8cdd35]/85 border border-solid border-[#8cdd35]/85 text-white font-semibold text-[0.5rem] md:text-[0.67rem]"></div>
    </button>
    <div class="flex flex-row pl-6 md:pl-7 md:pl-8 gap-4 mb-2 -mt-1">
        <div
            class="
                flex flex-col text-white text-xs
            "
        >
            <label
                for='projectedScenario'
            >
                Scenario:
            </label>
            <select
                bind:value={projectedScenario}
                disabled={!projectedDataCenterOn}
                id='projectedScenario'
                class="border border-white rounded-sm"
            >
                {#each projectedScenarios as s}
                    <option
                        class=""
                        value={s}
                    >
                        {toTitleCase(s)}
                    </option>
                {/each}
            </select>
        </div>
        <div
            class="
                flex flex-col text-white text-xs
            "
        >
            <label
                for='projectedGravity'
            >
                Market Gravity:
            </label>
            <select
                bind:value={projectedGravity}
                disabled={!projectedDataCenterOn}
                id='projectedGravity'
                class="border border-white rounded-sm"
            >
                {#each projectedGravities as g}
                    <option
                        class=""
                        value={g}
                    >
                        {g}
                    </option>
                {/each}
            </select>
        </div>
    </div>
    <button
        class="cursor-pointer flex flex-row gap-2 items-center w-full h-8"
        onclick={() => { municipalWaterOn = !municipalWaterOn }}
        disabled={!municipalWaterLoaded}
    >
        <Icon
            inline
            class="
                w-4 md:w-6 h-4 md:h-6 shrink-0 text-[#85BFE5]
            "
            icon={municipalWaterLoaded ? (municipalWaterOn ? "proicons:checkbox-checked" : "proicons:checkbox-unchecked") : "proicons:checkbox-indeterminate" }
        />
        <span
            class="
                text-xs md:text-sm text-white
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
        <div class="ml-auto h-4 md:h-5 w-18 md:w-25 rounded-xs bg-[#00aeef]/50 border border-solid border-[#00aeef]/50"></div>
    </button>
    <button
        class="cursor-pointer flex flex-row gap-2 items-center w-full h-8"
        onclick={() => { transmissionOn = !transmissionOn }}
        disabled={!transmissionLoaded}
    >
        <Icon
            inline
            class="
                w-4 md:w-6 h-4 md:h-6 shrink-0 text-[#85BFE5]
            "
            icon={transmissionLoaded ? (transmissionOn ? "proicons:checkbox-checked" : "proicons:checkbox-unchecked") : "proicons:checkbox-indeterminate" }
        />
        <span
            class="
                text-xs md:text-sm text-white
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
                w-4 md:w-6 h-4 md:h-6 shrink-0 text-[#85BFE5]
            "
            icon={fiberLoaded ? (fiberOn ? "proicons:checkbox-checked" : "proicons:checkbox-unchecked") : "proicons:checkbox-indeterminate" }
        />
        <span
            class="
                text-xs md:text-sm text-white
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
                backgroundColorRGBA="rgba(233, 7, 108, 0.25)"
            >1</Hexagon>
            <Hexagon
                backgroundColorRGBA="rgba(233, 7, 108, 0.35)"
                class="mt-4 -ml-1"
            >2</Hexagon>
            <Hexagon
                backgroundColorRGBA="rgba(233, 7, 108, 0.45)"
                class="-ml-1"
            >5</Hexagon>
            <Hexagon
                backgroundColorRGBA="rgba(233, 7, 108, 0.55)"
                class="mt-4 -ml-1"
            >10</Hexagon>
            <Hexagon
                backgroundColorRGBA="rgba(233, 7, 108, 0.65)"
                class="-ml-1"
            >25</Hexagon>
        </div>
    </button>
</div>
