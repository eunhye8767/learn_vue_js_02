<template>
	<div>
		<ul>
			<li v-for="todoItem in todoItems" v-bind:key="todoItem">
				{{ todoItem }}
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

</style>