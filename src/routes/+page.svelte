<script>
    import CalculatorRow from '$lib/calculatorRow.svelte'; //import calculator row component

    let rows = $state([{id:1, profit:0}]); //create a variable that holds an array of dictionaries/objects that map an Id:number
    let nextId = 2;
    let total_profit = $derived(rows.reduce((sum,row) => sum + row.profit,0)); //sum is the accumulator, row is the current value, 0 is the initial sum value

    function addRow(){
        rows.push({id:nextId++, profit:0}); //for each row, add a new instance of calculator row
    }

    function deleteRow(id){ //given a specific id, filter the array of rows and add everything but that ID
        rows = rows.filter(row => row.id !== id);
    }
</script>

<main>
    <h1>Treasury Calculator</h1>
    <h2 style="color: green;">Total Expected Profit: ${total_profit.toFixed(2)}</h2>
    <hr style="margin-bottom: 20px;" />
    <!--svelete specific code that is like a for loop, for each row in rows. (row.id) is essentially a tracking key-->
    {#each rows as row (row.id)}
        <CalculatorRow
            deletefunc={() => deleteRow(row.id)} //passes the delete function to give each component a personalized button to delete it
            bind:profit={row.profit} //secretely a getter and setter with bindable. 
        />
    {/each}

    <button onclick={addRow} class="btn btn-primary">+ Add Another Treasury</button>
</main>