<template>
  <!-- Nuxt.jsでは、template直下はHTML要素1つだけ（divとか、ここではulとか） -->
  <ul>
    <!-- li要素内をv-forディレクティブで作っていく -->
    <li v-for="content in contents" :key="content.id">
      <!-- nuxt-linkはWebサイト内のリンクを作るのに使う（ページの先読みをしてくれる） -->
      <!-- `` はテンプレートリテラル。${} の中にJavaScriptを書くことができる引用符 -->
      <nuxt-link :to="`/${content.id}`">
        {{ content.publishedAt }}<br>
        {{ content.title }}
      </nuxt-link>
    </li>
  </ul>
</template>

<script>
import axios from 'axios'
export default {
  // async, awaitは非同期通信をしますよーとブラウザに伝える記述
  // 書いておくと、次の処理を待ってくれます
  async asyncData() {
    // const { data } は分割代入
    // https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment

    // awaitを書いたあとの関数の実行を待って、次の処理を実行します。
    // VVV ここから VVV
    const { data } = await axios.get(
      // your-service-id部分は自分のサービスidに置き換えてください
      'https://moonglows76-blog.microcms.io/api/v1/blog',
      {
        // your-api-key部分は自分のapi-keyに置き換えてください
        headers: { 'X-MICROCMS-API-KEY': '2e9ee6a0-1ebb-49ff-baeb-d1ccb3eff57e' }
      }
    )
    // AAA ここまでを待ちます AAA
    // 上の処理が終わったら、下の処理を実行します。
    return data
  }
}
</script>
