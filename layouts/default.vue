<template>
<v-app app dark>
    <v-navigation-drawer app v-model="drawer">
        <v-list subheader>
            <v-subheader>Recent Chat</v-subheader>
            <v-list-tile v-for="u in users" :key="u.id"  @click.prevent>
                <v-list-tile-content>
                    <v-list-tile-title>{{ u.name }}</v-list-tile-title>
                </v-list-tile-content>

                <v-list-tile-action>
                    <v-icon :color="u.id === 2 ? 'primary' : 'grey'">chat_bubble</v-icon>
                </v-list-tile-action>
            </v-list-tile>
        </v-list>
    </v-navigation-drawer>
    <v-toolbar app>
        <v-toolbar-side-icon @click="drawer = !drawer"></v-toolbar-side-icon>
        <v-btn icon @click="exit">
            <v-icon>arrow_back</v-icon>
        </v-btn>
        <v-toolbar-title>Chat Room {{ user.room }}</v-toolbar-title>
    </v-toolbar>
    <v-content>
        <div>
            <nuxt />
        </div>
    </v-content>
</v-app>
</template>

<script>
import {mapState, mapMutations} from 'vuex'
export default {
    data() {
        return {
            drawer: true,
            users: [
              {id:1, name: 'User 1'},
              {id:2, name: 'User 2'}
            ]
        }
    },
    computed: mapState(['user']),
    methods: {
      ...mapMutations(['clearData']),
        exit() {
          this.$router.push('/?message=leftChat')
          this.clearData();

        }
    }
};
</script>
