<template>
  <div class="list-task">
    <div
      v-for="task of tasks"
      class="item-task d-flex align-items-start border-bottom pt-3 pb-4"
    >
      <input
        type="checkbox"
        name="status"
        id="task"
        class="me-2 mt-2"
        :checked="task.isDone"
      />
      <div class="d-flex flex-column">
        <div class="title-task mb-1">
          {{ task.title }}
        </div>
        <div class="description-task small text-muted">
          {{ task.description }}
        </div>
      </div>
    </div>
    <div class="action py-2">
      <button
        class="add-button"
        v-if="!isCreating"
        @click="isCreating = !isCreating"
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
          <button class="btn btn-primary me-2" @click="submit">Save</button>
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
          title: "Task 1",
          description: "ini deskripsi",
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
        title: this.titleValue,
        description: this.descriptionValue,
        isDone: false,
      });
      console.log(this.tasks);
    },
  },
};
</script>
