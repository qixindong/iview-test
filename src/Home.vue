<style scoped>
    .layout-con {
        height: 100%;
        width: 100%;
    }

    .header {
        text-align: center;
    }

    .header-title {
        color: rgba(255, 255, 255, .7);
        margin: 0 auto;
        display: inline-block;
    }

    .content {
        background: #ffffff;
        boxShadow: 0 2px 3px 2px rgba(0, 0, 0, .1)
    }

    .menu-item span {
        display: inline-block;
        overflow: hidden;
        width: 69px;
        text-overflow: ellipsis;
        white-space: nowrap;
        vertical-align: bottom;
        transition: width .2s ease .2s;
    }

    .menu-item i {
        transform: translateX(0px);
        transition: font-size .2s ease, transform .2s ease;
        vertical-align: middle;
        font-size: 16px;
    }

    .collapsed-menu {
        display: none;
    }

    .collapsed-menu span {
        width: 0px;
        transition: width .2s ease;
        display: none;
    }

    .collapsed-menu i {
        transform: translateX(5px);
        transition: font-size .2s ease .2s, transform .2s ease .2s;
        vertical-align: middle;
        font-size: 22px;
    }
</style>
<template>
    <div class="layout">
        <Layout :style="{minHeight: '100vh'}">
            <Sider collapsible :collapsed-width="78" v-model="isCollapsed" class="sider">
                <div class="header"><span class="header-title">Sider Title</span></div>
                <Menu theme="dark" width="auto" :class="menuitemClasses" >
                    <SiderMenu v-for="item in menuList" :icon="item.icon" :name="item.name" v-bind:key="item.key"
                               :content="item.content" :submenu="item.submenu">
                    </SiderMenu>
                </Menu>
            </Sider>
            <Layout>
                <Header class="header content"><span class="header-title" style="color: rgba(105,105,105,0.96);">iView Test</span>
                </Header>
                <Content :style="{padding: '0 16px 16px',width:'100%'}">
                    <Row>
                        <div style="float: left">
                            <Breadcrumb :style="{margin: '16px 0'}">
                                <BreadcrumbItem v-for="item in tabsList" :to="item.url" v-bind:key="item.key" v-if="item.vif">
                                    {{item.title}}
                                </BreadcrumbItem>
                            </Breadcrumb>
                        </div>
                        <div id="userOptions" style="float: right">
                            <User :userInfo="{headPic: 'static/images/tx.png'}"/>
                        </div>
                    </Row>
                    <Tabs type="card" closable @on-tab-remove="handleTabRemove">
                        <TabPane v-for="item in tabsList" :label="item.title" v-if="item.vif" v-bind:key="item.key"
                                 :closable="item.closable"
                                 style="text-align: center;height: 488px">
                            <Scroll style="width: 100%;height: 488px" :height="488">
                                <RouterView style="display: inline-block"></RouterView>
                            </Scroll>
                            <!--<div>
                                <RouterView style="display: inline-block"></RouterView>
                            </div>-->
                        </TabPane>
                    </Tabs>
                </Content>
                <Footer :style="{background: '#fff', boxShadow: '0 2px 3px 2px rgba(0,0,0,.1)'}"
                        style="text-align: center"><span
                    style="display: inline-block">©2019 祁新东 1360817315@qq.com </span>
                </Footer>
            </Layout>
        </Layout>
    </div>
</template>
<script>
    import User from './components/user'
    import SiderMenu from './components/siderMenu'

    export default {
        components: {User, SiderMenu},
        data() {
            return {
                isCollapsed: false,
                menuList: [
                    {
                        key: 0,
                        name: 'menu1',
                        content: 'menu1',
                        icon: 'ios-navigate',
                        submenu: [
                            {
                                key: 0,
                                name: 'submenu1-1',
                                url: '/Page1',
                                icon: 'ios-navigate',
                                content: 'submenu1-1',
                            }
                        ]
                    },
                ],
                tabsList: [
                    {
                        key: 0,
                        url: '/',
                        closable:false,
                        vif: true,
                        title: 'Home'
                    },
                    {
                        key: 1,
                        url: '/Page1',
                        closable:true,
                        vif: true,
                        title: 'another page'
                    }]
            };
        },
        computed: {
            menuitemClasses: function () {
                return [
                    'menu-item',
                    this.isCollapsed ? 'collapsed-menu' : ''
                ]
            }
        },
        methods: {
            handleTabRemove(key) {
                this.tabsList[key].vif=false;
            }
        }
    }
</script>
