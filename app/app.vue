<template>
  <div>
    <NuxtRouteAnnouncer />
    <NuxtPage />
  </div>
</template>

<style>
* {
  box-sizing: border-box;
}
html,
body {
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Hanken Grotesk', -apple-system, system-ui, sans-serif;
  color: #111111;
  background: #fafafa;
  -webkit-font-smoothing: antialiased;
}
::selection {
  background: rgba(99, 102, 241, 0.16);
}
</style>
