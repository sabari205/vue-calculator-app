<template>
	<div class="flex flex-row mb-2 rounded-xl bg-white p-2 cursor-pointer" @click="historyOnClick">
		<div>
			<p>{{ historyItem.expr }}</p>
		</div>
		<div>
			<p>{{ "= " + historyItem.result }}</p>
		</div>
	</div>
</template>

<script>
	export default {
		name: "HistoryListItem",
		props: {
			historyItem: Object
		},
		emits: ['historyClicked'],
		methods: {
			historyOnClick() {
				console.log("List item");
				this.$emit('historyClicked');
			}
		}
	}
</script>