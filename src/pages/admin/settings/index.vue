<template>
    Đây là trang quản lý Setting
</template>

<script>

import { useMenu } from '../../../stores/use-menu';

export default {
    setup() {
        useMenu().onSelectedKeys(['admin-settings']);
    },
}
</script>