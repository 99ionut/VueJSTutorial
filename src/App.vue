<template>
  <navbar
        :pages="pages"
        :active-page="activePage"
        :nav-link-click="(index) => activePage = index"
    ></navbar>

    
    <page-viewer 
        :page="pages[activePage]">
    </page-viewer>
</template>

<script>
import PageViewer from './components/PageViewer.vue';
import Navbar from './components/Navbar.vue';

export default {
    components: {
      Navbar,
      PageViewer
    },
    data(){
        return{
            activePage: 0,
            pages: [
            {
                link: {text:"Home", url: "index.html"},
                title:"Hello, Home",
                content:"content hello home"
            },
            {   link: {text:"About", url: "about.html"},
                title:"Hello, About",
                content:"content hello About"
            },
            {
                link: {text:"Contact", url: "contact.html"},
                title:"Hello, Contact",
                content:"content hello heContactContactllo"
            }
            ]
        };
    },
}
</script>
