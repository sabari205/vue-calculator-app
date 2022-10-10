<template>
	<div class="flex flex-col ml-10 mt-10">
		<div class="mb-2 text-center text-sm md:text-xl font-bold font-sans">
			<h1>History</h1>
		</div>
		<div class="flex flex-col-reverse">
			<HistoryListItem 
				v-for="(historyItem, index) in historyList" 
				:historyItem="historyItem"
				:key="index"
				@historyClicked="onHistoryItemClick(index)"
			/>
		</div>
	</div>
</template>

<script>
	import HistoryListItem from './HistoryListItem.vue';

	export default {
		name: "History",
		props: {
			historyList: Object
		},
		emits: ['historyClick'],
		components: {
			HistoryListItem
		},
		methods: {
			onHistoryItemClick(index) {
				console.log("List item ", index);
				this.$emit('historyClick', index);
			}
		}
	}
</script>