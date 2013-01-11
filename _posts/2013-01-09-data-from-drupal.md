---
layout: default
title: "Getting Data From Drupal"
published: true
classes:
 - slide
data:
  x: 8000
  y: 0

---

{% highlight php %}
/**
 * Implements hook_menu().
 */
function todos_menu() {
  $items['todos/todos.json'] = array(
    'title' => 'Todos JavaScript service',
    'page callback' => 'todos_json',
    'access arguments' => array('access content'),
    'type' => MENU_CALLBACK,
  );
  return $items;
}

/**
 * Menu callback: Data provider for Backbone.js front-end.
 */
function todos_json() {
  $results = views_get_view_result('all_todos', 'default');
  $fields = array(
    'nid'   => 'nid',
    'title' => 'node_title',
    'created' => 'node_created',
    'done' => 'node_data_field_done_field_done_value',
  );
  $data = array();
  foreach ($results as $row) {
    $node = new stdClass();
    foreach ($fields as $key => $views_key) {
      $node->{$key} = $row->{$views_key};
    }
    $node->_id         = (int) $node->nid;
    $node->created     = (int) $node->created;
    $node->done        = $node->done ? 'true' : 'false';
    $data[] = $node;
  }
  drupal_json($data);
  exit();
}
{% endhighlight %}
