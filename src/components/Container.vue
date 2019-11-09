<template>
    <section class="content" id="Container">
        <div :class =" ['card',{'bg_img':todo.done}] " v-for ="( todo , index ) in todos" :key="todo.id">
            <div class="card-content">
                <div class="card-content-inner">{{todo.task}}</div>
                <div class="card-content-inner" style="color:darkcyan">{{todo.times}}</div>
            </div>
            <div class="card-footer">
                <button class="button button-success icon icon-check"
                :class="{'button-fill':todo.done}"
                @click='changedone'
                :data-index="todo.id"
                ></button>
                <button class="button button-danger icon icon-remove"
                @click="changeflag"
                :data-index="todo.id"
                ></button>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    name:'Container',
    props: ['todos'],
    methods: {
        changeflag(e) {
            let index=Number(e.target.getAttribute('data-index'))-1
            this.$emit('changeflagdel', index)

        },
        changedone(e) {
            // console.log(e.target)
            let index=Number(e.target.getAttribute('data-index'))-1
            this.$emit('userchangedone', index)
        },
    },
}
</script>