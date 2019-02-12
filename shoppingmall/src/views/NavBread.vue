<template>
    <div class="nav-breadcrumb-wrap">
        <div class="container">
            <nav class="nav-breadcrumb">
            <a href="/">Home</a>
            <!-- slot插槽，供其他页面来放内容进去 -->
            <slot name="bread"></slot>
            </nav>
        </div>
    </div>
</template>
<script>
export default {
    
}
</script>
