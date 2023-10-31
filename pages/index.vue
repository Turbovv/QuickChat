<template>
<v-layout column justify-center align-center>
    <v-flex xs12 sm8>
        <v-card min-width="400">
            <v-snackbar v-model="snackbar" :timeout="6000" top>
            {{ message }}
            <v-btn color="pink" flat @click="snackbar = false">Close</v-btn>
        </v-snackbar>


            <v-card-title>
                <h1>Nuxt Chat</h1>
            </v-card-title>
            <v-card-text>

                <v-form ref="form">
                    <v-text-field v-model="name" :counter="16" :rules="nameRules" label="Name" required></v-text-field>

                    <v-text-field v-model="room" :rules="roomRules" label="Enter Room" required></v-text-field>

                    <div class="d-flex flex-column">
                        <v-btn color="primary" class="mt-4" block @click="submit">
                            Enter
                        </v-btn>
                    </div>
                </v-form>
            </v-card-text>

        </v-card>
    </v-flex>
</v-layout>
</template>

<script>
import {
    mapMutations
} from 'vuex'
export default {
    layout: 'empty',
    head: {
        title: 'Welcome to nuxt chat'
    },
    sockets: {
        connect: function () {
            console.log("socket connected");
        }
    },
    data: () => ({
        valid: true,
        snackbar: false,
        message: "",
        name: "",
        nameRules: [
            v => !!v || "Name is required",
            v => (v && v.length <= 16) || "Name must be less than 16 characters",
        ],
        room: "",
        roomRules: [
            v => !!v || "Room ID is required"
        ]
    }),
    mounted() {
        const {message} = this.$route.query
        if (message === "noUser") {
            this.message = "Enter data"
        } else if (message === 'leftChat') {
            this.message = "You have left the chat"
        }

        this.snackbar = !!this.message
    },
    methods: {
        ...mapMutations(['setUser']),
        submit() {
            if (this.$refs.form.validate()) {
                const user = {
                    name: this.name,
                    room: this.room
                };

                this.$socket.emit('userJoined', user, data => {
                if (typeof data === 'string') {
                    console.error(data)
                } else {
                    user.id = data.userId
                    this.setUser(user);
                    this.$router.push('/chat')
                }
                })

            }
        },
    },
}
</script>
