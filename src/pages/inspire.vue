<template>
    <section>
        <b-table :data="items">
            <template slot-scope="props">
                <b-table-column field="id" label="ID" numeric>
                  <nuxt-link :to="`/users/${props.row.user.id}`">
                    {{ props.row.user.id }}
                  </nuxt-link>
                </b-table-column>
                <b-table-column field="title" label="Title">
                    {{ props.row.title }}
                </b-table-column>
                <b-table-column field="url" label="URL">
                    <a :href="props.row.url">{{ props.row.url }}</a>
                </b-table-column>
            </template>
        </b-table>
    </section>
</template>

<script>
export default {
  async asyncData({ app }) {
    const items = await app.$axios.$get('https://qiita.com/api/v2/items?query=tag:quicksight')
    return{
      items
    }
  }
}
</script>