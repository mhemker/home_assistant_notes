Show all entities where the object_id starts with a specific string.  Also shows the attributes

{% for state in states if state.object_id.startswith('dream_router') %}
- {{ state.entity_id }}
  {%- for key, value in state.attributes.items() %}
    * {{ key }}: {{ value }}
  {%- endfor %}
{% endfor %}
