<template>
  <!-- Sidebar Menu -->
  <nav class="mt-2">
    <ul class="nav nav-pills nav-sidebar flex-column" data-widget="treeview" role="menu" data-accordion="false">
<!-- 
      <li class="nav-item">
        <nuxt-link :to="{ name: 'admin-dashboard' }" class="nav-link">
          <i class="nav-icon fas fa-tachometer-alt"></i>
          <p>
            Dashboard
          </p>
        </nuxt-link>
      </li>

      <li class="nav-header">
        <h6>CONTENT</h6>
      </li> -->

      <li class="nav-item">
        <nuxt-link :to="{ name: 'admin-pendaftaran' }" class="nav-link">
          <i class="nav-icon fas fa-user"></i>
          <p>
            Pendaftaran
          </p>
        </nuxt-link>
      </li>

      <!-- <li class="nav-item">
        <nuxt-link :to="{ name: 'admin-post' }" class="nav-link">
          <i class="nav-icon fas fa-book-open"></i>
          <p>
            Posts
          </p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'admin-saran' }" class="nav-link">
          <i class="nav-icon fas fa-bacon"></i>
          <p>
            Saran
          </p>
        </nuxt-link>
      </li>

      <li class="nav-header">
        <h6>SETTING</h6>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'admin-user' }" class="nav-link">
          <i class="nav-icon fas fa-users"></i>
          <p>
            Users
          </p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'admin-profile' }" class="nav-link">
          <i class="nav-icon fas fa-book-open"></i>
          <p>
            Set Profile Group
          </p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'admin-informasi' }" class="nav-link">
          <i class="nav-icon fas fa-book-open"></i>
          <p>
            Set Informasi Group
          </p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'admin-statistik' }" class="nav-link">
          <i class="nav-icon fas fa-book-open"></i>
          <p>
            Set Statistik Group
          </p>
        </nuxt-link>
      </li> -->

    </ul>
  </nav>
  <!-- /.sidebar-menu -->
</template>

<script>
export default {

}
</script>

<style scoped>
a.nuxt-link-active {
  background-color: rgba(255, 255, 255, .1);
}
</style>
