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
	// set editing variables
	let setName = "";
	let setAmount = null;
	let setId = null;
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

	function setModifiedExpense(id) {
		let expense = expenses.find(item => item.id === id);
		console.log(expense);
		setId = expenses.id;
		setName = expenses.name;
		setAmount = expenses.amount;
	}

	setContext('removeExpense', removeExpense);
	setContext('modify', setModifiedExpense);
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
