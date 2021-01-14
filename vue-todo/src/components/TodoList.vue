<template>
	<div>
		<ul>
			<li v-for="todoItem in todoItems" v-bind:key="todoItem" class="shadow">
				{{ todoItem }}
				<span class="removeBtn" v-on:click="removeTodo">
					<i class="fas fa-trash-alt"></i>
				</span>
			</li>
		</ul>
	</div>
</template>

<script>
export default {
	//로컬스토리지에서 담을 data 속성을 만든다
	data: function() {
		return {
			todoItems: []
		}
	},
	methods: {
		removeTodo: function() {
			
		}
	},
	created: function() {
		// 로컬스토리지에 저장된 것을 가져온다
		if ( localStorage.length > 0 ) {
			for(var i=0; i < localStorage.length; i++) {
				// 빈 배열에 push=담다
				if(localStorage.key(i) !== 'loglevel:webpack-dev-server') {
					this.todoItems.push(localStorage.key(i));
				}
				// console.log(localStorage.key(i));
			}
		}
	}
}
</script>

<style>
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