<template>
    <div id="app">
        <h1>Tarefas</h1>
        <NewTask @newTask="addTask" />
        <TaskGrid :tasks="tasks"/>
    </div>
</template>

<script>
import NewTask from './components/NewTask'
import TaskGrid from './components/TaskGrid'

export default {
    components: { NewTask, TaskGrid, },

    data() {
        return {
            tasks: [
                {   
                    name: 'Estudar VueJS', 
                    done: false
                },
                {   
                    name: 'Estudar MongoDB',
                    done: false
                },
                {   
                    name: 'Estudar Java',
                    done: true
                }
            ],
        }
    },

    methods: {
        addTask(task) {
            let sameName = t => t.name === task.name;
            let reallyNew = this.tasks.filter(sameName).length == 0;

            if(reallyNew) {
                this.tasks.push({
                    name: task.name,
                    done: false,
                })
            }
        }
    }
}
</script>

<style>
    body {
        font-family: 'Lato', 'sans-serif';
        background: linear-gradient(to right, rgb(22, 34, 42), rgb(48, 96, 115));
        color: #fff;
    }
    
    #app {
        display: flex;
        flex: 1;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100%;
    }

    #app h1 {
        margin-bottom: 5px;
        font-weight: 300;
        font-size: 3rem;
    }
</style>