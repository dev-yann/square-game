<template>
    <div id="app">

        <Square v-for="(square, index) in squares" :key="index" :square="square" :index="index" v-on:divide="divide"/>

    </div>
</template>

<script>
    import Square from './components/Square'

    export default {
        name: 'App',
        components: {
            Square
        },
        data() {
            return {
                squares: [
                    {
                        width: 300,
                        height: 300,
                        top: this.getRandom(0, window.innerHeight - 50),
                        left: this.getRandom(0, window.innerWidth - 50),
                        color: 'blue'
                    }
                ],
                screen: {
                    maxWidth: window.innerWidth - 50,
                    maxHeight: window.innerHeight - 50
                },
                colors: ['blue', 'red', 'yellow', 'grey', 'black']
            }
        },
        methods: {

            getRandom(min, max) {
                min = Math.ceil(min);
                max = Math.floor(max);
                return Math.floor(Math.random() * (max - min)) + min; //The maximum is exclusive and the minimum is inclusive
            },

            divide: function (index) {

                let width = this.squares[index].width;
                // this.squares.splice(index, 1);
                this.squares.splice(index, 1, ...this.generateSquare(width));

                console.log(this.squares);
            },

            generateSquare: function (preWidth) {
                let squareArray = [];

                console.log(this.colors.length);

                for (let i = 0; i <= 3; i++) {
                    squareArray.push({
                        width: preWidth / 4,
                        height: preWidth / 4,
                        top: this.getRandom(0, this.screen.maxHeight),
                        left: this.getRandom(0, this.screen.maxWidth),
                        color: this.colors[this.getRandom(0, this.colors.length)]
                    })
                }

                console.log(squareArray);
                return squareArray;
            }
        }
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        height: 100vh;
        width: 100vw;
        position: relative;
    }
</style>
