<template>
  <q-page padding>
    <!-- <example-component
      title="Example component"
      active
      :todos="todos"
      :meta="meta"
    ></example-component> -->
    <div class="row q-mb-lg">
      <q-input class="col" v-model="text" placeholder="Add new task"/>
      <q-btn color="primary" label="Add"/>
    </div>

    <div class="row">
      <div class="q-pa-md col">
        <q-list bordered separator>
          <q-toolbar class="bg-primary text-white shadow-2">
            <q-toolbar-title>Tasks</q-toolbar-title>
          </q-toolbar>
          <q-item clickable v-ripple>
            <q-item-section>
              <q-item-label>Item with caption</q-item-label>
            </q-item-section>
            <q-item-section top side>
              <div class="text-grey-8 q-gutter-xs">
                <q-btn class="gt-xs" size="12px" flat dense round icon="delete" />
                <q-btn class="gt-xs" size="12px" color="green" flat dense round icon="done" />
                <q-btn size="12px" flat dense round icon="more_vert" />
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
import { Vue, Component } from 'vue-property-decorator';

@Component({
  components: { ExampleComponent },
})
export default class PageIndex extends Vue {
  todos: Todo[] = [
    {
      id: 1,
      content: 'ct1',
    },
    {
      id: 2,
      content: 'ct2',
    },
    {
      id: 3,
      content: 'ct3',
    },
    {
      id: 4,
      content: 'ct4',
    },
    {
      id: 5,
      content: 'ct5',
    },
  ];

  meta: Meta = {
    totalCount: 1200,
  };
}
</script>
