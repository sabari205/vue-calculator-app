<template>
	<div :class="classes">
		<textarea 
			class="resize-none w-full border-2 border-gray-200 rounded-xl text-xl px-2 py-1 text-right"
			disabled
			rows="1"
			:value="expValue">
		</textarea>
	</div>
</template>

<script>
	export default {
		name: 'Display',
		props: {
			expValue: {
				type: String
			},
			dispType: {
				type: String
			}
		},
		data() {
			return {
				classList: [
					"flex",
					"flex-row"
				]
			}
		},
		computed: {
			classes() {
				if (this.dispType === "result") {
					return this.classList.join(" ") + " -mt-1 mb-2";
				} else {
					return this.classList.join(" ");
				}
			}
		}
	}
</script>