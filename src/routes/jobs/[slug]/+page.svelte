<script>
    import SvelteMarkdown from 'svelte-markdown';
    import humanize from 'humanize-plus';
    import { getUserId } from '../../../utils/auth.js';
    export let data;
   
    

    


</script>

<div class="mt-10 pr-16 pl-16 pb-16">
    <div class="flex">
        <div class="flex-1">
            <h1 class="text-3xl font-extrabold">{data.job.title}</h1>
            <p class="text-xl">{data.job.employer}</p>
        </div>
    </div>

    <div class="flex flex-row w-full mt-8">
        <div class="basis-2/3 prose max-w-none w-full">
            <h2 class="text-xl font-thin">Description</h2>
            <SvelteMarkdown source={data.job.description} />
            <div class="mt-6" />
            <h2 class="text-xl font-thin">Requirements</h2>
            <SvelteMarkdown source={data.job.requirements} />
            <div class="mt-6" />
            <h2 class="text-xl font-thin">How to Apply?</h2>
            <SvelteMarkdown source={data.job.applicationInstructions} />
        
        </div>
        <div class="basis-1/3 ml-4">
            <h2 class="text-xl font-thin">Location</h2>
            <SvelteMarkdown source={data.job.location} />
            <div class="mt-6" />
            <h2 class="text-xl font-thin">Salary Range</h2>
            <p>
                USD {humanize.formatNumber(data.job.minAnnualCompensation)} - USD {humanize.formatNumber(
                    data.job.maxAnnualCompensation
                )}
            </p>
        </div>
    </div>
    <div class="pt-10 position-relative left-0"> 
            {#if data.job.user == getUserId()}
            <a href = "/jobs/{data.job.id}/update" class="text-white bg-gray-700 hover:bg-white hover:text-black focus:ring-4 focus:ring-transparent-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-transparent-600 dark:hover:bg-transparent-700 focus:outline-none dark:focus:ring-transparent-800">Edit</a>
            {/if}
    </div>
       
        
</div>

