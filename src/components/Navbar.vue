<template>
    <nav class="teal darken-1">
        <div class="nav-wrapper">
            <router-link to="/" class="brand-logo">Задачи</router-link>
              <ul class="right hide-on-med-and-down">
               <li><router-link to="/" exact active-class="active">
                    <a>Создать</a>
                </router-link>
               </li>
                  <li><router-link to="/list" active-class="active">
                    <a>Список задач</a>
                </router-link>
                  </li>
             </ul>
        </div>
    </nav>
</template>

<script>
    export default {
        name: "Navbar"
    }
</script>

<style lang="scss" scoped>
    nav {
        padding: 0 2rem;
    }
</style>