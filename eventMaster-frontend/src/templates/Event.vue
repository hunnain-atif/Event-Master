<template>
  <Layout>
    <v-container>
      <v-row>
        <v-col sm="6" offset-sm="2">
          <h1>{{ $page.event.title }}</h1>
          <img :src="`http://localhost:1337${$page.event.image}`" />
          <p>{{ $page.event.description }}</p>
        </v-col>
      </v-row>
    </v-container>
  </Layout>
</template>


<page-query>
  query($id: ID!) {
    event(id: $id) {
        id
        title
        duration
        description
        price
        date
        image
    }
}
</page-query>

<script>
export default {
  metaInfo() {
    return {
      title: this.$page.event.title,
    };
  },
};
</script>

<style>
p {
  margin-top: 25px;
  width: 750px;
  text-decoration: none;
  text-align: justify;
  font-size: 1.2rem;
}

img {
  margin-top: 10px;
}

h1 {
  color: #ffa233;
}
</style>
