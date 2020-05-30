# Initialization of the project

We'll create a REST API with Postgresql and NodeJS.
The first step is to create our main folder and place this document structure:

```bash
- __portfolio__
   - __main__
     - [README.md](main/README.md)
     - [babel.config.js](main/babel.config.js)
     - [node\_modules](main/node_modules)
     - [package\-lock.json](main/package-lock.json)
     - [package.json](main/package.json)
     - __public__
       - [favicon.ico](main/public/favicon.ico)
       - [index.html](main/public/index.html)
     - __src__
       - [App.vue](main/src/App.vue)
       - __assets__
       - __components__
         - [HelloWorld.vue](main/src/components/HelloWorld.vue)
         - [Home.vue](main/src/components/Home.vue)
       - __controllers__
       - [index.js](main/src/index.js)
       - [main.ts](main/src/main.ts)
       - __routes__
       - [shims\-tsx.d.ts](main/src/shims-tsx.d.ts)
       - [shims\-vue.d.ts](main/src/shims-vue.d.ts)
       - __store__
         - [index.ts](main/src/store/index.ts)
     - [tsconfig.json](main/tsconfig.json)
```
