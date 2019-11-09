<template>
    <div class="bg" v-if='flag' @click.self="changeflag" id="Usercheck">
        <div class="userbox_a">
            <p>您确定要删除吗？</p>
            <p><a href="#" class="button button-fill"
                @click="del"
                >确定</a></p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Usercheck',
    props: ['flag'],
    methods: {
        changeflag() {
            this.$emit('changeflagdel2')
        },
        del() {
            this.$emit('deltask')
            this.$emit('changeflagdel2')
        }
    },
}
</script>