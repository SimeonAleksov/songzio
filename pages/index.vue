<template>
  <div class="main" @click="handleStart">
    <h1>Start a trivia game now!</h1>
    <Button> Start </Button>
  </div>
</template>

<script>
import Button from "@/components/shared/Button";
export default {
  name: "IndexPage",
  components: { Button },
  methods: {
    handleStart() {
      this.$router.push("game/create");
    },
  },
};
</script>
<style lang="scss"></style>
