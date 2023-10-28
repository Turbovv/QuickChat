<template>
    <div>
        chat {{ user.name }}
    </div>
</template>

<script>
import {mapState} from 'vuex'
export default {
    middleware: ['chat'],
    head() {
        return {
            title: `Room Id ${this.user.room}`
        }
    },
computed: mapState(["user"])
}
</script>