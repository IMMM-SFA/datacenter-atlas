<script>

    import im3Logo from "$lib/img/im3-logo.png";
    import doeLogo from "$lib/img/doe-os-logo.jpg";
    import Link from "./Link.svelte";

    const slideto = (ref) => {
        const element = document?.getElementById(`ref-${ref}`)

        if (element) {
            element.scrollIntoView({
                behavior: 'smooth',
            });

            element.style.transition = 'none';
            element.style.backgroundColor = 'rgba(255,222,33,0.5)';

            setTimeout(() => {
                element.style.transition = 'background 3s';
                element.style.backgroundColor = '';
            }, 200);
        }
    }

</script>

<div
    class="text-xs md:text-sm flex flex-col gap-4 pb-4 pr-4 text-white max-h-96 overflow-y-auto"
>
    <p>
        The <Link href="https://im3.pnnl.gov">IM3</Link> Open Source Data Center Atlas provides locations and facility footprints (when available) of existing and projected data centers across the United States (U.S.).
    </p>
    <p>
        Existing data centers are a mixture of small-scale, co-located facilities that might support individual firms and hyperscale data centers that are supporting the widespread expansion of computing for Artificial Intelligence (AI). Locations were sourced from OpenStreetMap <sup class="text-sky-400"><button class="cursor-pointer" onclick={() => slideto(1)}>[1]</button></sup> and processed to determine additional variables <sup class="text-sky-400"><button class="cursor-pointer" onclick={() => slideto(2)}>[2]</button></sup>. We also include additional data layers that provide context for why data centers might be in certain locations. These include transmission line data <sup class="text-sky-400"><button class="cursor-pointer" onclick={() => slideto(1)}>[1]</button></sup>, public supply water service areas <sup class="text-sky-400"><button class="cursor-pointer" onclick={() => slideto(3)}>[3]</button></sup>, and areas where fiber service providers can deliver greater than or equal to 1 Gbps of fiber service <sup class="text-sky-400"><button class="cursor-pointer" onclick={() => slideto(4)}>[4]</button></sup>. Visit the data repository for more information and to download the post-processed dataset of existing data centers.
    </p>
    <p>
        Projected facilities are modeled as of 2035 across four data center growth scenarios and five market gravity scenarios <sup class="text-sky-400"><button class="cursor-pointer" onclick={() => slideto(5)}>[5]</button></sup>. Market gravity scenarios indicate the relative importance of proximity to existing data center markets or high population areas compared to locational costs. Future data center locations are constrained to be within 2 km of electric substations, 5 km of water supplier service areas, and 2 km of high-speed fiber provider service areas, and include 11 additional geospatial exclusions. Future research will explore the interactions between new data centers, the electricity grid, and water availability. Visit the data repository for more information.
    </p>
    <p>
        If you use the data center location data in a downstream application, please use the following citation(s):
    </p>
    <p>
        For the existing data centers:
    </p>
    <p class="ml-1 pl-2 border-l-3 border-l-[#d77900] rounded text-xs italic">
        Mongird, K., Thurber, T., Vernon, C., Burleyson, C., Akdemir, K. Z., & Rice, J. (2025). IM3 Open Source Data Center Atlas (Version v1) [Data set]. MSD-LIVE Data Repository. <Link href=https://doi.org/10.57931/2550666 />
    </p>
    <p>
        For the projected data centers:
    </p>
    <p class="ml-1 pl-2 border-l-3 border-l-[#d77900] rounded text-xs italic">
        Mongird, K., Burleyson, C., Akdemir, K. Z., Thurber, T., Vernon, C., & Rice, J. (2025). IM3 Projected US Data Center Locations (Version v1) [Data set]. MSD-LIVE Data Repository. <Link href=https://doi.org/10.57931/2571680 />
    </p>
    <p>
        Additionally, because of the Open Database License (ODbL) license applied to the OSM dataset any derivative datasets of the existing locations intended for reuse should continue to apply the ODbL license.
    </p>
    <p class="font-medium">
        References:
    </p>
    <div class="flex flex-col gap-2 text-xs italic">
        <span id='ref-1' class="flex flex-row gap-2">
            <span class="">[1]</span>
            <span>OpenStreetMap contributors (2025). OpenStreetMap [Data set]. OpenStreetMap Foundation. Available as open data under the Open Data Commons Open Database License (ODbL) at <Link href=https://openstreetmap.org />.</span>
        </span>
        <span id='ref-2' class="flex flex-row gap-2">
            <span>[2]</span>
            <span>US Census Bureau (2024). TIGER/Line Shapefiles. U.S. Department of Commerce. <Link href=https://www.census.gov/cgi-bin/geo/shapefiles/index.php />.</span>
        </span>
        <span id='ref-3' class="flex flex-row gap-2">
            <span>[3]</span>
            <span>Buchwald, C.A., Houston, N.A., Stewart, J.S., York, B.C., and Valseth, K.J., (2022). Public-supply water service areas within the conterminous United States, 2017, U.S. Geological Survey data release: <Link href=https://doi.org/10.5066/P9I22Z24 />.</span>
        </span>
        <span id='ref-4' class="flex flex-row gap-2">
            <span>[4]</span>
            <span>FCC (2025). National Broadband Map. Available at: <Link href=https://broadbandmap.fcc.gov/home />.</span>
        </span>
        <span id='ref-5' class="flex flex-row gap-2">
            <span>[5]</span>
            <span>Aljbour, Jordan, Tom Wilson, and Poorvi Patel. "Powering intelligence: Analyzing artificial intelligence and data center energy consumption." <Link href="https://www.epri.com/research/products/000000003002028905">EPRI White Paper no. 3002028905</Link> (2024).</span>
        </span>
    </div>
    <p class="font-medium">
        Acknowledgements:
    </p>
    <div class="flex flex-row flex-wrap gap-2">
        <a class="cursor-pointer" href="https://im3.pnnl.gov" target="_blank" rel="noreferrer"><img class="h-32 object-contain" alt="" src={im3Logo} /></a>
        <a class="cursor-pointer" href="https://www.energy.gov/science/office-science" target="_blank" rel="noreferrer"><img class="h-32 object-contain" alt="" src={doeLogo} /></a>
    </div>
    <p class="text-xs italic">
        This data was collected by the IM3 project which is supported by the U.S. Department of Energy, Office of Science, as part of research in MultiSector Dynamics.
    </p>
</div>