<script>
    import { getContext } from 'svelte';
    export let id;
    export let name = '';
    export let amount = 0;
    let displayAmount = false;
    const toggleAmount = () => {
        displayAmount = !displayAmount;
    };
    const removeExpense = getContext('removeExpense');
    const setModifiedExpense = getContext('modify');
</script>

<div>
    <article class="single-expense">
        <div class="expense-info">
            <h2>
                {name}
                <button class="amount-btn" on:click={toggleAmount}>
                    <i class="fas fa-caret-down"></i>
                </button>
            </h2>
            {#if displayAmount}
            <h4>amount : ${amount}</h4>
            {/if}
        </div>
        <div class="expense-buttons">
            <button class="expense-btn edit-btn" on:click={() => setModifiedExpense(id)}>
                <i class="fas fa-pen"></i>
            </button>
            <button class="expense-btn delete-btn" on:click={() => removeExpense(id)}>
                <i class="fas fa-trash"></i>
            </button>
        </div>
    </article>
</div>