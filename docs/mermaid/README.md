# tips for mermaid

## how to add mermaid into docsify

add following to the index.html

```html
<script src="//unpkg.com/mermaid/dist/mermaid.js"></script>
<script>
  var num = 0;

  mermaid.initialize({ startOnLoad: false });

  window.$docsify = {
    loadSidebar: true,
    markdown: {
      renderer: {
        code: function (code, lang) {
          if (lang === "mermaid") {
            return (
              '<div class="mermaid">' +
              mermaid.render("mermaid-svg-" + num++, code) +
              "</div>"
            );
          }
          return this.origin.code.apply(this, arguments);
        },
      },
    },
  };
</script>
```

## mermaid examples

```mermaid
%%{init: {
"flowchart":{
    "diagramPadding": 64
  }
}}%%
graph TD;
a-->b;
a-->c;
c-->b;
b-->c;
```

```mermaid
%%{init: {
"flowchart":{

    "diagramPadding": 64

  }
}}%%
graph LR;
a-->b;
a-->c;
c-->b;
b-->c;
```

```mermaid

%%{init: {"theme": "dark"}}%%
pie showData
title hello
"a":90.7
"b":10.5
"c":20.2
```

```mermaid
%%{init: {"sequence": {"mirrorActors":false}}}%%
sequenceDiagram
    Cook->>+Timer: Remind me in 3 minutes
    Timer-->>-Cook: Done!
    Note left of Timer: mirrorActors turned off
```
