<template>
    <nav class="bar bar-tab"  id="Footnav">
        <a
        v-for='tab in tabs' :class="[tab.class,type==tab.choose && 'active']" 
        @click="userchoose1(tab.choose)" :key="tab.id"
        >
            <span class="icon icon-emoji"></span>
            <span class="tab-label">{{tab.choose}}</span>
            <span class="badge">{{tab.num}}</span>
        </a>
        <!-- <a class="tab-item external" href="#">
            <span class="icon icon-message"></span>
            <span class="tab-label">UnDone</span>
            <span class="badge">2</span>
        </a>
        <a class="tab-item external" href="#">
            <span class="icon icon-star"></span>
            <span class="tab-label">Finished</span>
            <span class="badge">2</span>
        </a> -->
    </nav>
</template>

<script>
export default {
    name: 'Footnav',
    props: ['tabs', 'type'],
    methods: {
        userchoose1(choose) {
            this.$emit('userchoose', choose)
        }
    },

}
</script>