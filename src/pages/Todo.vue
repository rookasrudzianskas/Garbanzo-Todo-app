<template>
  <q-page class="bg-grey-3 column">
    <q-list
      class="bg-white"
      separator
      >
      <q-item
        v-for="task in tasks"
        :key="task.title"
        v-ripple>
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        {
          title: 'Get bannanas',
          done: false
        },

        {
          title: 'Get mandarinas',
          done: false
        },

        {
          title: 'Get food',
          done: false
        },
      ]
    }
  }
}
</script>
