<template>
  <div class="list-task p-4">
    <h1>Todo List</h1>
    <div
      v-for="task of tasks"
      :key="task.id"
      class="item-task d-flex align-items-start border-bottom pt-3 pb-4"
    >
      <input
        type="checkbox"
        name="status"
        id="task"
        class="me-2 mt-2 form-check-input"
        :checked="task.isDone"
        @change="toggleTaskCompletion(task)"
      />
      <div class="d-flex flex-column">
        <div class="title-task mb-1 fw-bold">
          <h2 :class="{ 'text-decoration-line-through': task.isDone }">
            {{ task.title }}
          </h2>
        </div>
        <div class="description-task small text-muted fs-5">
          {{ task.description }}
        </div>
        <button @click="deleteTask(task.id)" class="btn btn-danger mt-3">
          Delete
        </button>
      </div>
    </div>
    <p v-if="tasks.length === 0">Belum ada Task</p>
    <div class="action py-2">
      <button
        class="add-button"
        v-if="!isCreating"
        @click="
          emptyForm();
          isCreating = !isCreating;
        "
      >
        Add Task
      </button>
      <div class="add-card" v-else>
        <div class="card mb-2">
          <div class="card-body d-flex flex-column p-0">
            <input
              class="form-control border-0 mb-2"
              placeholder="Title"
              type="text"
              v-model="titleValue"
            />
            <textarea
              class="form-control border-0 small"
              placeholder="Description"
              rows="3"
              v-model="descriptionValue"
            ></textarea>
          </div>
        </div>
        <div class="button-wrapper d-flex">
          <button
            class="btn btn-primary me-2"
            @click="
              submit();
              isCreating = !isCreating;
            "
          >
            Save
          </button>
          <button
            class="btn btn-outline-secondary"
            @click="isCreating = !isCreating"
          >
            Cancel
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";
export default {
  data() {
    return {
      tasks: [
        {
          id: 1,
          title: "Task 1",
          description: "Deskripsi 1",
          isDone: false,
        },
      ],
      isCreating: false,
      titleValue: "",
      descriptionValue: "",
    };
  },
  methods: {
    submit() {
      this.tasks.push({
        id: this.tasks.length + 1,
        title: this.titleValue,
        description: this.descriptionValue,
        isDone: false,
      });
      console.log(this.tasks);
    },
    emptyForm() {
      this.titleValue = "";
      this.descriptionValue = "";
    },
    deleteTask() {
      this.tasks.splice(this.tasks.length - 1, 1);
    },
    toggleTaskCompletion(task) {
      task.isDone = !task.isDone;
    },
  },
};
</script>
