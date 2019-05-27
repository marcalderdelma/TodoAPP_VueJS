<template>
	<div id="app">
		<h1>Tarefas</h1>
		<status-bar>
			<div class="status" :style="{'width': progress + '%'}"></div>
		</status-bar>
		<span>{{ progress }}%</span>
		<input-task/>

		<Tasks>
			<template v-if="tasks.length">
				<Task :task='task' slot="task" v-for="task in tasks" :key="task['description']">
					<div slot="content" class="task-header">
						<div>
							<div @click="markAsDone(task)" class="check-area"><span class="check"></span></div>
							<button @click="removeTask(task)">X</button>
						</div>
					</div>				
				</Task>
			</template>
			<template v-else>
				<span>Você está em dia :)</span>
			</template>
		</Tasks>
	</div>
</template>

<script>
	import StatusBar from '@/components/StatusBar.vue'
	import InputTask from '@/components/Input.vue'
	import Tasks from '@/components/Tasks.vue'
	import Task from '@/components/Task.vue'
	import Buzz from '@/buzz'
	
	export default {
		components: {
			StatusBar,
			InputTask,
			Tasks,
			Task
		},
		data() {
			return {				
				tasks: [],
			}
		},
		methods: {
			markAsDone(task) {
				task['done'] = !task['done']
			},
			removeTask(task){
				this.tasks.splice(this.tasks.indexOf(task),1)
			},
			syncLocalStrage() {
				localStorage.setItem('tasksList', JSON.stringify(this['tasks']))
			}
		},
		computed: {
			progress() {
				let taskDone = this.tasks.filter(task => task['done']).length
				let total = this['tasks'].length
				return Math.round(taskDone / total * 100) || 0	
			}
		},
		watch: {
			tasks: {
				deep: true,
				handler() {
					this['syncLocalStrage']()
				}
			}
		},
		created() {
			Buzz.listenEvent('newTask', task => {
				const sameName = t => t.description === task.description

				const taskNotExist =  this.tasks.filter(sameName).length === 0
				
				taskNotExist && this.tasks.unshift(task)
			})

			let data = localStorage.getItem('tasksList')
			data = JSON.parse(data);
			this['tasks'] = Array.isArray(data) ? data : []
		}
	}
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
		color: #a8a8ac;
	}

	#app {
		margin: auto;
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		width: 80vw;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 300;
		font-size: 3rem;
	}
</style>
