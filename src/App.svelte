<script>
	// Component
	import Navbar from './Navbar.svelte';
	import ExpensesList from './ExpensesList.svelte';
	// Data
	import expensesData from './expenses';
	// Variables
	let expenses = [...expensesData];
	// Functions
	const removeExpense = id => {
		expenses = expenses.filter(item => item.id !== id);
	};
</script>

<Navbar />
<main class="content">
	<ExpensesList {expenses} {removeExpense} />
</main>
