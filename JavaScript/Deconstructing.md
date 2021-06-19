# De-constructing

```javascript
const js = {
  name: "JavaScript",
  type: "programming language",
  version: "ES6",
  tools: {
    frameworks: {
      framework1: "AngularJS",
      framework2: "Vue.js",
    },
    libraries: {
      library1: "jQuery",
      library2: "React",
    },
  },
};
const { framework1, framework2 } = js.tools.frameworks;
```
