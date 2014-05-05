backbone.event-spec
===================

The unofficial specification for Backbone Event names.

### About

Backbone has a simple event system that is used to transfer information between objects in your Application. Perhaps the most
common example of this is the `change` event fired when a Model's property changes.

This is an unofficial specification that combines a precedent set by Backbone with a few additional rules to create
a consistent, extensible event naming system. This allows you to use Backbone Events in a predictable manner throughout
your application in more ways.

### Structure

Events in Backbone classes should follow the following format:

`adverb:action:subject`

##### The Separator

The separator to be used within event names is a colon, `:`. The colon should be used instead of other
separation mechanisms, such as period, hyphenating or camelcase.

```js
// Events that use an incorrect separator
'show:myView';
'show:my.view';
'show:my-view';

// Events that use a correct separator
'show:my:view';
```

##### The adverb

The first part of the event name is the adverb. The most common adverb is `before`. The adverb is optional. In Backbone
there are no standard events triggered with an adverb.

The following example shows an event that might be triggered before a close event on a custom class.

`before:close`

Do note that you should never use the adverb `after`. Backbone Events without an adverb are assumed to always be fired after
the event occurs. For instance, `change` is only fired on the Model *after* its properties have been changed.

##### Action

The action is always present tense. The action should be a simple verb that describes the event
that just happened. The action is the only required part of the event name.

```js
// Bad Backbone event name
'rendered';

// Good Backbone event name
'render';
```

##### Subject

The last part of the event name is the subject. Like the adverb, the subject is optional. An event may have at most
a single subject.

The subject is ideally a simple, one-word noun. In the case of a more complex noun you should use colons
to separate out the pieces.

Here is an example event name that might be fired when a child view is shown by the parent:

```js
show:child
```

When the subject of the verb is the object itself you can omit it. For instance, the event is just `change` in Backbone, not
`change:model`. Only when it's referencing a particulaly property of the model does it use the subject.

We can use this pattern to determine possible event names for rendering a view.

```js
// When a view renders
'render';

// When a child view of a parent view renders
'render:child';
```

##### Compound actions and subjects

If any part of the event consists of more than one word, then a colon should be used to separate them. No standard Backbone Event has
a compound action or subject, and in general they should be avoided when possible.

An example of an event with a compound subject would be:

`show:red:button`

In this case, the subject has an adjective describing it which is separated by the colon.