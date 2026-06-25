<script>
    let {deletefunc, profit = $bindable(0), principal = $bindable()} = $props(); //function and variables passed down from parent. Inplace modifiable object, similar to referece by memory in c
    //default 0 profit. THIS component CANNOT MODIFY deletefunc, it is readonly. bindable creates a pipe to the caller function for remote modification
    //row.profit -> bind:profit -> bindable -> calculator's profit
    let rate = $state()  //variables to store user input
    let weeks = $state()
    
    $effect(() => { //tells the DOM to watch for any changes in values to principal rate and weeks
        profit = (principal && rate && weeks) ? principal * (rate / 100) * (weeks / 52) : 0; //run the math to calculate profit
    })
</script>

<div class="relative flex flex-col md:flex-row md:items-center gap-6 mb-6 p-5 bg-white rounded-xl shadow-md border border-gray-200 transition-shadow hover:shadow-lg">    
    <!--create different labels with input fields for user to put in-->
    <div class="flex flex-col md:flex-row gap-4 w-full md:w-auto">
        <label class="flex flex-col text-sm font-medium text-gray-700">
            Principal Amount ($) 
            <input 
                type="number" 
                bind:value={principal} 
                placeholder="Must be > 100" 
                min="100" 
                step="100"
                onkeydown={(e) => {
                    if (e.key !== 'ArrowUp' && e.key !== 'ArrowDown' && e.key !== 'Tab'){
                        e.preventDefault();
                    }
                }}
                class="mt-1 px-4 py-2 caret-transparent cursor-default bg-white border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-slate-500 w-full md:w-40"
                />
        </label>
    
        <label class="flex flex-col text-sm font-medium text-gray-700">
            Interest Rate (%)
            <input 
                type="number" 
                bind:value={rate} 
                step="0.01"
                class="mt-1 px-3 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-slate-500 w-full md:w-28" 
            />
        </label>
    
        <label class="flex flex-col text-sm font-medium text-gray-700">
            # Of Weeks
            <select 
                bind:value={weeks}
                class="mt-1 px-3 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-slate-500 w-full md:w-48"
            >
                <option value={undefined} disabled selected>Select a duration...</option>
                <option value={4}>4 Weeks (1 Month)</option>
                <option value={8}>8 Weeks (2 Months)</option>
                <option value={13}>13 Weeks (3 Months)</option>
                <option value={17}>17 Weeks (4 Months)</option>
                <option value={26}>26 Weeks (6 Months)</option>
                <option value={52}>52 Weeks (1 Year)</option>
            </select>
        </label>
    </div>
    <!--output how much interest an individual would make with the parameters-->
    <div class="w-full md:w-auto md:ml-auto md:pl-8 md:pr-12 md:border-l md:border-gray-300 min-w-[220px] flex flex-col justify-center md:self-stretch md:-my-5 md:py-5">
        {#if principal && rate && weeks}
            <span class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-1">Estimated Profit</span>
            <span class="text-2xl font-extrabold text-green-600">${profit.toFixed(2)}</span>
        {:else}
            <span class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-1">Estimated Profit</span>
            <span class="text-lg font-medium text-gray-400 italic mt-1">Awaiting inputs...</span>
        {/if}
    </div>

    <!--button to delete this specific treasury row-->
    <button 
        onclick={deletefunc} 
        class="absolute top-3 right-3 w-8 h-8 flex items-center justify-center rounded-full bg-red-50 text-red-500 font-bold transition-colors hover:bg-red-600 hover:text-white">
        X
    </button>
</div>
