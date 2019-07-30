<template>
    <div style="height: 40px;width: 50px">
        <span style="height: 40px;width: 50px">
            <img :src="userInfo.headPic" height="35px">
            <Dropdown>
                <a href="javascript:void(0)" class="dropdownBtn"><Icon type="ios-arrow-down"></Icon></a>
                <DropdownMenu slot="list">
                    <DropdownItem>个人中心</DropdownItem>
                    <DropdownItem>退出登录</DropdownItem>
                </DropdownMenu>
            </Dropdown>
        </span>
    </div>
</template>

<script>

    export default {
        name: "user",
        props: {
            userInfo: {
                type: Object,
                required: true,
                default: {headPic: '../../static/images/logo.png'}
            }
        }
    }
</script>

<style scoped>
    .dropdownBtn {
        top: 50%; /*偏移*/
        height: 35px;
        position: relative;
    }
</style>
