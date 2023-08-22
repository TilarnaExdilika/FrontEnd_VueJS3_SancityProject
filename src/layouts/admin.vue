<template>
    <TheHeader/>
    <div class="containter-fluid mt-3">
        <div class="row">
            <div class="col-sm-3 d-none d-sm-flex">
                <!-- ant list -->
                <a-list bordered style="width: 100%;">
                    <TheMenu/>
                    <template #header>
                    <div>BẢNG ĐIỀU KHIỂN</div>
                    </template>
                </a-list>
            </div>

            <div class="col-12 col-sm-9">
                <router-view></router-view>
            </div>
        </div>
    </div>
</template>
<script>
import TheHeader from '../components/TheHeader.vue';
import TheMenu from '../components/TheMenu.vue';

export default {
    components: {
        TheHeader,
        TheMenu
    }
}
</script>