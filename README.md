backbone.event-spec
===================

An unofficial specification for Backbone Event names.

### About

Backbone has a simple event system that is used to transfer information between objects in your Application. Perhaps the most
common example of this is the `change` event fired when a Model's property changes.

This is an unofficial specification that combines a precedent set by Backbone with a few additional rules to create
a consistent, extensible event naming system. This allows you to use custom Backbone Events in a predictable manner throughout
your application.

### Structure

Events in Backbone classes should follow the following format:

`adverb:action:subject`

##### The Separator

The separator is used to separate the three pieces of the event name, described above. It's a colon, `:`. The colon should only
be used to separate the different sections of the event name. Within each section camel case should be used for multiple words.

```js
// Using the separator incorrectly
'showMyView';
'show-view';
'show:my:view';

// Using it correctly
'show:myView';
```

##### The adverb

The first part of the event name is the adverb. The most common adverb to use is `before`. The adverb is optional. In Backbone
there are no standard events triggered with an adverb.

The following example shows an event that might be triggered before a close event on a custom class.

`before:close`

Do note that you should never use the adverb `after`. Backbone Events without an adverb are assumed to always be fired after
the event occurs. For instance, `change` is only fired on the Model *after* its properties have been changed.

##### The action

The action is always present tense. The action should be a simple verb that describes the event
that just happened. The action is the only required part of the event name.

```js
// Bad Backbone event name
'rendered';

// Good Backbone event name
'render';
```

##### The subject

The last part of the event name is the subject. Like the adverb, the subject is optional. An event may have at most
a single subject.

The subject is ideally a simple, one-word noun. In the case of a more complex noun you should use colons
to separate out the pieces.

Here is an example event name that might be fired when a child view is shown by the parent:

```js
'show:child';
```

When the subject of the verb is the object itself you can omit it. For instance, the event is just `change` in Backbone, not
`change:model`. Only when it's referencing a particular property of the model does it use the subject.

We can use this pattern to determine possible event names for rendering a view.

```js
// When a view renders
'render';

// When a child view of a parent view renders
'render:child';
```

##### Compound actions and subjects

If any part of the event consists of more than one word, then camel case should be used to separate them. Note that no standard Backbone Event has
a compound action or subject, and in general they should be avoided when possible.

An example of an event with a compound subject would be:

`show:redButton`

In this case, the subject has an adjective describing it, and they are written in camel case.

### Consistency

This specification is unofficial, so you shouldn't think of it as the *right way* to name your events.
[Even I'm not sure](https://github.com/jmeas/backbone.event-spec/issues/1) if I completely like everything here. This is
just an opinionated way to remain consistent.

And that philosophy of consistency is more important than any rule in this document. However you decide to name your events is
absolutely fine, so long as you follow some set of rules. This becomes increasingly important as your applications grow. It can save time
if you can just 'know' what the event name is based on your own guidelines, rather than always having to look it up.
