<template>
	<div>
		<ul>
			<li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem.item" class="shadow">
				<i class="checkBtn fas fa-check" 
					v-bind:class="{checkBtnCompleted: todoItem.completed}" 
					v-on:click="toggleComplate(todoItem)"></i>
				<span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
				<span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
					<i class="fas fa-trash-alt"></i>
				</span>
			</li>
		</ul>
	</div>
</template>

<script>
export default {
	props: ['propsdata'],
	methods: {
		removeTodo: function(todoItem, index) {
			// console.log('remove items');
			// console.log(todoItem, index);
			
			// 로컬스토리지의 정보 삭제
			localStorage.removeItem(todoItem);
			
			// 화면 영역 li 삭제
			// 해당 인덱스 번호부터 1번째 자리까지 삭제
			this.todoItems.splice(index, 1);
		},
		toggleComplate: function(todoItem) {
			// console.log(todoItem);
			todoItem.completed = !todoItem.completed;
			
			// 로컬 스토리지의 데이터 갱신
			// 기존의 정보를 삭제한다 (로컬스토리지에서는 업데이트 해주는 기능이 없다)
			localStorage.removeItem(todoItem.item);
			localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
		}
	},
}
</script>

<style scoped>
ul {
	list-style-type: none;
	padding-left: 0px;
	margin-top: 0;
	text-align: left;
}
li {
	display: flex;
	min-height: 50px;
	height: 50px;
	line-height: 50px;
	margin: .5rem 0;
	padding: 0 .9rem;
	background: #fff;
	border-radius: 5px;
}
.removeBtn {
	margin-left: auto;
	color: #de4343;
}
.checkBtn {
	line-height: 45px;
	color: #62acde;
	margin-right: 5px;
}
.checkBtnCompleted {
	color: #b3adad;
}
.textCompleted {
	text-decoration: line-through;
	color: #b3adad;
}
</style>