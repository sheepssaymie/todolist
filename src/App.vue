<template>
	<div id="app">
		<Header @createFn="newFn" :arr="showArr"></Header>
		<Main :arr="showArr" @delFn="del"></Main>
		<Footer :arr="showArr" @changeType="changeFn" @clear="clearFn"></Footer>
	</div>
</template>

<script>
	import "./styles/base.css";
	import "./styles/index.css";

	import Header from "./components/todoHeader.vue";
	import Main from "./components/todoMain.vue";
	import Footer from "./components/todoFooter.vue";

	export default {
		data() {
			return {
				list: JSON.parse(localStorage.getItem("todoList")) || [],
				getSel: "all",
			};
		},
		components: {
			Header,
			Main,
			Footer,
		},
		methods: {
			newFn(taskName) {
				let newId =
					this.list.length == 0 ? 100 : this.list[this.list.length - 1].id + 1;
				this.list.push({
					id: newId,
					name: taskName,
					isDone: false,
				});
			},
			del(delId) {
				let index = this.list.findIndex((obj) => obj.id === delId);
				this.list.splice(index, 1);
			},
			changeFn(str) {
				this.getSel = str;
			},
			clearFn() {
				this.list = this.list.filter((obj) => obj.isDone == false);
			},
		},
		computed: {
			showArr() {
				if (this.getSel === "yes") {
					// 显示已完成
					return this.list.filter((obj) => obj.isDone === true);
				} else if (this.getSel === "no") {
					// 显示未完成
					return this.list.filter((obj) => obj.isDone === false);
				} else {
					return this.list; // 全部显示
				}
			},
		},
		watch: {
			list: {
				deep: true,
				handler() {
					// 8.0 只要list变化 - 覆盖式保存到localStorage里
					localStorage.setItem("todoList", JSON.stringify(this.list));
				},
			},
		},
	};
</script>

<style>
</style>
