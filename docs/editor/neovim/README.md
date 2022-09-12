# NeoVim

## keymap

| Action      | Key | Notes                       |
| ----------- | --- | --------------------------- |
| Hover       | K   | used in markdown dictionary |
| Switch case | ~   |                             |

## tips

### substitute

It accept pattern search
For example,`: 1662473225:0;ls -la`
can use `:s/:.*;/` to represent pattern of

start with :, has more than one char , till;

## plugins

### motions

[quick scope](https://github.com/unblevable/quick-scope)
quick move by

- forward f/t
- backward F/T

then ;(forward) ,(backward)

[vi"](https://github.com/wellle/targets.vim)

### change surrounding

| key acions       | start                | end                  |
| ---------------- | -------------------- | -------------------- |
| cs"'             | "hello world"        | 'hello world'        |
| cs"<li>          | "hello world"        | <li>hello world</li> |
| cst'             | <li>hello world</li> | 'hello world'        |
| ds"              | "hello world"        | hello world          |
| ysiw[            | hello world          | [ hello ] world      |
| ysiw]            | hello world          | [hello] world        |
| yssb entire line | hello world          | (hello world)        |
