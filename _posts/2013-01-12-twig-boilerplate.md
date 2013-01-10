---
layout: default
title: "Twig Boilerplate"
published: true
classes:
 - slide
data:
  x: 0
  y: 0

---
Twig "filter" syntax examples:

{% highlight javascript %}
{# General format for using a filter: #}
{ { value | filter_name }}

{# Examples: #}
{ { "Translatable string" | t }}
{ { safe_html_value | raw }}
{% endhighlight %}

We need to provide the t (translate) and raw filters:

{% highlight javascript %}
Twig.extendFilter("t", function(value) {
  return Drupal.t(value);
});
Twig.extendFilter("raw", function(value) {
  return value;
});
{% endhighlight %}
