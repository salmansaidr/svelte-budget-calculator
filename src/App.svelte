<script>
	// library
	import { setContext } from 'svelte';
	// Component
	import Navbar from './Navbar.svelte';
	import ExpensesList from './ExpensesList.svelte';
	import Totals from './Totals.svelte';
	import ExpenseForm from './ExpenseForm.svelte';
	// Data
	import expensesData from './expenses';
	// Variables
	let expenses = [...expensesData];
	// Functions
	const removeExpense = id => {
		expenses = expenses.filter(item => item.id !== id);
	};
	const clearExpenses = () => {
		expenses = [];
	};

	function addExpense({ name, amount }) {
		let expense = { id: Math.random() * Date.now(), name, amount }
		expenses = [expense, ...expenses];
	}

	setContext('removeExpense', removeExpense);
	$: total = expenses.reduce((acc, curr) => {
		return (acc += curr.amount);
		} ,0);
</script>

<Navbar />
<main class="content">
	<ExpenseForm {addExpense} />
	<Totals title="total expenses" {total} />
	<ExpensesList {expenses} {removeExpense} />
	<button type="button" class="btn btn-primary btn-block" on:click={clearExpenses}>clear expenses</button>
</main>
