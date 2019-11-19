<template>
<div>
  <p>
    <nuxt-link to="/inspire">
      <small><b>トップへ</b></small>
    </nuxt-link>
  </p>
  <div class="card">
    <div class="card-content">
      <div class="media">
        <div class="media-left">
          <figure class="image is-48x48">
            <img :src="user.profile_image_url" width="120" alt="">
          </figure>
        </div>
        <div class="media-content">
          <p class="title is-4">{{ user.name }}</p>
          <p class="subtitle is-6">@{{ user.id }}</p>
        </div>
      </div>

      <div class="content">
        <p>{{ user.description || 'No description' }}</p>
      </div>
    </div>
  </div>
  <b>投稿一覧</b>
  <section>
      <b-table
          :data="items">
          <template slot-scope="props">
              <b-table-column field="title" label="title">
                  {{ props.row.title }}
              </b-table-column>
              <b-table-column field="url" label="url">
                  {{ props.row.url }}
              </b-table-column>
          </template>
      </b-table>
  </section>
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