<!-- Please remove this file from your project -->
<template>
  <div>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.1.2/dist/tailwind.min.css" rel="stylesheet">
    <div>

    <b-form @submit="onSubmit">
<b-form-input v-model="text" placeholder="Search"></b-form-input>

</b-form>


  <b-container class="bv-example-row">
  <b-row>
    <b-col cols="8">

<div class="mt-5">
{{main.id.videoId}}

 <iframe width="560" height="315" :src="'https://www.youtube.com/embed/'+main.id.videoId" :title="main.snippet.title" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

{{main.snippet.title}}
{{main.snippet.description}}

</div>

    </b-col>


    <b-col>
<div class="mt-5" v-for="(extra,index) in extras" :key="extra.id.videoId">

  <iframe width="260" height="65" :src="'https://www.youtube.com/embed/'+extra.id.videoId" :title="videos[0].snippet.title" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>{{extra.snippet.title}}

</div>

    </b-col>
  </b-row>
</b-container>


    </div>
  </div>
</template>

<script>
export default {
  name: 'NuxtTutorial',
  data: () => ({
    text: '',
    videos: [],
    main: null,
    extras: null,
  }),
      methods: {
      async onSubmit(event) {


           event.preventDefault();
        const result = await this.$axios.$get(`https://www.googleapis.com/youtube/v3/search?part=snippet&maxResults=6&q=${this.text}&key=AIzaSyAkr0nTbprhqbE15xjm0bcEcwb59sDx_7E`)

        this.videos = result.items

        console.log(this.videos)

        this.main = this.videos[0]

      if(this.videos.length > 1) {
        this.extras = this.videos.slice(1)
      }

        console.log(this.videos)
      }
    }


}
</script>
