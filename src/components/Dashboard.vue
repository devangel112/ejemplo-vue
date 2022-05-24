<template>
  <b-container>
    <h1>Dashboard</h1>
    <div class="grid">
      <b-card
        title="Card Title"
        img-src="https://picsum.photos/600/300/?image=25"
        img-alt="Image"
        img-top
        tag="article"
        style="max-width: 20rem"
        class="mb-2"
      >
        <b-card-text>
          Some quick example text to build on the card title and make up the
          bulk of the card's content.
        </b-card-text>

        <b-button href="#" variant="primary">Go somewhere</b-button>
      </b-card>
    </div>
  </b-container>
</template>

<script>
export default {};
</script>

<style scoped>
.grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    align-items: center;
}
</style>
