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
````


##  Group productd by modell + show color swatches for collection pages + detail page
You need to add two metafields for earch product: modell e.g. `airmax90` + colorcode e.g. `#000000`

````
{%- if product.metafields.modell != blank -%}
  {%- capture productModells -%}
    {% assign modell = product.metafields.modell.value %}
    {% for p in collections.all.products %}
      {% assign pmodell = p.metafields.modell.value %}
          {% if p.id != product.id %}
          {% if modell == pmodell %}
            <a class="colorcode" href="{{ p.url }}" style="background-color: {{ p.metafields.colorcode.value }}"></a>
          {% endif %}
          {% endif %}
    {% endfor %}
  {%- endcapture -%}
  {%- if productModells != blank -%}
  <div class="color-swatches">
    <a href="#" class="colorcode active" style="background-color: {{ product.metafields.colorcode.value }};"></a>
    {{ productModells }}
  </div>
  {% endif %}
{%- endif -%}
````
