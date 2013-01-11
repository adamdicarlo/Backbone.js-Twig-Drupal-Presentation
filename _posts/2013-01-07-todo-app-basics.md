---
layout: default
title: "Todo App: Basic Structure"
published: true
classes:
 - slide
data:
  x: 6000
  y: 0

---

{% highlight javascript %}
var Todo = Backbone.Model.extend({});
var TodoList = Backbone.Collection.extend({
  model: Todo,
  localStorage: new Backbone.LocalStorage("todos-backbone"),
});
var TodoView = Backbone.View.extend({
  tagName: "li",
  template: ...,
  events: {
    "click .toggle": "toggleDone",
    "blur .edit"   : "close",
  },
  toggleDone: function() {
    this.model.toggle();
  },
  close: function() {
    // ...
  }
});
var Todos = new TodoList();
var AppView = Backbone.View.extend({
  el: "#todoapp",
  initialize: function() {
    Todos.fetch();
  }
});
var App = new AppView();
{% endhighlight %}

Abbreviated version of [http://is.gd/bb_todos_src](http://is.gd/bb_todos_src).

