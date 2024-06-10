<template>
    <nav 
        :class="[`bg-${theme}`, `navbar-${theme}`, 'navbar', 'container', 'navbar-expand-lg']">
        <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
            <li v-for="(page, index) in pages" class="nav-item active" :key="index">
            <a 
                class="nav-link" 
                :class="{active: activePage == index}"
                :href="page.link.url"
                :title="`This link goes to ${page.link.text} page`"
                @click.prevent="navLinkClick(index)"
                >
                {{page.link.text}}
                </a>
            </li>
        </ul>
        </div>
        <button 
            @click="changeTheme"
            >Change mode</button>
    </nav>
</template>
<script>
export default {
    props: ["pages","activePage", "navLinkClick"],
    data(){
        return{
            theme: "dark"
        }
    },
    methods:{
        changeTheme(){
            console.log("change theme");
            this.theme = (this.theme == 'light' ? 'dark' : 'light');
        }
    }
}
</script>


