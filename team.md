In the page file:

```vue
<template>
  <div>
    <SectionHead :section="page.acf.section_head" />
    <SectionTeams :section="page.acf.section_teams" :teams="teams"/>
  </div>
</template>
<script>
  export default{
    asyncData:async function({$apiService}){
      //you actually don't need to provide the full url here, asuming you've setup the api base_url for axios in nuxt.config.js
      var page = await $apiService.get('/page/<page-id>').then(res=>{return res.data})
      var teams = await $apiService.get('/team').then(res=>{return res.data})
    }
  }
</script>
```

In the Team Section file:

```vue
<template>
  <div>
    <SingleTeam v-for="(page_team_id, index) in page_team_ids" :key="index" :team="get_team(page_team_id)"/>
  </div>
</template>
<script>
  export default{
    props:['teams', 'section'],
    computed:{
      page_team_ids:function(){
        return this.section.team_ids // or whatever the property of the team_ids array in the page is called, don't know exactly yet, sorry.
      }
    },
    methods:{
      get_team(id){
        return teams.find(x => x.id === id)
      }
    }
  }
</script>
```
