<script>
export default {
    name: 'AppHeader',
    data() {
        return {
            menuLinks: [
                {
                    label: 'Home',
                    routeName: 'home'
                },
                {
                    label: 'About',
                    routeName: 'about'
                },
                {
                    label: 'Posts',
                    routeName: 'posts'
                },
                {
                    label: 'Contact us',
                    routeName: 'contact-us'
                }
            ]
        };
    }
}
</script>

<template>
    <header>
        <nav class="navbar navbar-expand-lg bg-light">
            <div class="container-fluid">
                <a class="navbar-brand" href="#">Navbar</a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav">
                    <li class="nav-item" v-for="link in menuLinks">
                        <router-link class="nav-link active" aria-current="page" :to="{ name: link.routeName }">{{ link.label }}</router-link>
                    </li>
                </ul>
                </div>
            </div>
        </nav>
    </header>
</template>