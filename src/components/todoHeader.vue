<template>
	<header class="header">
		<h1>todos</h1>
		<input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll" />
		<label for="toggle-all"></label>
		<input
			class="new-todo"
			placeholder="输入任务名称-回车确认"
			autofocus
			@keydown.enter="addFn"
			v-model="task"
		/>
	</header>
</template>

<script>
	export default {
		props: ["arr"],
		data() {
			return {
				task: "",
			};
		},
		methods: {
			addFn() {
				if (this.task.trim().length === 0) {
					alert("任务名不能为空");
					return;
				}
				this.$emit("createFn", this.task);
				this.task = "";
			},
		},
		computed: {
			isAll: {
				set(checked) {
					// 只有true / false
					// 9.3 影响数组里每个小选框绑定的isDone属性
					this.arr.forEach((obj) => (obj.isDone = checked));
				},
				get() {
					// 9.4 小选框统计状态 -> 全选框
					// 9.5 如果没有数据, 直接返回false-不要让全选勾选状态
					return (
						this.arr.length !== 0 && this.arr.every((obj) => obj.isDone === true)
					);
				},
			},
		},
	};
</script>

<style>
</style>