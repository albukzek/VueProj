<template>
     <nav class="navbar orange lighten-1">
      <div class="nav-wrapper">
        <div class="navbar-left">
          <a href="#" @click.prevent="$emit('click')">
            <i class="material-icons black-text">dehaze</i>
          </a>
          <span class="black-text">{{ date }}</span> 
        </div>

        <ul class="right hide-on-small-and-down">
          <li>
            <a
                class="dropdown-trigger black-text"
                href="#"
                data-target="dropdown"
                ref="dropdown"
            >
              USER NAME
              <i class="material-icons right">arrow_drop_down</i>
            </a>

            <ul id='dropdown' class='dropdown-content'>
              <li>
                <router-link to="/profile" class="black-text">
                  <i class="material-icons">account_circle</i>Профиль
                </router-link>
              </li>
              <li class="divider" tabindex="-1"></li>
              <li>
                <a href="#" class="black-text" @click.prevent="logout">
                  <i class="material-icons">assignment_return</i>Выйти
                </a>
              </li>
            </ul>
          </li>
        </ul>
      </div>
    </nav>
</template>

<script>
export default {
    data: () =>({
        date : new Date().toLocaleDateString(),
        interval : null,
        dropdown : null
    }),
    methods : {
        logout(){
            console.log('Logout')
            this.$router.push("/login?message=logout")
        }
    },
    mounted(){
        this.interval = setInterval(()=>{
            this.date  = new Date().toLocaleTimeString() //таймер времени в навбаре
        }, 1000)
        // console.log(this.$refs) 
        this.dropdown = M.Dropdown.init(this.$refs.dropdown, {
            constrainWidth: false //значенние из материалайза цсс
        })
    },
    beforeDestroy(){
        clearInterval(this.interval)
        if(this.dropdown && this.dropdown.destroy){ //проверка инициализации дропдавна перед удалением на случай быстрого открытия и закрытия страницы
            this.dropdown.destroy()
        }
       console.log('before destroy') //хук вызывается после закрытия страицы . Использую для удаения часиков и дропдавна
    }
}
</script>