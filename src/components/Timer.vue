<template>
    <div id="timer">
        <h2 >{{timeShow}}</h2>
    </div>
</template>

<script>
    export default {
        name: 'Timer',
        data () {
            return {
                timeNow: 59,
                timer: null
            }
        },
        props: {
          runTimer: Boolean,
          rightPairs: Number
        },
        methods: {
            startTimer () {
                this.$emit('showTimer');
                this.timer = setInterval(() => {
                    this.timeNow--;
                }, 1000);
            },
            stopTimer () {
                clearInterval(this.timer);
            }
        },
        computed: {
            timeShow () {
                let timeStr = '';
                timeStr = String(this.timeNow);

                if (this.timeNow < 1) {
                    return `00:00`
                } else if (this.timeNow < 10) {
                    return `00:0${timeStr}`;
                } else {
                    return `00:${timeStr}`;
                }
            },

        },
        watch: {
            runTimer (newVal) {
                if (newVal) {
                    this.timeNow = 59;
                    this.startTimer();
                }
            },
            rightPairs () {
                if (this.rightPairs === 6) {
                    this.stopTimer();
                    //modal popupWindow Win;
                    this.$emit('showWindow', ['win', 'Play again']);
                    this.$emit('stopTimer');
                }
            },
            timeNow () {
                if (this.timeNow === 0) {
                    this.stopTimer();
                    //modal popupWindow lose;
                    this.$emit('showWindow', ['lose', 'Try again']);
                    this.$emit('stopTimer');
                }
            }
        }
    }
</script>

<style scoped>
    h2 {
        margin: 30px auto;
        text-align: center;

        font-family: Arial, sans-serif;
        font-size: 32px;
        line-height: 36px;
        color: #434344;
    }
</style>
