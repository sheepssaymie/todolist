<template>
	<footer class="footer">
		<span class="todo-count"
			>剩余<strong>{{ count }}</strong></span
		>
		<ul class="filters" @click="fn">
			<li>
				<a
					:class="{ selected: isSel === 'all' }"
					href="javascript:;"
					@click="isSel = 'all'"
					>全部</a
				>
			</li>
			<li>
				<a
					href="javascript:;"
					:class="{ selected: isSel === 'no' }"
					@click="isSel = 'no'"
					>未完成</a
				>
			</li>
			<li>
				<a
					href="javascript:;"
					:class="{ selected: isSel === 'yes' }"
					@click="isSel = 'yes'"
					>已完成</a
				>
			</li>
		</ul>
		<button class="clear-completed" @click="delAll">清除已完成</button>
	</footer>
</template>

<script>
	export default {
		props: ["arr"],
		data() {
			return {
				isSel: "all",
			};
		},
		computed: {
			count() {
				return this.arr.length;
			},
		},
		methods: {
			fn() {
				this.$emit("changeType", this.isSel);
			},
			delAll() {
				this.$emit("clear");
			},
		},
	};
</script>

<style>
</style>