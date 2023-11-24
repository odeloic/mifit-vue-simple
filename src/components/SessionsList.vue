<template>
  <div id="sessions-list">
    <ul class="sessions-list">
      <li v-for="session in sessions">
        <a @click="$emit('showSession', session.id)"
          >{{
          <span>`session-#${session.id}`</span>
          }}</a
        >
        ' - '
        <a @click="$emit('deleteSession', session.id)">Delete session</a>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: 'SessionsList',
  props: ['sessions'],
};
</script>
<style scoped>
ul li {
  list-style: none;
}

a {
  text-decoration: underline;
  cursor: pointer;
}
</style>
