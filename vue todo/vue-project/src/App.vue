<template>
  <div class="container">
    <div class="card">
      <div class="card-header">
        <h2>To-do list</h2>
        <i class="far fa-square"></i>
      </div>
      <div class="card-body">
        <ul class="list-group todo-list">
          <li
            class="
              list-group-item
              d-flex
              justify-content-between
              align-items-baseline
              my-2
            "
            v-for="(item, index) in todolist"
            :key="index"
          >
            {{ item }}
            <div>
              <button class="btn btn-warning align-self-end me-2">Edit</button>
              <button class="btn btn-danger" @click="sil(index)">Delete</button>
            </div>
          </li>
        </ul>
      </div>
      <div class="card-footer">
        <form>
          <input
            type="text"
            class="form-control"
            v-model="todo"
            placeholder="to-do list..."
          />
          <button @click.prevent="send" type="submit">
            <i class="fas fa-plus"></i>
          </button>
        </form>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      todo: "",
      todolist: [],
    };
  },

  methods: {
    send() {
      if (this.todo == "") {
        alert("bos olmaz");
      } else {
        this.todolist.push(this.todo);
        localStorage.setItem('todo',JSON.stringify(this.todolist));
        this.todo = "";

      }
    },
    sil(index) {
      this.todolist.splice(index, 1);
      localStorage.setItem('todo',JSON.stringify(this.todolist))
    },
  },
  created(){
    this.todolist=JSON.parse(localStorage.getItem('todo'))
  }
 
};
</script>


<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  position: relative;
  min-height: 100vh;
  background-color: #181818;
  font-family: Georgia, "Times New Roman", Times, serif;
  text-transform: capitalize;
}

body::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(#ff4f81, #f0f);
  clip-path: circle(20% at right 80%);
}

body::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(#ff4f81, #f0f);
  clip-path: circle(15% at left 20%);
}

.container {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1;
  max-width: 800px;
  margin: auto;
}

.card {
  position: relative;
  width: 90%;
  background: rgba(175, 21, 106, 0.9);
  box-shadow: 20px 20px 50px rgba(0, 0, 0, 0.8);
  border-radius: 5px;
  padding: 20px;
  margin: 50px 0;
  color: #fff;
}

.card-header {
  display: flex;
  align-items: center;
  padding: 10px 0;
  border-bottom: 3px solid #ff4f81;
}

.card-header i {
  margin-left: auto;
  cursor: pointer;
}

.card-body {
  padding: 10px 0;
  height: 300px;
  overflow-y: scroll;
}

.todo-list {
  list-style: none;
}

form {
  padding: 10px 0;
  display: flex;
}

.card-footer input {
  width: 100%;
  font-size: 15px;
  line-height: 30px;
  color: #fff;
  padding: 5px 10px;
  background-color: rgba(255, 255, 255, 0.1);
  border: none;
  border-radius: 5px 0 0 5px;
  text-transform: capitalize;
}

.card-footer input:focus,
.card-footer button:focus {
  outline: none;
}

.card-footer button {
  border-radius: 0px 5px 5px 0;
  background-color: #ff4f81;
  width: 60px;
  font-size: 18px;
  color: #fff;
  border: none;
  cursor: pointer;
}

.card-footer button:hover {
  background-color: #801936;
}
</style>
