<template>
  <main class="main">
    <h1 class="title">{{ title }}</h1>
    <p class="publishedAt">{{ publishedAt }}</p>
    <div class="post" v-html="body"></div>
    <!-- メタ情報 -->
    <p>{{ meta.title }}</p>
    <p><img :src="meta.image.url" alt=""></p>
    <p>{{ meta.description }}</p>


    <!-- topic(Tech/Hobbyが入っている配列) -->
    <div
      v-for="(content, index) in topic"
      :key="`topic_${index}`"
    >
      <!-- Tech -->
      <div
        v-if="content.fieldId === 'tech'"
        class="content--tech"
      >
        <h2>{{ content.title }}</h2>
        <!-- body(richEditor/richlink/markdownが入っている配列) -->
        <div
          v-for="(body_content, index) in content.body"
          :key="`body_content_${index}`"
        >
          <div
            v-if="body_content.fieldId === 'richEditor'"
            v-html="body_content.richEditor"
          />
          <div
            v-if="body_content.fieldId === 'richlink'"
          >
            <a :href="body_content.richlink">{{ body_content.richlink }}</a>
          </div>
          <div
            v-if="body_content.fieldId === 'markdown'"
            v-html="body_content.markdown"
          />
        </div>
      </div>
      <!-- Hobby -->
      <div
        v-if="content.fieldId === 'hobby'"
        class="content--hobby"
      >
        <h2>{{ content.title }}</h2>
        <!-- body(richEditor/richlink/markdownが入っている配列) -->
        <div
          v-for="(body_content, index) in content.body"
          :key="`body_content_${index}`"
        >
          <div
            v-if="body_content.fieldId === 'richEditor'"
            v-html="body_content.richEditor"
          />
          <div
            v-if="body_content.fieldId === 'richlink'"
          >
            <a :href="body_content.richlink">{{ body_content.richlink }}</a>
          </div>
          <div
            v-if="body_content.fieldId === 'markdown'"
            v-html="body_content.markdown"
          />
        </div>
      </div>
    </div>

  </main>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData({ params }) {
    const { data } = await axios.get(
      `https://moonglows76-blog.microcms.io/api/v1/blog/${params.slug}`,
      {
        headers: { 'X-MICROCMS-API-KEY': '2e9ee6a0-1ebb-49ff-baeb-d1ccb3eff57e' }
      }
    )
    return data
  }
}
</script>

<style lang="scss" scoped>
.main {
  width: 960px;
  margin: 0 auto;
}

.title {
  margin-bottom: 20px;
}

.publishedAt {
  margin-bottom: 40px;
}

.post ::v-deep {
  & > h1 {
    font-size: 30px;
    font-weight: bold;
    margin: 40px 0 20px;
    background-color: #eee;
    padding: 10px 20px;
    border-radius: 5px;
  }

  & > h2 {
    font-size: 24px;
    font-weight: bold;
    margin: 40px 0 16px;
    border-bottom: 1px solid #ddd;
  }

  & > p {
    line-height: 1.8;
    letter-spacing: 0.2px;
  }

  & > ol {
    list-style-type: decimal;
    list-style-position: inside;
  }
}
</style>
