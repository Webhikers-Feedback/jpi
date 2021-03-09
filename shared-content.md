For content that is only required in one page, you can do it like this:
In your page file:

```vue
<template>
  <div>
    <SectionHead :section="page.acf.section_head" />
    <SectionTeams :teams="teams"/>
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

And in your team section file:

```vue
<template>
  <div>
    <SingleTeam v-for="(team, index) in teams" :key="index" :team="team"/>
  </div>
</template>
<script>
  export default{
    props:['teams']
  }
</script>
```

For content, that you need globally on multiple pages, such as navbar and footer you can do it like this:
In your `@/store/index.js`  file:

```javascript
export const actions = {
  async nuxtServerInit(vuex, nuxt){
    await this.dispatch('shared/init')
  }
}
```


For content that is only required in one page, you can do it like this:
In your page file:
```vue
<template>
  <div>
    <SectionHead :section="page.acf.section_head" />
    <SectionTeams :teams="teams"/>
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

And in your team section file:

```vue
<template>
  <div>
    <SingleTeam v-for="(team, index) in teams" :key="index" :team="team"/>
  </div>
</template>
<script>
  export default{
    props:['teams']
  }
</script>
```

For content, that you need globally on multiple pages, such as navbar and footer you can do it like this:

In you `@/store/index.js`  file:
```javascript
export const actions = {
  async nuxtServerInit(vuex, nuxt){
    await this.dispatch('shared/init')
  }
}
```
  
And in your `@/store/shared.js`  file:
  
```javascript
export const state = () => ({
  data : {},
})
export const mutations = {
  init(state, data){
    state.data = data
  },
}
export const actions = {
  async init(state){
    var data = await this.$apiService.get('/wp/v2/pages/<id_of_page_with_shared_content_such_as_navbar_or_footer>').then(res => {return res.data})
    commit('init', data)
  }
}
```
