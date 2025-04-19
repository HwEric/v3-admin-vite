<!-- <script>
import markdownIt from "markdown-it"

export default {
  data() {
    return {
      rawMarkdown: `# Hello World\nThis is a **bold** text.`
    }
  },
  computed: {
    compiledMarkdown() {
      const md = markdownIt()
      return md.render(this.rawMarkdown)
    }
  }
}
</script>

<template>
  <div v-html="compiledMarkdown" />
</template>
<template>
  <div>
    <pre><code>
      <!DOCTYPE html>
      <html lang="en">
        <head>
          <meta charset="UTF-8">
          // name viewport 表示移动设备 content定义viewport的具体属性 initial-scale表设备与视口的缩放比例
          <meta name="viewport" content="width=device-width, initial-scale=1.0">
          <title>Document</title>
        </head>
        <body>
          html：超文本传输协议
        </body>
      </html>
    </code></pre>
  </div>
</template> -->
<script>
import { router } from "@/router"
import hljs from "highlight.js"
import MarkdownIt from "markdown-it"

// 处理返回
// eslint-disable-next-line unused-imports/no-unused-vars
function handleReturn() {
  router.push("/")
}

// 配置 markdown-it
const md = new MarkdownIt({
  html: true, // 允许 HTML 标签
  linkify: true, // 自动识别链接
  typographer: true, // 优化排版
  highlight(str, lang) { // 代码高亮
    if (lang && hljs.getLanguage(lang)) {
      try {
        return `<pre class="hljs"><code>${
          hljs.highlight(str, { language: lang, ignoreIllegals: true }).value
        }</code></pre>`
      } catch (e) {
        console.log(e)
      }
    }
    return `<pre class="hljs"><code>${md.utils.escapeHtml(str)}</code></pre>`
  }
})

export default {
  data() {
    return {
      markdownText: `
# Hello Markdown!

\`\`\`html
      // 代码示例
      <!DOCTYPE html>
      <html lang="en">
        <head>
          <meta charset="UTF-8">
          <meta name="viewport" content="width=device-width, initial-scale=1.0">
          <title>Document</title>
        </head>
        <body>
          html：超文本传输协议
          lang: 告诉浏览器我这里的语言是什么类型（zh-CN中文、en英文）
          name viewport: 表示移动设备 content定义viewport的具体属性
          initial-scale: 表设备与视口的缩放比例
        </body>
      </html>
\`\`\`
      `
    }
  },
  computed: {
    compiledMarkdown() {
      return md.render(this.markdownText)
    }
  },
  methods: {
    handleReturn() {
      router.push("/")
    }
  }
}
</script>

<template>
  <div class="markdown-content" v-html="compiledMarkdown" />
  <el-button type="primary" size="large" @click.prevent="handleReturn">
    返回首页
  </el-button>
</template>

<style>
/* 引入 highlight.js 主题样式 */
@import "~highlight.js/styles/github-dark.css";

/* 自定义样式 */
.markdown-content {
  font-family: Arial, sans-serif;
  line-height: 1.6;
}

.hljs {
  padding: 1em;
  border-radius: 4px;
  background: #1e1e1e;
  color: #dcdcdc;
}
</style>
