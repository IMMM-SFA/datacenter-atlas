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
    class="text-sm flex flex-col gap-4 pb-4"
>
    <p>
        The <Link href="https://im3.pnnl.gov">IM3</Link> Open Source Data Center Atlas provides locations and facility footprints (when available) of existing data centers across the United States (U.S.). In addition to data center locations, the dashboard also provides complementary information on electricity infrastructure, municipal water supply, and high-speed fiber availability. This dashboard can be used to identify areas of concentrated data center development and inform government and private sector planning strategies for future buildout of data centers and the infrastructure necessary to support it.
    </p>
    <p>
        Data center locations were derived from OpenStreetMap (OSM), an open crowd-sourced database available for reuse <sup class="text-blue-600"><button class="cursor-pointer" onclick={() => slideto(1)}>[1]</button></sup>. Data centers in the dataset are a mixture of small-scale collocated facilities that might support individual firms and hyperscale data centers that are supporting the widespread expansion of computing for Artificial Intelligence (AI). Data points from OSM have been processed to determine additional variables provided in the dataset including facility area (square feet) and associated U.S. county and U.S. state <sup class="text-blue-600"><button class="cursor-pointer" onclick={() => slideto(2)}>[2]</button></sup>. The post-processed dataset has been made available for reuse (see citation below).
    </p>
    <p>
        We include additional data layers that provide context for why data centers might be located in certain areas. Transmission line data was collected from the Homeland Infrastructure Foundation-Level Data (HIFLD) <sup class="text-blue-600"><button class="cursor-pointer" onclick={() => slideto(3)}>[3]</button></sup> and shows lines across a range of voltages. Public supply water service areas were collected from data provided by the U.S. Geological Survey (USGS) <sup class="text-blue-600"><button class="cursor-pointer" onclick={() => slideto(4)}>[4]</button></sup>. Water supply areas spatially represent where customers are served by each public water supplier. Fiber availability is derived from information in the Federal Communications Commission’s (FCC) National Broadband Map <sup class="text-blue-600"><button class="cursor-pointer" onclick={() => slideto(5)}>[5]</button></sup>. This layer shows the number of fiber service providers capable of delivering greater than or equal to 1 Gbps of fiber service to customers in each area.
    </p>
    <p>
        If you use this data in a downstream application, please use the following citation:
    </p>
    <p class="ml-1 pl-2 border-l-3 border-l-[#d77900] rounded text-xs italic">
        Mongird, <span class="cursor-[url(/minesheep.png),auto]">K</span>., Thurber, T., Vernon, C., Burleyson, C., Akdemir, K. Z., & Rice, J. (2025). IM3 Open Source Data Center Atlas (Version v1) [Data set]. MSD-LIVE Data Repository. <Link href=https://doi.org/10.57931/2550666 />
    </p>
    <p>
        Additionally, because of the Open Database License (ODbL) license applied to the OSM dataset any derivative datasets intended for reuse should continue to apply the ODbL license.
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
            <span>HIFLD (2025). Transmission Lines. Geospatial Management Office. Available at <Link href=https://hifld-geoplatform.hub.arcgis.com/datasets/geoplatform::transmission-lines-1/about />.</span>
        </span>
        <span id='ref-4' class="flex flex-row gap-2">
            <span>[4]</span>
            <span>Buchwald, C.A., Houston, N.A., Stewart, J.S., York, B.C., and Valseth, K.J., (2022). Public-supply water service areas within the conterminous United States, 2017, U.S. Geological Survey data release: <Link href=https://doi.org/10.5066/P9I22Z24 />.</span>
        </span>
        <span id='ref-5' class="flex flex-row gap-2">
            <span>[5]</span>
            <span>FCC (2025). National Broadband Map. Available at: <Link href=https://broadbandmap.fcc.gov/home />.</span>
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