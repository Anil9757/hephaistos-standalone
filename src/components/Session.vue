<template>
  <div id="create">
    <h2>{{getSessionById(sessionId).name}}</h2><br>
    <div
      v-for="exercise in getExercisesBySessionId(sessionId)"
      :key="exercise.id"
      class="mx-auto"
      outlined
    >
      <v-card>
        <h4><router-view :to="{ name: 'exercise', params: { seId: sessionId, exId: exercise.id } }">{{exercise.title}}</router-view></h4>
      </v-card><br>
    </div>
  </div>
</template>

<script>
import { mapState, mapGetters, mapActions } from "vuex";
import Session from '../components/Session.vue'
export default {
  name: "Module",
  export default {
    data: () => ({
    }),
  computed: {
    ...mapState(["sessions"]),
    ...mapState(["exercises"]),
    ...mapGetters("sessions", ["getSessionById"]),
    ...mapGetters("exercises", ["getExercisesBySessionId"])
  },
  methods: {
    ...mapActions("exercises", ["fetchExercisesForSession"]),
    ...mapActions("sessions", ["fetchSessionsForModule", "fetchSession"]),
  },
  async mounted() {
    this.fetchSession({ id: this.sessionId });
    this.fetchExercisesForSession({ sessionId: this.sessionId });
  }
};
</script>
