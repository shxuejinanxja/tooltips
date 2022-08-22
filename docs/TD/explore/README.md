# Study notes of Explore it!

## Charter your explorations

[charter](charter.md)

## Evaluate Results

> How do you know if the behavior you're seeing is correct?

### Never and Always

> Every system have some never and always rules. If at any time your explorations cause the system to volate them, it's a serious problem.

#### Never and Always Rules for Acad

- it should never crash.
- it should never corrupt user's drawing.
- user should always albe to see display of same drawing
- always able to undo aka back to an usable state from any user input or action

##### core capabilities

> The core capabilities in your view maybe quite different from the business analyst or product manager.

##### quality factors

> Accuracy: never provide an inaccurate result; always generate error messages on invalid inputs that cannot be used in a calculation
>
> Reliability: always recover to a usable state from any user input or action, no matter how ill-timed or incorrect that input or action was
>
> Availability: always respond to user requests (within a specified time period)
>
> Usability: always give users feedback about the effects of their actions; always provide clear indicators of available actions
>
> Accessibility: always provide keyboard shortcuts; always provide text alternatives for images
>
> Security: never expose secure data to an unauthorized recipient; never execute user input as code

internal consistence

approximation

- resonable range
- revert A-B B-A
- fix other variable then change one or two parameter to see the effect of them (max min)

## vary sequences and interactions

> Real-world users are not, on the whole, an orderly lot. They do things willy-nilly, not respecting the flow of actions that the designers intended them to follow in any given software application

### nouns and verbs

think of nouns and verbs of the program/feature
randomly pick one noun and one verb then add them to a sequence of actions you may find a new path when try to make it work.
or you may creativly find workaound to achieve same goals.

### Random navigation

> With your list of navigation options in hand, explore your software while considering these questions:

- What are all the ways you can close the current window?
- What are all the ways you can go back from your current location to the previous window or view?
- What are all the ways you can input data into a given field?
- What are all the ways you can submit or save changes?
- What are all the ways you can cancel or undo an action?

### Personas

> a persona is an archetype for a class of users our system needs to serve.
> Adopting the mantle of a persona prompts you to interact with the software with a self-consistent set of assumptions, expectations, desires, and quirks.

## Explore entities and their relationships

### CRUD Create Read Update Delete

> I always run is to create entities with values in all the optional fields and then attempt an update where I delete the values in those fields.

Look for different ways to CRUD entities, such as these examples:

- By navigating through different paths, screens, or commands
- As a side effect of some other action
- Through undo/redo commands
