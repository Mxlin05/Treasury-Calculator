<script>
    let {deletefunc, profit = $bindable(0)} = $props(); //function and variables passed down from parent. Inplace modifiable object, similar to referece by memory in c
    //default 0 profit. THIS component CANNOT MODIFY deletefunc, it is readonly. bindable creates a pipe to the caller function for remote modification
    //row.profit -> bind:profit -> bindable -> calculator's profit
    let principal = $state() //variables to store user input
    let rate = $state()
    let weeks = $state()
    
    $effect(() => { //tells the DOM to watch for any changes in values to principal rate and weeks
        profit = (principal && rate && weeks) ? principal * (rate / 100) * (weeks / 52) : 0; //run the math to calculate profit
    })
</script>

<div class="row-container">    
    <!--create different labels with input fields for user to put in-->
    <div style="display: flex; gap: 15px;">
        <label>
            Principal Amount ($): 
            <input 
                type="number" 
                bind:value={principal} 
                placeholder="Must be > 100" 
                min="100" 
                step="0.01"/>
        </label>
    
        <label>
            Interest Rate (%):
            <input type="number" bind:value={rate} step="0.01"/>
        </label>
    
        <label>
            Weeks:
            <select bind:value={weeks}>
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
    <div class="profit-bar">
        {#if principal && rate && weeks}
            <p>Estimated Profit: ${profit.toFixed(2)}</p>
        {:else}
            <p style="color: gray;"><em>Awaiting inputs...</em></p>
        {/if}
    </div>

    <!--button to delete this specific treasury row-->
    <button onclick={deletefunc} class="btn btn-danger" style="margin-left: auto;">Delete</button>
</div>
