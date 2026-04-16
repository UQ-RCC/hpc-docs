---
layout: default
---

<style>
  /* Fix the 'Narrow' issue and kill the sidebar */
  .wrapper { max-width: 1100px !important; margin: 0 auto !important; padding: 40px !important; }
  header { display: none !important; }
  section { width: 100% !important; float: none !important; }

  body { font-family: Arial, sans-serif !important; color: #333; line-height: 1.6; }
  h1 { color: {{ site.uq_purple }}; border-bottom: 4px solid {{ site.uq_gold }}; padding-bottom: 10px; }
  
  .folder-section { margin-top: 40px; }
  .folder-header { color: {{ site.uq_purple }}; font-size: 1.5rem; font-weight: bold; margin-bottom: 5px; }
  .folder-blurb { font-style: italic; color: #666; margin-bottom: 15px; }

  /* 2-Column Grid for a wider, more modern look */
  .resource-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(450px, 1fr));
    gap: 12px;
  }

  .item-card { 
    display: flex;
    justify-content: space-between;
    padding: 12px 18px;
    background: #fff;
    border: 1px solid #e1e1e1;
    border-left: 5px solid {{ site.uq_purple }};
    border-radius: 4px;
    text-decoration: none;
    transition: 0.2s ease;
  }
  .item-card:hover { border-left-color: {{ site.uq_gold }}; background: #f9f9f9; transform: translateX(5px); }
  .item-link { font-weight: bold; color: {{ site.uq_purple }}; }
</style>

# UQ RCC HPC Documentation
Welcome to the central index for information and guides for systems operated by the UQ Research Computing Centre.

{% comment %} Loop through categories in the order defined in _data/descriptions.yml {% endcomment %}
{% for category in site.data.descriptions %}
  {% assign dir_name = category[0] %}
  {% assign blurb = category[1] %}

  <div class="folder-section">
    <div class="folder-header">{{ dir_name | capitalize }}</div>
    <div class="folder-blurb">{{ blurb }}</div>

    <div class="resource-grid">
      {% comment %} Sort pages by weight (primary) then title (secondary) {% endcomment %}
      {% assign sorted_pages = site.pages | sort: "weight" %}
      
      {% for page in sorted_pages %}
        {% if page.path contains dir_name %}
          <a href="{{ site.baseurl }}{{ page.url }}" class="item-card">
            <span class="item-link">{{ page.title | default: page.basename | replace: "-", " " | capitalize }}</span>
          </a>
        {% endif %}
      {% endfor %}
    </div>
  </div>
{% endfor %}

