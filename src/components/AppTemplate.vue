<template>
  <div class="d-flex justify-space-between top header">
    <div class="d-flex align-center">
      <img src="/icon_alpha.png" class="max-w-16 max-h-16 contain" />
      <div class="title">Terrapino</div>
    </div>
    <div class="w-100"></div>
  </div>
  <div class="p-2">
    <slot></slot>
  </div>
</template>



<style  scoped>
.d-flex {
  display: flex;
}

.justify-space-between {
  justify-content: space-between;
}

.align-center {
  align-items: center;
}

.w-100 {
  width: 100%;
}

#app {
  background: #f5fafe;
}

.top {
  background: #fff;
}

.title {
  padding-left: 1rem;
  font-size: 1.25rem;
  font-weight: 400;
  line-height: 1.75rem;
}

.p-2 {
  padding: 1rem;
}

.header {
  padding: .25rem;
}

.max-w-16 {
  max-width: 4rem;
}

.max-h-16 {
  max-height: 4rem;
}

.contain {
  object-fit: contain;
}

img {
  max-width: 100%;
  height: auto;
}

</style>
