<template>
  <li>
    <router-link
      :to="`/${index}`"
      :href="page.link.url"
      :title="`This link goes to the \${page.link.text} page`"
      aria-current="page"
      class="nav-link"
     active-class="active"
     
      >{{ page.link.text }}</router-link
    >
  </li>
</template>

<script>
export default {
  props: ["page","index"],
  
};
</script>


