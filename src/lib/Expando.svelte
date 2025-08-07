<script>

    import Icon from "@iconify/svelte";
    import Link from "./Link.svelte";

    let {
        label = '',
        children = undefined,
        expanded = $bindable(true),
        downloado = false,
    } = $props();

    let height = $state(0)

</script>


<div
    class="
        border-t border-t-[#506372]
        overflow-hidden transition-[height]
    "
    class:h-10={downloado || !expanded}
    style="height:{!downloado && expanded ? `calc(2.5rem + ${height}px)` : ''}"
>
    {#if downloado}
        <div
            class="
                flex flex-row items-center font-bold text-base text-gray-200 
                px-4 py-2 uppercase w-full text-start
            "
        >
            <Icon
                class="inline-block mr-1"
                inline
                icon="ph:arrow-square-out-bold"
            /> <span class="hidden md:inline">Get the&nbsp;</span> Data
            <div class="flex-1 flex flex-row items-center justify-around text-xs md:text-sm pl-2">
                <Link href=https://doi.org/10.57931/2550666>
                    <Icon class="inline-block mr-1" inline icon="carbon:data-center"></Icon>Existing
                </Link>
                <Link href=https://doi.org/10.57931/2571680>
                    <Icon class="inline-block mr-1" inline icon="ph:chart-line-up"></Icon>Projected
                </Link>
            </div>
        </div>
    {:else}
        <button
            class="
                font-bold text-base text-gray-200 hover:text-sky-400
                px-4 py-2 cursor-pointer uppercase w-full text-start
            "
            onclick={() => { expanded = !expanded }}
        >
            <Icon
                class="inline-block"
                inline
                icon={expanded ? "ph:caret-down-bold" : "ph:caret-right-bold"}
            /> {label}
        </button>
        <div
            class="px-4 pb-2" 
            bind:clientHeight={height}
        >
            {@render children?.()}
        </div>
    {/if}
</div>
