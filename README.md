# shopify-code-snippets
Collection of useful shopify code snippets

##  Show available variants on collection pages
By adding some css you can also highlight the availability

```
<div class="mo-availability">
  {% unless sold_out %}
    {% unless product.has_only_default_variant %}
      {% for option in product.options_with_values %}
          {% for value in option.values %}
            {% assign variant_available = true %}
            {% if product.options.size == 1 %}
              {% unless product.variants[forloop.index0].available  %}
                {% assign variant_available = false %}
              {% endunless %}
            {% endif %}
            <span class="value{% unless variant_available %} soldout{% endunless %}">{{ value | escape }}</span>
          {% endfor %}
      {% endfor %}
    {% endunless %}
  {% endunless %}
  </div>
```

##  Show custom product label based on a tag
Just add the tag e.g. `label-comingsoon` to your product
````
{% if product.tags contains 'label-comingsoon' %}
  <div class="ribbon-wrapper">
    <div class="ribbon comingsoon">
      {{ 'products.product.comingsoon' | t }}
    </div>
  </div>
{% endif %}
