<template>
<div id="session-details">
  <h2>You are viewing session-#{{session.id}}</h2>
  <h3>Add new workout</h3>
  <form @submit.prevent="createNewWorkout(newWorkout)">
    <label for="name">Workout name</label>
    <input v-model="newWorkout.name" type="text" />
    <button @click.prevent="createNewWorkout(newWorkout)">Add workout</button>
  </form>
  <h3>Workouts</h3>
  <ul id="session-workouts">
    <li v-for="(workout, idx) in session.workouts">
      <span>{{ workout.name }}</span>
      | 
      <span> {{ workout.status}}</span>
      | 
      <a @click="markAsCompleted(idx)">Set as completed</a>
      | 
      <a @click="removeWorkout(idx)">Delete workout</a>
    </li>
  </ul>
</div>
</template>
<script>
export default {
  name: 'SessionDetails',
  props: ['session'],
  data: () => ({
    newWorkout: {
      name: '',
      status: 'pending'
    }
  }),
  methods: {
    createNewWorkout(workout) {
    this.$emit('updateSession', {
      ...this.session,
      workouts: [
        ...this.session.workouts,
        workout
      ]
    });
    this.newWorkout = {
      name: '',
      status: 'pending'
    }
  },
    removeWorkout(idx) {
      const thisSession = this.session;
      thisSession.workouts.splice(idx, 1);
      this.$emit('updateSession', thisSession);
    },
    markAsCompleted(idx) {
      const workout = this.session.workouts[idx];
      if(workout) {
        workout.status = 'completed';
        this.session.workouts.splice(idx, 1, workout);
      }
    }
  },
  
}