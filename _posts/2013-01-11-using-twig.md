---
layout: default
title: "Using Twig"
published: true
classes:
 - slide
data:
  x: 0
  y: 0

---
Simplest method: Place templates inside of a script tag in your markup:

{% highlight html %}
<script type="text/html" id="template-welcome">
  <h1 id="{ { html_id }}">{ { 'Welcome' | t }}<h1>
  { % if error_message %}
    <p class="error">{ { error_message }}</p>
  { % endif %}
</script>
{% endhighlight %}

{% highlight javascript %}
var WelcomeView = Backbone.View.extend({
  template: twig({ data: $("#template-welcome").html() }),
  render: function() {
    var markup = this.template.render({
      html_id: "page-title",
      error_message: Drupal.t("DANGER!")
    });
    this.$el.html(markup);
    return this;
  }
});
{% endhighlight %}
