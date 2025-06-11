<script>
    let {
        show = $bindable(),
    } = $props();
</script>

<div
    class="
        absolute top-0 left-0 right-0 bottom-0
        bg-black/75 z-50 pb-4
        flex items-center justify-center overflow-hidden
    "
>
    <div
        class="
            w-11/12 h-3/4 max-w-xl max-h-max
            bg-white rounded shadow
            px-4 py-2 flex flex-col
        "
    >
        <h1 class="font-semibold text-lg">
            Disclaimer
        </h1>
        <div class="mt-2 p-2 rounded-sm text-sm overflow-y-auto border border-gray-200">
            <p class="">
                This material was prepared as an account of work sponsored by an agency of the United States Government.  Neither the United States Government nor the United States Department of Energy, nor the Contractor, nor any or their employees, nor any jurisdiction or organization that has cooperated in the development of these materials, makes any warranty, express or implied, or assumes any legal liability or responsibility for the accuracy, completeness, or usefulness or any information, apparatus, product, software, or process disclosed, or represents that its use would not infringe privately owned rights.  Reference herein to any specific commercial product, process, or service by trade name, trademark, manufacturer, or otherwise does not necessarily constitute or imply its endorsement, recommendation, or favoring by the United States Government or any agency thereof, or Battelle Memorial Institute. The views and opinions of authors expressed herein do not necessarily state or reflect those of the United States Government or any agency thereof.
            </p>
            <p class="mt-4 text-center">
                PACIFIC NORTHWEST NATIONAL LABORATORY<br/>
                operated by<br/>
                BATTELLE<br/>
                for the<br/>
                UNITED STATES DEPARTMENT OF ENERGY<br/>
                under Contract DE-AC05-76RL01830
            </p>
        </div>
        <div class="mt-4 pb-2 flex justify-center md:justify-end">
            <button
                class="
                    px-2 py-1 bg-blue-600 text-white text-sm
                    hover:border-blue-500 hover:ring hover:ring-blue-500/20
                    rounded-sm cursor-pointer
                    shadow shadow-black/25 border border-blue-600
                    active:shadow-inner active:shadow-white/25 active:border-blue-700/50
                "
                onclick={() => { show = false }}
            >
                Acknowledge
            </button>
        </div>
    </div>
</div>