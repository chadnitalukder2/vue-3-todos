<script setup>
//ref and reactive we are same but reactive e multiple data patanu jay
 /* const todo = ref ('testing');
 console.log(todo.value); //'Testing'

 const todoState = reactive({
    todo: "Testing reactive ",
    class: "34",
 });
 console.log(todoState.todo); // 'Testing reactive'*/
//=========================================================
import { defineEmits, reactive} from 'vue';

const emit = defineEmits(["create-todo"]);

const todoState = reactive ({
  todo: "",
  invalid: null,
  errMsg: "",

});

const createTodo = () => {
  todoState.invalid = null;
  if(todoState.todo !== ""){
    emit("create-todo", todoState.todo);
    todoState,todo = "";
    return;
  }
  todoState.invalid = true;
  todoState.errMsg = "Todo value cannot be empty";

}


</script>


<template>
    <div class="input-wrap">
       <input type="text" v-model="todoState.todo">
       <button @click="createTodo()">Create</button>
    </div>
    <!-- <p v-show="todoState.invalid" class="errmsg">{{ todoState.errMsg }} </p> -->
    <p v-if="todoState.invalid" class="errmsg">{{ todoState.errMsg }} </p>  
    <!-- <p class="errmsg">{{ todoState.errMsg }} </p>  -->
</template>

<style lang="scss" scoped>
    .input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid #41b080;

  &:focus-within {
    box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
      0 -2px 4px -2px rgb(0 0 0 / 0.1);
  }

  input {
    width: 100%;
    padding: 8px 6px;
    border: none;

    &:focus {
      outline: none;
    }
  }

  button {
    padding: 8px 16px;
    border: none;
  }
}
</style>