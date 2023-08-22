<template>
    <div class="containter-fluid">
        <div class="row text-white" style="background-color: rgb(40, 62, 55); padding: 1rem;">
            <div class="col-1 d-flex d-sm-none align-items-center justify-content-center">
                <span @click="showDrawer()">
                  <font-awesome-icon :icon="['fas', 'align-justify']" />
                </span>
            </div>

            <div class="col-10 col-sm-9 d-flex align-items-center justify-content-center justify-content-sm-start">
                <img src="../assets/logo-light.png" alt="logo" height="32" class="ms-3 me-3">
                <span class="d-none d-sm-flex">Quản trị</span>
            </div>

            <div class="col-sm-3 d-none d-sm-flex align-items-center justify-content-sm-end">
                <span>admin</span>
            </div>

            <div class="col-1 d-flex d-sm-none align-items-center justify-content-center">
                <span @click="showDrawer_user()" >
                  <font-awesome-icon :icon="['far', 'user']" />
                </span>
            </div>
        </div>
    </div>
    
    <a-drawer v-model:visible="visible" title="DANH MỤC" placement="left">
      <TheMenu/>
    </a-drawer>

    <a-drawer v-model:visible="visible_user" title="ADMIN" placement="right">
        <p>Some contents...</p>
        <p>Some contents...</p>
        <p>Some contents...</p>
    </a-drawer>

</template>
<script>
import TheMenu from "../components/TheMenu.vue";
import { defineComponent, ref } from "vue";
export default defineComponent({
  components: {
    TheMenu
  },

  setup() {
    const visible = ref(false);
    const visible_user = ref(false);

    const showDrawer = () => {
      visible.value = true;
    };

    const showDrawer_user = () => {
      visible_user.value = true;
    };

    return {
      visible,
      visible_user,
      showDrawer,
      showDrawer_user
    };
  },
});
</script>