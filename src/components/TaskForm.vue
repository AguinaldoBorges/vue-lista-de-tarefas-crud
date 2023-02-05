<template>
    <div class="task-form container-fluid">
        <div class="row p-3">
            <div class="col-12">
                <input type="text" class="form-control" placeholder="Digite aqui, a tarefa que deseja criar"
                    aria-label="First name" v-model="inputTarefa">
            </div>
            <div class="col-lg-6">
                <button class="btn" @click="createTask(inputTarefa)">Adicionar Tarefa</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'taskForm',
    data() {
        return {
            tarefas: [],
            inputTarefa:''
        }
    },
    methods: {
        createTask(nome) {
            let novaTarefa = {
                id: this.tarefas.length+1,
                name: nome,
                status: false,
                color:'#f2f2f2c7',
                colorYes:'#bcf5c1c7',
                colorNo:'#f2f2f2c7'
            }
            this.getTasks()
            this.tarefas.push(novaTarefa)
            this.adjustTaskId()
            localStorage.setItem('tarefas', JSON.stringify(this.tarefas))
            this.inputTarefa = ''
        },
        getTasks(){
            this.tarefas = JSON.parse(localStorage.getItem('tarefas'))
        },
        adjustTaskId(){
             /* Acertar os ids */
            let tempTarefas = []
            this.tarefas.map((item, index)=>{
                    item.id = index + 1
                    tempTarefas.push(item)
            })
        }
    },
    beforeMount() {

    }

}
</script>

<style>
.task-form .row {
    height: 200px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: url('') var(--cor-overlay) no-repeat;
    border-radius: 7px;
}

.task-form button {
    width: 100%;
    background-color: var(--cor-botao-primario);
    color: #f2f2f2;
    height: 60px;
}

.task-form button:hover {
    background-color: var(--cor-botao-primario-hover);
    color: #f2f2f2;
}

.task-form input {
    text-align: center;
}
</style>