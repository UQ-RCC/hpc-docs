---
layout: default
---

<style>
  body { font-family: Arial, sans-serif !important; color: #333; line-height: 1.6; }
  h1 { color: {{ site.uq_purple }}; border-bottom: 3px solid {{ site.uq_gold }}; margin-bottom: 30px; }
  
  .folder-section { margin-top: 45px; }
  .folder-header { color: {{ site.uq_purple }}; border-left: 8px solid {{ site.uq_gold }}; padding: 5px 15px; margin-bottom: 10px; font-size: 1.6rem; }
  .folder-blurb { font-style: italic; color: #555; margin-bottom: 15px; padding-left: 23px; }
  
  .resource-grid { display: flex; flex-direction: column; gap: 8px; margin-bottom: 20px; }
  .item-card { 
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 15px;
    background: #fff;
    border: 1px solid #eee;
    border-radius: 4px;
    text-decoration: none;
    transition: 0.2s ease;
  }
  .item-card:hover { border-color: {{ site.uq_purple }}; background: #fcfcfc; transform: translateX(5px); }
  .item-link { font-weight: bold; color: {{ site.uq_purple }}; text-decoration: none; }
  .item-ext { font-size: 0.7rem; color: #888; text-transform: uppercase; font-family: monospace; border: 1px solid #ddd; padding: 1px 4px; border-radius: 3px; }
</style>

# UQ RCC HPC Resource Hub
Welcome to the central index for information and guides for systems operated by the UQ Research Computing Centre.

{% assign raw_dirs = "" %}
{% for file in site.static_files %}
  {% if file.extname == ".md" or file.extname == ".html" %}
    {% assign parts = file.path | split: "/" %}
    {% if parts.size > 2 %}
      {% assign raw_dirs = raw_dirs | append: parts[1] | append: "," %}
    {% endif %}
  {% endif %}
{% endfor %}
{% assign directory_names = raw_dirs | split: "," | uniq | sort %}

{% for dir in directory_names %}
  <div class="folder-section">
    <div class="folder-header">{{ dir | replace: "-", " " | replace: "_", " " | capitalize }}</div>
    
    {% comment %} LOOKUP BLURB FROM _data/descriptions.yml {% endcomment %}
    {% if site.data.descriptions[dir] %}
      <div class="folder-blurb">{{ site.data.descriptions[dir] }}</div>
    {% endif %}

    <div class="resource-grid">
    {% for file in site.static_files %}
      {% if file.path contains dir %}
        {% if file.extname == ".md" or file.extname == ".html" %}
          {% assign final_url = file.path | replace: ".md", ".html" %}
          <a href="{{ site.baseurl }}{{ final_url }}" class="item-card">
            <span class="item-link">{{ file.basename | replace: "-", " " | replace: "_", " " | capitalize }}</span>
            <span class="item-ext">{{ file.extname | replace: ".", "" }}</span>
          </a>
        {% endif %}
      {% endif %}
    {% endfor %}
    </div>
  </div>
{% endfor %}
