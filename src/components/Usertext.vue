<template>
    <div class="bg" v-if='textflag' @click.self="changetextflag" id="Usertext">
        <div class="userbox">
            <p>请输入您的计划：</p>
            <input type="text" @keyup.enter="writetext">
        </div>
    </div>
</template>

<script>


export default {
    name: 'Usertext',
    props: ['textflag'],
    mounted() {
        
    },
    methods: {
        changetextflag() {
            this.$emit('changetext2')
        },
        writetext(e) {
            this.$emit('userwrite', e.target.value)
            this.$emit('changetext2')
        }
    }
}
</script>