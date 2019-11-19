<template>
  <div>
    <h2>{{ user.id }}</h2>
    <img :src="user.profile_image_url" width="120" alt="">
    <p>{{ user.description || 'No description' }}</p>
    <p>
      <nuxt-link to="/inspire">
        <small><b>トップへ</b></small>
      </nuxt-link>
    </p>
    <h2>{{ user.id }}の投稿一覧</h2>
    <ul>
      <li v-for="(item,key) in items" :key="key">
        <h4>
          <span>{{ item.title }}</span>
        </h4>
        <div>{{ item.body.slice(0,50) }}・・・・</div>
        <p><a target="_blank" :href="item.url">{{ item.url }}</a></p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  async asyncData({ route,app }){
    const user = await app.$axios.$get(`https://qiita.com/api/v2/users/${route.params.id}`)
    const items = await app.$axios.$get(`https://qiita.com/api/v2/items?query=user:${route.params.id}`)
    return { user,items }
  }
}
</script>