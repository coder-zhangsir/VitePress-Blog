---
# https://vitepress.dev/reference/default-theme-home-page
layout: home

hero:
  name: "ZDoc"
  text: "赋予程序以生命"
  tagline: ZDoc译为Zhang Documents，保持良好的心态书写独属于我的笔记💪
  image:
    src: strive.svg
    alt: logo
  actions:
    - theme: brand
      text: + Follow Me(Bilibili)
      link: https://space.bilibili.com/483711690?spm_id_from=333.1007.0.0
    - theme: alt
      text: About Me
      link: /about

features:
  - title: JavaScript
    icon:
      src: ./language/js.svg
    details: JavaScript（通常缩写为JS）是一门基于原型和头等函数的多范式高级解释型编程语言，它支持面向对象程序设计、指令式编程和函数式编程。
    link: /js/trusted-event
  - title: Docker
    icon:
      src: ./language/docker.svg
    details: Docker 是一个应用打包、分发、部署的工具。你也可以把它理解为一个轻量的虚拟机，它只虚拟你软件需要的运行环境，多余的一点都不要。
    link: /docker/inspect
  - title: 项目规范
    icon:
      src: normalize.svg
    link: /specification/create-vue/summary
    details: 学习不同框架开发者前辈们的编程项目规范，并提取核心点
  - title: 速查表
    icon:
      src: zoom-table.svg
    link: /common-tools/cheat-sheet/git
    details: Git,Docker命令语句速查表
  - title: 大陆通行
    icon:
      src: mainland.svg
    link: /mainland/domain-name-filing/summary
    details: 想在中国内陆互联网畅通无阻就必须明白这几件事...
  - title: 插件使用
    icon:
      src: plugin-use.svg
    link: /plugin-using/lint-staged/summary
    details: Github各种有用插件的使用简记
---
