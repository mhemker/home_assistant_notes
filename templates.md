Show all entities where the object_id starts with a specific string.
```
{% for state in states if state.object_id.startswith('dream_router') %}
- {{ state.entity_id }}
{% endfor %}
```

Show all entities where the object_id starts with a specific string.  Also shows the attributes
```
{% for state in states if state.object_id.startswith('dream_router') %}
- {{ state.entity_id }}
  {%- for key, value in state.attributes.items() | sort %}
    * {{ key }}: {{ value }}
  {%- endfor %}
{% endfor %}
```

Use the auto-entities card to show all entities that have a specific value in their object_id.  It also will remove a configurable prefix from the name.
The value to search for and the prefix to remove are set in variables at the top which makes this very easy to reuse by just updating those 2 lines.
```
type: custom:auto-entities
card:
  type: entities
  title: Roborock QV 35S
filter:
  template: |-
    {% set ns = namespace(ents=[]) %}
    {% set entity_search = 'roborock' %}
    {% set prefix_to_remove = 'Roborock QV 35S ' %}
    {% for s in states if entity_search in s.object_id %}
      {% set ns.ents = ns.ents + [{'entity': s.entity_id, 'name': s.name | replace(prefix_to_remove, '')}] %}
    {% endfor %}
        
    {{ ns.ents }}
sort:
  method: name
```
