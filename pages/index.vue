<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6></v-flex>

    <v-btn @click="message">
      NEW MESSAGE
    </v-btn>

  </v-layout>
</template>

<script>
export default {
  components: {},
  sockets: {
    connect: function() {
      console.log("socket connected");
    }
  },
  methods: {
    message() {
      this.$socket.emit("createMessage", {
        text: "FROM CLIENT"
      });
    }
  }
};
</script>
