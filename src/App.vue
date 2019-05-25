<template>
	<div id="app">
		<h1>Tarefas</h1>
		<status-bar>
			<div class="status" :style="{'width': progress}"></div>
		</status-bar>
		<span>{{ progress }}</span>
		<input-task />

		<Tasks>			
			<Task :task='task' slot="task" v-for="task in tasks" :key="task.id">
				<div slot="content" class="task-header">
					<div>
						<div @click="markAsDone(task)" class="check-area"><span class="check"></span></div>
						<button @click="removeTask(task)">X</button>
					</div>
				</div>
				
			</Task>
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
				tasks: [
					{id: 1, description: 'Mussum Ipsum, cacilds vidis litro abertis.', done: true},
					{id: 2, description: 'A ordem dos tratores não altera o pão duris.', done: false},
					{id: 3, description: 'Per aumento de cachacis, eu reclamis', done: false},
					{id: 4, description: 'Suco de cevadiss deixa as pessoas mais interessantis.', done: true},
					{id: 5, description: 'Delegadis gente finis, bibendum egestas augue arcu ut est.', done: true},
					{id: 6, description: 'Per aumento de cachacis, eu reclamis.', done: false},
					{id: 7, description: 'Copo furadis é disculpa de bebadis, arcu quam euismod magna', done: true},
					{id: 8, description: 'Mussum Ipsum, cacilds vidis litro abertis. Mé faiz elementum girarzis, nisi eros vermeio.', done: true},
					],
			}
		},
		methods: {
			markAsDone(task) {
				if(task.done) return;
				task.done = true
			},
			removeTask(task){
				//event.stopPropagation()
				this.tasks.splice(this.tasks.indexOf(task),1)
				//console.log(this.tasks.indexOf(task))
			}
		},
		computed: {
			progress() {
				let count = 0
				if(!this.tasks.length) 
					return '0%'
				else {
					this.tasks.forEach(task => {
						if(task.done)
							count++
					})
					return Math.round(count * 100 / this.tasks.length) + '%'
				}
			}
		},
		created() {
			Buzz.listenEvent('newTask', task => {
				const sameName = t => t.description === task.description

				const taskNotExist =  this.tasks.filter(sameName).length === 0
				
				if(taskNotExist)
					this.tasks.unshift(task)
			})
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
		/* height: 100vh; */
		width: 80vw;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 300;
		font-size: 3rem;
	}
</style>
