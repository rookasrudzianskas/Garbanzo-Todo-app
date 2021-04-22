<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">

      <q-input
        v-model="newTask"
        @keyup.enter="addTask"
        placeholder="Add task"
        dense
        bg-color="white"
        class="col"
        square
        filled

      >
        <template v-slot:append>
          <q-btn
            round
            dense
            flat
            icon="add"
            @click="addTask"/>
        </template>


      </q-input>

    </div>
    <q-list
      class="bg-white"
      separator
      >
      <q-item
        v-for="(task, index) in tasks"
        :key="task.title"
        @click="task.done = !task.done"
        :class="{'done bg-blue-1' : task.done}"
        clickable
        v-ripple>
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            class="no-pointer-events"
            color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>

        <q-item-section v-if="task.done" side>
          <q-btn
            @click.stop="deleteTask(index)"
            flat
            dense
            round
            color="primary"
            icon="delete"
            />
        </q-item-section>
      </q-item>
    </q-list>
    <div class="no-tasks absolute-center" v-if="!tasks.length">
      <q-icon name="check" size="100px" color="primary">

      </q-icon>
      <div class="text-h5 text-primary text-center">
        No tasks
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [
        // {
        //   title: 'Get bannanas',
        //   done: false
        // },
        //
        // {
        //   title: 'Get mandarinas',
        //   done: false
        // },
        //
        // {
        //   title: 'Get food',
        //   done: false
        // },
      ]
    }
  },
  methods: {
    deleteTask(index) {

      this.$q.dialog({
        title: 'Confirm',
        message: 'Would you like to delete task?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify('Task deleted')
      })

    },
    addTask() {
      this.tasks.push({
        title:this.newTask,
        done: false
      }),
        this.newTask = ''
    }
  }
}
</script>

<style lang="scss">
.done{
  .q-item__label {
    text-decoration: line-through;
    color: #bbb;
  }
}

.no-tasks {
  opacity: 0.5;
}
</style>
