# NeoVim

## how to use recored to record repeatable work

example add list mark for following items.
item1
item2
item3

1. press qz to start record action to registery z
2. then do any actions you want insert a - then esc
3. q to quit recording
4. 2@z to make the action over the 2 line below
5. :h q to view the help

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
