<template>
  <div class="block" v-if="showBlock" @click="stopTimer">
      Click me
  </div>
</template>

<script>
export default {
    props: ['delay'],
    data(){
        return {
            showBlock: false,
            timer: null,
            reactionTime: 0
        }
    },
    methods: {
        startTimer(){
            this.timer = setInterval(() => {this.reactionTime += 10}, 10 )
        },
        stopTimer(){
            clearInterval(this.timer)
            //clear interval é uma função nativa do JS que limpa o timer de setInterval.
            this.$emit('end', this.reactionTime)
            //O primeiro parametro de emit é o nome que pode ser qualquer coisa a ser declarado, já o segundo parametro é qualquer dado(data) que você queira
            //emitir para o componente que está recebendo o evento.
        }
    },
    mounted(){
        //O hook mounted é disparado após o componente ser renderizado, ou seja antes do before create e do created.
        console.log('component mounted')
        setTimeout(() => {
            this.showBlock = true
            this.startTimer()
            console.log(this.delay)
        }, this.delay)
        //setTimeout() é uma função nativa do javascript usada para dispararmos uma função de forma async, ou seja quando usamos o setTimeout() a função só ira dispara quando o tempo delimitado for passado.
        //essa função espera como parametro um objeto que é o que ela irá disparar e depois um tempo que é o 'timer' de quando ela vai disparar.
        //nesse caso nosso 'timer' é uma função definida no elemento pai e passada via props chamada 'delay'.
    },
    updated() {
        //Esse hook é disparado quando qualquer dado (data) dentro do nosso componente é alterado.
        console.log('component updated')
    },
    unmounted(){
        //Esse hook é disparado quando o component for destruido da dom.
        console.log('unmounted')
    }
}

</script>

<style>
    .block {
        width: 400px;
        border-radius: 20px;
        background: green;
        color: white;
        text-align: center;
        padding: 100px 0;
        margin: 40px auto;
    }
</style>