<script>
    import CalculatorRow from '$lib/calculatorRow.svelte'; //import calculator row component

    let rows = $state([{id:1, profit:0, principal: undefined}]); //create a variable that holds an array of dictionaries/objects that map an Id:number
    let nextId = 2;
    let total_profit = $derived(rows.reduce((sum,row) => sum + row.profit,0)); //sum is the accumulator, row is the current value, 0 is the initial sum value
    let total_principal = $derived(rows.reduce((sum, row) => sum + (row.principal || 0), 0));
    function addRow(){
        rows.push({id:nextId++, profit:0}); //for each row, add a new instance of calculator row
    }

    function deleteRow(id){ //given a specific id, filter the array of rows and add everything but that ID
        rows = rows.filter(row => row.id !== id);
    }
</script>
<!--p-4 is mobile, sm is tablet, lg is desktop.-->
<main class="max-w-7xl mx-auto p-4 sm:p-6 lg:p-8">
    <h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-2">
        Treasury Calculator
    </h1>

    
    
    <hr class="border-gray-300 mb-6 w-screen relative left-1/2 -translate-x-1/2" />

    <div class="flex flex-col lg:flex-row gap-8 algin-top">
        <div class="flex-1 flex-col gap-4 mb-6">
            {#each rows as row (row.id)}
                <CalculatorRow
                    deletefunc = {() => deleteRow(row.id)} //passes the delete function to give each component a personalized button to delete it
                    bind:profit = {row.profit} //secretely a getter and setter with bindable. 
                    bind:principal = {row.principal}
                />
            {/each}
        </div>

        <div class="w-full lg:w-80">
            <div class="sticky top-8 flex flex-col gap-6 p-6 bg-white rounded-xl shadow-md border border-gray-200">
                <div>
                    <h2 class="text-sm font-bold text-gray-500 uppercase tracking-wide">
                        Total Principal Invested
                    </h2>
                    <p class="text-3xl font-extrabold text-slate-800 mt-1">
                        ${total_principal.toFixed(2)}
                    </p>
                </div>
                
                <div>     
                    <h2 class="text-sm font-bold text-gray-500 uppercase tracking-wide">
                        Total Expected Profit
                    </h2>
                    <p class="text-3xl font-extrabold text-green-600 mt-1">
                        ${total_profit.toFixed(2)}
                    </p>
                </div>
                
                <div class="flex flex-col gap-4">
                    <h3 class="text-lg font-bold text-gray-800 border-b pb-2">Actions</h3>
                    <button onclick={addRow} class="w-full sm:w-auto px-6 py-3 rounded-md font-semibold transition-all duration-200 bg-slate-900 text-white hover:bg-slate-700 shaadow-sm hover:shadow-md">
                        + Add Another Treasury
                    </button>
                </div>

                <div class="mt-2 border-t pt-6">
                    <h3 class="text-sm font-bold text-gray-500 uppercase tracking-wide mb-6">Potential Growth</h3>
                    <div class="flex h-32 w-full">

                        <div class="flex flex-col justify-between items-end pr-2 border-r border-gray-200 text-[10px] font-semibold text-gray-400 w-12 pb-1">
                            <span>${Math.max(total_principal, total_principal + total_profit, 1).toFixed(0)}</span>
                            <span>$0</span>
                        </div>

                        <div class="flex-1 flex items-end justify-around gap-6 border-b border-gray-200 pl-4 pb-1">
                            <div class="relative w-1/2 h-full flex flex-col justify-end items-center group">
                                <span class="absolute -top-6 text-xs font-bold text-slate-800 opacity-0 group-hover:opacity-100 transition-opacity">
                                    ${total_principal.toFixed(0)}
                                </span>
                                <div class="w-full bg-slate-800 rounded-t-md transition-all duration-500 ease-out"
                                     style="height: {total_principal === 0 ? 0: (total_principal / Math.max(total_principal, (total_profit + total_principal), 1)) * 100}%; min-height: 4px;">
                                </div>
                            </div>
    
                            <div class="relative w-1/2 h-full flex flex-col justify-end items-center group">
                                <span class="absolute -top-6 text-xs font-bold text-green-500 opacity-0 group-hover:opacity-100 transition-opacity">
                                    ${(total_principal + total_profit).toFixed(0)}
                                </span>
                                <div 
                                    class="w-full bg-green-500 rounded-t-md transition-all duration-500 ease-out"
                                    style="height: {total_profit === 0 ? 0 : ((total_profit + total_principal) / Math.max(total_principal, (total_profit + total_principal), 1)) * 100}%; min-height: 4px;"
                                ></div>
                            </div>
                        </div>
                        
                    </div>

                    <div class="flex justify-around mt-2">
                        <span class="text-xs font-semibold text-gray-500">Principal</span>
                        <span class="text-xs font-semibold text-gray-500">Profit</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!--svelete specific code that is like a for loop, for each row in rows. (row.id) is essentially a tracking key-->
    

</main>