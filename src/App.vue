<script setup>
import { ref, onMounted, computed, watch } from "vue";

const todos = ref([]);
const name = ref('');

const input_content = ref('');
const input = ref(null);

const todos_asc = computed(() =>
  todos.value.sort((a, b) => {
    return b.createdAT - a.createdAT;
  })
);

const addTodo = () => {
	if (input_content.value.trim() === ''	|| input_category.value === null) {
		return 
	}
	console.log("addTodo")
};

watch(name, (newVal) => {
  localStorage.setItem("name", newVal);
});

onMounted(() => {
  name.value = localStorage.getItem("name") || "";
});
</script>

<template>
  <main class="app">
    <section class="greeting">
      <h2 class="title">
        Olá, <input type="text" placeholder="Nome aqui" v-model="name" />
      </h2>
    </section>

    <section class="create-todo">
      <h3>Criar To Do</h3>

      <form @submit.prevent="addTodo">
        <h4>O que ira fazer hoje?</h4>
        <input
          type="text"
          placeholder="e.g. Estudar para prova de sexta"
          v-model="input_content"
        />

        <h4>Escolha uma categoria</h4>

        <div class="options">
          <label>
            <input type="radio" 
									name="category" 
									id="category1" 
									value="business"
									v-model="input_category" />
						<span class="bubble business"></span>
						<div>Trabalho</div>
          </label>

					<label>
            <input type="radio" 
									name="category" 
									id="category1" 
									value="personal"
									v-model="input_category" />
						<span class="bubble personal"></span>
						<div>Pessoal</div>
          </label>
					{{ input_category }}
        </div>
				<input type="submit" value="Add To Do">
      </form>
    </section>

  </main>

</template>