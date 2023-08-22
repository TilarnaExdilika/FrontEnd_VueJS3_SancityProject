<template>
    Đây là trang quản lý Roles
</template>

<script>

import { useMenu } from '../../../stores/use-menu';

export default {
    setup() {
        useMenu().onSelectedKeys(['admin-roles']);
    },
}
</script>