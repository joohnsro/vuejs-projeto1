<template>
    <ul :id="o.id" class="dropdown-content" v-for="o in config.menusDropdown">
        <li v-for="item in o.itens">
            <a :href="item.url">{{ item.name }}</a>
        </li>
    </ul>
    <ul id="dropdown-logout" class="dropdown-content">
        <li>
            <a :href="config.urlLogout" @click.prevent="goToLogout()">Sair</a>
            <form id="logout-form" :action="config.urlLogout" method="POST" style="display: none;">
                <input type="hidden" name="_token" :value="config.csrfToken"/>
            </form>
        </li>
    </ul>
    <nav>
        <div class="nav-wrapper container">
            <a href="#" class="brand-logo">Financeiro</a>
            <a href="#" data-activates="nav-mobile" class="button-collapse">
                <i class="material-icons">menu</i>
            </a>
            <ul class="hide-on-med-and-down right">
                <li v-for="o in config.menus">
                    <a v-if="o.dropdownId" class="dropdown-button" href="#" :data-activates="o.dropdownId">
                        {{ o.name }} <i class="material-icons right">arrow_drop_down</i>
                    </a>
                    <a v-else :href="o.url">{{ o.name }}</a>
                </li>
                <li>
                    <a class="dropdown-button" href="#!" data-activates="dropdown-logout">
                        <i class="material-icons left">perm_identity</i> {{ config.name }} <i class="material-icons right">arrow_drop_down</i>
                    </a>
                </li>
            </ul>
            <ul id="nav-mobile" class="side-nav">
                <li v-for="o in config.menus">
                    <a :href="o.url">{{ o.name }}</a>
                </li>
            </ul>
        </div>
    </nav>
</template>

<script type="text/javascript">
    export default {
        props: {
            config: {
                type: Object,
                default(){
                    return {
                        name: '',
                        menus: [],
                        menusDropdown: [],
                        urlLogout: '/admin/logout'
                    };
                }
            }
        },
        ready() {
            $(".button-collapse").sideNav();
            $(".dropdown-button").dropdown();
        },
        methods: {
            goToLogout(){
                $("#logout-form").submit();
            }
        }
    }
</script>