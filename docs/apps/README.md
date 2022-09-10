# Apps

## Notion

- It support Mermaid.
- It has very rich support of markdown elements.
- It can be select and copy paste as markdown

### Reference

[Basic edit](https://www.notion.so/help/writing-and-editing-basics)

## postman

### collections

The collections can be export to a json file and import later

### environment variable

It can also be export and import in form of json.

[Reference of using variables](https://learning.postman.com/docs/sending-requests/variables/)

#### init and current value

result from https response can be save to the current value of a variable.
After set init value. Need to use reset button to update it to the current value otherwise the collection is not able to use it.

#### save response data as environment variable

you can use test to do it. Tests are written in javascript and are run after the response is received. [Write Tests](https://learning.postman.com/docs/writing-scripts/test-scripts/)
