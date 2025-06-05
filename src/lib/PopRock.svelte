<script>

    import Popup from 'svelte-maplibre/Popup.svelte';

    const keyToLabel = {
        'name'          : 'Name',
        'operator'      : 'Operator',
        'state_abb'     : 'State',
        'county'        : 'County',
        'sqft'          : 'Footprint sq ft',
        'VOLT_CLASS'    : 'Voltage Class (kV)',
        'WSA_NAME'      : 'Water Service Area Name',
        'provider_count'    : 'High Speed Fiber Providers'
    }

</script>

<Popup openOn='click'>
    {#snippet children({ data })}
        <div class="flex flex-col gap-2 w-40">
            {#each Object.keys(keyToLabel) as k}
                {#if data.properties?.[k] || data[k]}
                    <div class="flex flex-col items-start">
                        <p class="text-[0.67rem] whitespace-nowrap uppercase leading-none text-gray-700">
                            {keyToLabel[k]}
                        </p>
                        <p class="text-base text-black leading-tight">
                            {#if k==='sqft'}
                                {Math.round(data.properties[k]).toLocaleString()}
                            {:else if k==='provider_count'}
                                {data[k] > 25 ? "25+" : data[k]}
                            {:else}
                                {data.properties?.[k]}
                            {/if}
                        </p>
                    </div>
                {/if}
            {/each}
        </div>
    {/snippet}
</Popup>
