# Vue.js 중급강좌
웹앱 제작으로 배워보는 Vue.js, ES6, Vuex

## 1. Todo App - 프로젝트 소개 및 구성
### 1.1. 뷰 CLI로 프로젝트 생성하기
1. [ 터미널 ] node 버전과 npm 버전 확인 후 CLI 설치한다
```
// node 10.x 버전 이상 (LTS 버전)
node -v
// 6.x 버전 이상
npm -v

// CLI 설치 (Vue CLI 공식문서 참고)
npm install -g @vue/cli
```
<br />

2. 설치가 완료 되면 @vue/cli@버전 확인할 수 있다
```
+ @vue/cli@4.5.10
updated 1 package in 34.824s
```
<br />

3. [  터미널 ] todo 프로젝트 관련 폴더를 생성한다.
```
vue create vue-todo
```
<br />

4. Default - Vue 2 babel, eslint 버전을 클릭한다<br />
![1-1-1](./_images/1-1-1.png)
<br /><br />

5. 설치가 완료되면 cd vue-todo, npm run serve 명령어를 확인할 수 있다<br />
![1-1-2](./_images/1-1-2.png)
<br /><br />

6. vue-todo 로컬서버를 실행시킨다
```
// 1. vue-todo 폴더로 이동
cd vue-todo

// 로컬서버 실행
npm run serve
```
![1-1-3](./_images/1-1-3.png)
<br /><br />

### 1.2. 프로젝트 소개 및 컴포넌트 설계 방법
- 컴포넌트를 작게 분리했을 때(영역별로 컴포넌트 분리) 재사용성이 높아진다<br />
![1-2-1](./_images/1-2-1.png)

<br /><br /><br />

## 2. Todo App - 프로젝트 구현
### 2.1. 컴포넌트 생성 및 등록하기
1. **src/components 에 컴포넌트를 등록**한다
2. components 폴더에 컴포넌트 .vue 파일을 생성하고 <br />
vue 자동완성 기능을 통해 기본 구성(template, script, style)을 맞춰준다<br />
![2-1-1](./_images/2-1-1.png)<br />

3. src/App.vue 파일에 생성한 컴포넌트 파일을 script 영역에 연결(import)해준다
```
<template>
	<div id="app">
		<TodoHeader></TodoHeader>
		<TodoInput></TodoInput>
		<TodoList></TodoList>
		<TodoFooter></TodoFooter>
	</div>
</template>

<script>
// 컴포넌트 등록
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
	components: {
		// 컴포넌트 태그명 : 컴포넌트 내용
		'TodoHeader' : TodoHeader,
		'TodoInput' : TodoInput,
		'TodoList' : TodoList,
		'TodoFooter' : TodoFooter,
	}
}
</script>

<style>
</style>
```

4. 브라우저에서 확인해보면 컴포넌트별로 등록된 것을 확인할 수 있다<br />
![2-1-2](./_images/2-1-2.png)<br />

<br />

### 2.2. 파비콘, 아이콘, 폰트, 반응형 태그 설정하기
- ./public/index.html 에 적용한다
	1. 반응형 메타태그 외에 아래 메타태그 3종이 적용되어 있는 지 확인
		- 뷰포트 < meta name="viewport" content="width=device-width,initial-scale=1.0" >
	```
	<meta charset="utf-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width,initial-scale=1.0">
	```

<br />

### 2.3. TodoHeader 컴포넌트 구현
1. TodoHeader.vue 파일에서 마크업을 한다
```
<template>
	<header>
		<h1>TODO it!</h1>
	</header>
</template>
```
<br />

2. style 값을 적용한다
	- scoped : 뷰 싱글 파일 컴포넌트에서 지원하는 속성
		- 해당 컴포넌트 아래에서만 존재하는(유효한) style 적용<br />
		동일한 곳, 클래스명, 아이디명 이라 하더라도 해당 컴포넌트에 포함되어 있지 않으면 상속되지 않는다.
```
<style scoped>
	h1 {
		color: #2f3b52;
		font-weight: 900;
		margin: 2.5rem 0 1.5rem;
	}
</style>
```
<br />

### 2.4. TodoInput 컴포넌트의 할 일 저장 기능 구현
1. 인풋박스에 입력된 내용을 받기 위해 v-model 디렉티브를 이용한다
2. v-model을 사용하기 위해 script 에 data 속성 newTodoItem을 추가하여 인풋박스 v-mdodel과 연결한다
```
<template>
	<div>
		<input type="text" v-model="newTodoItem">
	</div>
</template>
```
```
export default {
	data: function() {
		return {
			newTodoItem: "",
		}
	}
}
```
![2-4-1](./_images/2-4-1.png)<br />
<br />

3. add 버튼을 만들고 addTodo 이벤트를 연결한다.<br />
연결된 이벤트를 script - methods 속성에 addTodo 함수를 만든다
```
<template>
	<div>
		<input type="text" v-model="newTodoItem">
		<button v-on:click="addTodo">add</button>
	</div>
</template>
```
```
export default {
	data: function() {
		return {
			newTodoItem: "",
		}
	},
	methods: {
		addTodo: function() {
			
		}
	}
}
```

4. 버튼을 클릭할 때마다 인풋박스에 입력된 내용이 log에 보이게 적용
```
export default {
	data: function() {
		return {
			newTodoItem: "",
		}
	},
	methods: {
		addTodo: function() {
			console.log(this.newTodoItem);
		}
	}
}
```
![2-4-2](./_images/2-4-2.png)<br />
<br />

5. 인풋박스 입력 후 add 를 클릭한 후에 localStarage(로컬스토리지)에 저장을 한다
	- localStorage.setItem(keyName, keyValue)
	- localStorage에 keyName, keyValue 값을 전달하여 추가하거나 업데이트
```
export default {
	data: function() {
		return {
			newTodoItem: "",
		}
	},
	methods: {
		addTodo: function() {
			// 저장하는 로직
			localStorage.setItem();
		}
	}
}
```

6. setItem에 keyName 과 keyValue 값을 this.newTodoItem 으로 동일하게 적용한다
```
export default {
	data: function() {
		return {
			newTodoItem: "",
		}
	},
	methods: {
		addTodo: function() {
			// 저장하는 로직
			localStorage.setItem(this.newTodoItem, this.newTodoItem);
		}
	}
}
```

7. localStorage(로컬스토리지)에 .setItem() 을 이용해 인풋박스에 입력된 정보를 저장하면 브라우저 개발자도구에서 **Application 패널 탭 -> Storage -> Local Storage 에서 입력된 정보를확인**할 수 있다<br />
![2-4-3](./_images/2-4-3.png)<br />
<br />

8. add 버튼을 누른 후 인풋박스를 초기화시킨다
```
export default {
	data: function() {
		return {
			newTodoItem: "",
		}
	},
	methods: {
		addTodo: function() {
			// 저장하는 로직
			localStorage.setItem(this.newTodoItem, this.newTodoItem);
			this.newTodoItem = ""
		}
	}
}
```
![2-4-4](./_images/2-4-4.png)<br />
<br />

### 2.5. TodoInput 컴포넌트 코드 정리 및 UI 스타일링
1. 인풋박스 입력 -> add 버튼을 클릭하면 인풋박스 초기화 시켜주는 코드를 함수로 생성한다<br />
	- clearInput 메서드 함수를 만들었다
```
export default {
	data: function() {
		return {
			newTodoItem: "",
		}
	},
	methods: {
		addTodo: function() {
			localStorage.setItem(this.newTodoItem, this.newTodoItem);
		},
		clearInput: function() {
			this.newTodoItem = ""
		}
	}
}
```

2. addTodo 메서드 함수에서 this 를 이용하여 clearInput 함수를 실행시켜준다<br />
그러면 아까와 동일한 기능을 적용하게 된다
```
export default {
	data: function() {
		return {
			newTodoItem: "",
		}
	},
	methods: {
		addTodo: function() {
			localStorage.setItem(this.newTodoItem, this.newTodoItem);
			this.clearInput();
		},
		clearInput: function() {
			this.newTodoItem = ""
		}
	}
}
```

3. UI 스타일링 작업(css 작업)
	- button 에 적용한 v-on 디렉티브를 span에 추가하면 button과 동일한 기능이 적용된다
	- **style** 에 **scoped** 를 적용하여 **해당 컴포넌트 .vue 파일에서만 적용**되게 한다
```
<template>
	<div class="inputBox shadow">
		<input type="text" v-model="newTodoItem">
		<!-- <button v-on:click="addTodo">add</button> -->
		<span class="addContainer" v-on:click="addTodo">
			<i class="fas fa-plus addBtn"></i>
		</span>
	</div>
</template>
```
```
export default {
	data: function() {
		return {
			newTodoItem: "",
		}
	},
	methods: {
		addTodo: function() {
			localStorage.setItem(this.newTodoItem, this.newTodoItem);
			this.clearInput();
		},
		clearInput: function() {
			this.newTodoItem = ""
		}
	}
}
```
```
<style scoped>
input:focus {
	outline: none;
}
.inputBox {
	background: #fff;
	height: 50px;
	line-height: 50px;
	border-radius: 5px;
}
.inputBox input {
	border-style: none;
	font-size: .9rem;
}
.addContainer {
	float: right;
	background: linear-gradient(to right, #6478fb, #8763fb);
	display: block;
	width: 3rem;
	border-radius: 0 5px 5px 0;
}
.addBtn {
	color: #fff;
	vertical-align: middle;
}
</style>
```

4. 수정한 마크업과 css 적용이 되었고 기능도 제대로 작동한 것을 확인할 수 있다
![2-5-1](./_images/2-5-1.png)<br />
<br />

5. **인풋박스 입력 후, 엔터를 누르면 엔터버튼을 클릭한 것과 동일한 효과**를 주려고 한다.
	- 인풋박스에 v-on:keyup.enter 이벤트 기능을 추가하고 addTodo 메서드 함수를 연결해준다
```
<template>
	<div class="inputBox shadow">
		<input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
		<!-- <button v-on:click="addTodo">add</button> -->
		<span class="addContainer" v-on:click="addTodo">
			<i class="fas fa-plus addBtn"></i>
		</span>
	</div>
</template>
```