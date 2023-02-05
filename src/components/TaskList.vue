<template>
    <div class="task-list ">
        <ul class="list-group container">
            <li class="row list-group-item d-flex justify-content-center align-items-center p-5" v-for="item in tarefas"
                :key="item.id" :style="`background-color:${item.color}`">
                <div class="col-md-9 p-2 py-4">
                    <label class="form-check-label mx-2" :for="`tarefa${item.id}`">
                        <input class="form-check-input me-1" type="checkbox" value="" :id="`tarefa${item.id}`"
                            v-model="item.status" @input="updateStatusTask(item.id)">
                        {{ item.id }} - {{ item.name }}
                    </label>
                </div>
                <div class="col-md-3 p-2">
                    <button type="button" class="btn btn-danger" @click="deleteTask(item.id)">Apagar tarefa</button>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'taskList',
    props: 'novaTarefa',
    data() {
        return {
            tarefas: []
        }
    },
    methods: {
        setTasks() {
            localStorage.setItem('tarefas', JSON.stringify(this.tarefas))
        },
        getTasks() {
            this.tarefas = JSON.parse(localStorage.getItem('tarefas'))
        },
        deleteTask(id) {
            let tempTarefas = [];
            this.tarefas.map((item, index) => {
                if (id !== item.id) {
                    item.id = index + 1
                    tempTarefas.push(item)
                }
            })
            this.tarefas = tempTarefas
            /* Acertar os ids */
            this.adjustTaskId()

            this.tarefas = tempTarefas

            this.setTasks()

        },
        adjustTaskId() {
            /* Acertar os ids */
            let tempTarefas = []
            this.tarefas.map((item, index) => {
                item.id = index + 1
                tempTarefas.push(item)
            })
        },
        updateStatusTask(id) {
            this.tarefas.map((item) => {
                if (id === item.id) {
                    item.status = !item.status
                    /* mudar cor */
                    if (item.status === false) {
                        item.color = item.colorNo
                    } else {
                        item.color = item.colorYes
                    }
                }


            })
            this.setTasks()
        }
    },
    beforeMount() {
        setInterval(() => {
            this.getTasks()
        }, 1000);
    },
    computed() {
        this.getTasks()
    }

}
</script>

<style>
.task-list {
    min-height: 80vh;
    font-size: 20px;

}

#tarefa {
    background: var(--cor-secundaria);
}
</style>