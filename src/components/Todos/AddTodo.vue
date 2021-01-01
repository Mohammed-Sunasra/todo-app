<template>
    <form @submit.prevent="addTodo">
        <div class="form-control">
            <label for="title">Title</label>
            <input id="title" name="title" type="text" v-model="title" />
        </div>
        <div class="form-control">
            <label for="description">Description</label>
            <textarea id="description" rows="5" name="description" v-model="description"></textarea>
        </div>
        <div class="form-control">
            <label for="status">Status</label>
            <select name="status" id="status" v-model="status">
                <option value="todo">Todo</option>
                <option value="inprogress">InProgress</option>
                <option value="onhold">OnHold</option>
                <option value="done">Done</option>
            </select>
        </div>
        <div class="form-control">
            <label for="status">Priority</label>
            <div>
                <input id="low" name="low" type="radio" value="low" v-model="priority" />
                <label for="low">Low</label>
            </div>
            <div>
                <input id="medium" name="medium" type="radio" value="medium" v-model="priority" />
                <label for="medium">Medium</label>
            </div>
            <div>
                <input id="high" name="high" type="radio" value="high" v-model="priority" />
                <label for="high">High</label>
            </div>
        </div>
        <div class="form-control">
            <base-button>Add</base-button>
        </div>
        <div class="form-control">
            <p v-if="invalidInput">Please make sure you enter all the details</p>
        </div>
        <div class="form-control">
            <p v-if="invalidInput">Please make sure you enter all the details</p>
        </div>
    </form>
</template>

<script>
import axios from 'axios'

export default {
    data(){
        return {
            title: '',
            description: '',
            status: '',
            priority: '',
            invalidInput: false,
            errorMessage: ' '
        }
    },
    methods: {
        addTodo(){
            if(this.title === '' || this.description === '' || this.status === null || this.priority === null){
                this.invalidInput = true
                return
            }
        axios.post("https://todo-app-7a0f5-default-rtdb.firebaseio.com/todos.json", {
            title: this.title,
            description: this.description,
            status: this.status,
            priority: this.priority
        }).then(response => {
            if (response.status !== 200){
                throw new Error('Could not save data') 
            }
        }).catch(error => {
            console.log(error)
            this.errorMessage = error
        })

        }
    }
}
</script>

<style scoped>

form {
  margin: 2rem auto;
  max-width: 40rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 2rem;
  background-color: #ffffff;
}

.form-control {
  margin: 0.5rem 0;
}

label {
  font-weight: bold;
}

h2 {
  font-size: 1rem;
  margin: 0.5rem 0;
}

input,
select,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  margin-top: 0.5rem;
}

select {
  width: auto;
}

input[type='checkbox'],
input[type='radio'] {
  display: inline-block;
  width: auto;
  margin-right: 1rem;
}

input[type='checkbox'] + label,
input[type='radio'] + label {
  font-weight: normal;
}

button {
  font: inherit;
  border: 1px solid #0076bb;
  background-color: #0076bb;
  color: white;
  cursor: pointer;
  padding: 0.75rem 2rem;
  border-radius: 30px;
}

button:hover,
button:active {
  border-color: #002350;
  background-color: #002350;
}
</style>