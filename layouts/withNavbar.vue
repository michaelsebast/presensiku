<template>
    <div>
        <CurvedBottomNavigation foreground-color="#f3f4f6" background-color='#1e74d6' icon-color="#ffffff" :options="options" v-model="selected" />
        <h1>Halo</h1>
        <nuxt/>
    </div>
</template>

<script>

  import { CurvedBottomNavigation } from "bottom-navigation-vue";

  export default {
    components: { CurvedBottomNavigation },
    data: () => ({
      selected: 3,
      options: [
        { 
          id: 1, icon: "fas fa-home", 
          title: "Beranda",
          path: { name: "index"},
        },
        {
          id: 2,
          icon: "riwayat",
          title: "Riwayat",
          path: { name: "scan"},

        },
        {
          id: 3,
          icon: "fas fa-barcode-read",
          title: "Scan",
          path: { name: "scan"},
        },
        { 
          id: 4, 
          icon: "fas fa-plus", 
          title: "Presensi",
          childs: [
            { 
              id: 101, 
              icon: "sakit", 
              title: "Sakit",
              path: { name: "index"},
            },
            { id: 101, icon: "izin", title: "Izin" },
          ],
        },
        { 
          id: 5, 
          icon: "fas fa-user", 
          title: "Profil",
        },
      ],
    }),
  };

</script>

<style scoped>
@import 'https://pro.fontawesome.com/releases/v5.10.0/css/all.css';

html{
  font-family:Inter,ui-sans-serif,system-ui,-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Helvetica Neue,Arial,Noto Sans,sans-serif,Apple Color Emoji,Segoe UI Emoji,Segoe UI Symbol,Noto Color Emoji
}
</style>
``