<template>
    <Submenu slot="title" :name="name">
        <template slot="title">
            <Icon :type="icon"/>
            <span>{{content}}</span>
        </template>
        <MenuItem :name="item.name" v-for="item in submenu" v-bind:key="item.key" :to="item.url">
            <Icon :type="item.icon"/>
            <span>{{item.content}}</span>
        </MenuItem>
    </Submenu>
</template>

<script>
    export default {
        props: {
            name: String,
            content: String,
            icon: String,
            submenu: Array
        },
        name: "spiderMenu"
    }
</script>

<style scoped>

</style>
