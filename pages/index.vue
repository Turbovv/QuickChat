<template>
<v-layout column justify-center align-center>
    <v-flex xs12 sm8>
        <v-card min-width="400">

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
export default {
    layout: 'empty',
    sockets: {
        connect: function () {
            console.log("socket connected");
        }
    },
    data: () => ({
        name: '',
        nameRules: [
            v => !!v || 'Name is required',
            v => (v && v.length <= 16) || 'Name must be less than 16 characters',
        ],
        room: "",
        roomRules: [
            v => !!v || "Room ID is required"
        ]
    }),

    methods: {
        async submit() {
            const {
                valid
            } = await this.$refs.form.validate()

            if (valid) alert('Form is valid')
        },
    },
}
</script>
