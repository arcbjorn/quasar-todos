/* eslint-disable no-unused-expressions */
<template>
  <q-page padding>
    <div class="row q-mb-lg">
      <q-input
        class="col"
        v-model="newTodo"
        placeholder="Add new task"
        @keyup.enter="addTodo"
      />
      <q-btn
        color="primary"
        label="Add"
        @click.native="addTodo"
      />
    </div>

    <div class="row">
      <div class="q-pa-md col">
        <q-list bordered separator>
          <q-toolbar class="bg-primary text-white shadow-2">
            <q-toolbar-title>Tasks</q-toolbar-title>
          </q-toolbar>
          <q-item
            clickable
            v-ripple
            v-for="todo in todos"
            :key="todo.id"
          >
            <q-item-section>
              <q-item-label>{{ todo.content }}</q-item-label>
            </q-item-section>
            <q-item-section top side>
              <div class="text-grey-8 q-gutter-xs">
                <q-btn
                  class="gt-xs"
                  size="12px"
                  color="green"
                  flat dense round
                  icon="done"
                  @click.native="moveToDone(todo.id)"
                />
              </div>
            </q-item-section>
          </q-item>
        </q-list>

        <q-list class="q-mt-lg" bordered separator >
          <q-toolbar class="bg-primary text-white shadow-2">
            <q-toolbar-title>Done</q-toolbar-title>
          </q-toolbar>
          <q-item
            clickable
            v-ripple
            v-for="todo in done"
            :key="todo.id"
          >
            <q-item-section>
              <q-item-label>{{ todo.content }}</q-item-label>
            </q-item-section>
            <q-item-section top side>
              <div class="text-grey-8 q-gutter-xs">
                <q-btn
                  class="gt-xs"
                  size="12px"
                  color="red"
                  flat dense round
                  icon="close"
                  @click.native="deleteTodo(todo.id)"
                />
              </div>
            </q-item-section>
          </q-item>
        </q-list>

      </div>
    </div>
  </q-page>
</template>

<script lang="ts">
import { Todo, Meta } from 'components/models';
import ExampleComponent from 'components/ClassComponent.vue';
import { Vue, Component, Emit } from 'vue-property-decorator';

@Component({
  components: { ExampleComponent },
})
export default class PageIndex extends Vue {
  newTodo = '';

  todos: Todo[] = [];

  done: Todo[] = [];

  meta: Meta = {
    totalCount: 1200,
  };

  @Emit()
  addTodo() {
    const todo: Todo = { id: Math.random(), content: this.newTodo };
    this.todos.push(todo);
    this.newTodo = '';
  }

  @Emit()
  moveToDone(id: number) {
    this.done.push(this.todos.find((t) => t.id === id));
    this.todos = this.todos.filter((t) => t.id !== id);
  }

  @Emit()
  deleteTodo(id: number) {
    this.$q.dialog({
      title: 'Confirm',
      message: 'Really delete?',
      color: 'negative',
      ok: 'Yes, I\'m sure',
      cancel: true,
      default: 'cancel',
    }).onOk(() => {
      this.done.splice(id, 1),
      this.$q.notify('Deleted!');
    });
  }
}
</script>
