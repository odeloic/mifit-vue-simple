<template>
  <div>
    <button @click.prevent="createNewSession">Create Session</button>
    <SessionsList
      :sessions="sessions"
      @show-session="activateSession"
      @delete-session="removeSession"
    />
    <SessionDetails
      v-if="activeSession"
      :session="activeSession"
      @update-session="updateSession"
    />
  </div>
</template>
<script>
import SessionsList from './SessionsList.vue';
import SessionDetails from './SessionDetails.vue';
export default {
  name: 'AppHome',
  components: {
    SessionsList,
    SessionDetails,
  },
  props: {},
  data: () => ({
    sessions: [],
    activeSession: undefined,
  }),
  methods: {
    createNewSession() {
      this.sessions.push({
        id: this.sessions.length + 1,
        workouts: [],
      });
    },
    activateSession(id) {
      this.activeSession = this.sessions.find((session) => session.id === id);
    },
    updateSession(session) {
      console.log('cumminggg', session);
      const idx = this.sessions.findIndex(
        (_session) => _session.id === session.id
      );
      this.sessions[idx] = session;
      if (session.id === this.activeSession.id) this.activeSession = session;
    },
    removeSession(sessionId) {
      this.sessions = this.sessions.filter(
        (_session) => _session.id === sessionId
      );
    },
  },
  mounted() {
    console.log('Hello bitches!!!');
  },
};
</script>
<style scoped></style>
