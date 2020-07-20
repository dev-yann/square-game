<template>
    <transition name="slide-enter">
        <div class="square" v-if="show" v-bind:style="{ top: square.top + 'px', left: square.left + 'px', height: square.height + 'px', width: square.width + 'px', backgroundColor: square.color}"
             @click.prevent="divide"></div>
    </transition>
</template>

<script>
    export default {
        name: "Square",
        props: ['square', 'index'],
        data() {
            return {
                show: false
            }
        },
        mounted() {

            this.show = true

        },

        methods: {

            divide: function () {
                this.$emit('divide', this.index);
            },

        }
    }
</script>

<style scoped>
    .square {
        position: absolute;
        background-color: red;
    }

    .slide-enter-enter-active {
        transition: all .3s ease;
    }

    .slide-enter-leave-active {
        transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
    }

    .slide-enter-enter, .slide-fade-leave-to {
        transform: translateY(-150px);
        opacity: 0;
    }
</style>