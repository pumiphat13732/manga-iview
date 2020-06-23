<template xmlns:Col="http://www.w3.org/1999/html">
  <div class="container">
    Manga Search Page
    <Input v-model="query" placeholder="Enter something..." style="width: 100%"/>
    <Button type="primary" style="margin-top:20px " @click="handleSearchManga()">Search Manga</Button>
    <Divider></Divider>
    <Row :gutter="16" type="flex" justify="center">
      <Col v-for="manga in results" :key="manga.mal_id" style="width: 300px; margin-top: 10px"
           @click="handleMangaClick(manga)">
        <div @click="handleMangaClick(manga)">
          <Card>
            <p slot="title">{{manga.title}}</p>
            <Row>
              <Col :span="16">
                <p style="width: 100%;">
                  {{manga.synopsis}}
                </p>
              </Col>
              <Col :span="8">
                <img :src="manga.image_url" alt="" style="width: 40px;"/>
              </Col>
            </Row>
          </Card>
        </div>
      </Col>
    </Row>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    data() {
      return {
        query: 'Dragon',
        results: []
      }
    },
    methods: {
      handleSearchManga() {
        console.log('search manga key', this.query)
        const url = `https://api.jikan.moe/v3/search/manga?q=${this.query}}&page=1`
        console.log('URL', url)
        axios.get(url).then(response => {
          console.log(response)
          this.results = response.data.results
          console.log('THIS.RESULTS', this.results)
        })
      },
      handleMangaClick(manga) {
        console.log('manga click', manga)
        window.location = manga.url
      }

    }
  }
</script>

<style scoped>
  .container {
    margin: 40px 60px;
  }

</style>
