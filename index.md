---
layout: default
---

<style>
  /* Layout: Full Width & Professional Dashboard */
  .wrapper { max-width: 1200px !important; margin: 0 auto !important; padding: 20px !important; }
  header { display: none !important; }
  section { width: 100% !important; float: none !important; }

  body { font-family: Arial, sans-serif !important; color: #333; line-height: 1.6; }
  h1 { color: {{ site.uq_purple }}; border-bottom: 4px solid {{ site.uq_gold }}; padding-bottom: 10px; margin-bottom: 5px; }
  .welcome-blurb { margin-bottom: 40px; color: #555; font-size: 1.1rem; }
  
  .folder-section { margin-top: 50px; }
  .folder-header { color: {{ site.uq_purple }}; font-size: 1.6rem; font-weight: bold; margin-bottom: 5px; border-left: 10px solid {{ site.uq_gold }}; padding-left: 15px; }
  .folder-blurb { font-style: italic; color: #666; margin-bottom: 20px; padding-left: 25px; }

  /* Priority Grid (2 Columns) */
  .resource-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(500px, 1fr));
    gap: 15px;
    margin-bottom: 25px;
  }

  .item-card { 
    display: flex;
    padding: 15px 20px;
    background: #fff;
    border: 1px solid #ddd;
    border-left: 5px solid {{ site.uq_purple }};
    border-radius: 4px;
    text-decoration: none;
    transition: 0.2s ease;
  }
  .item-card:hover { border-left-color: {{ site.uq_gold }}; background: #fdfdfd; transform: translateX(5px); box-shadow: 0 2px 8px rgba(0,0,0,0.1); }
  .item-link { font-weight: bold; color: {{ site.uq_purple }}; font-size: 1.05rem; }

  /* Dropdown for Additional Docs */
  details { background: #f9f9f9; padding: 15px; border-radius: 4px; border: 1px solid #eee; margin-top: 10px; }
  summary { font-weight: bold; color: {{ site.uq_purple }}; cursor: pointer; outline: none; }
  .extra-list { list-style: none; padding: 15px 0 0 10px; margin: 0; display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); gap: 10px; }
  .extra-list a { color: {{ site.uq_purple }}; text-decoration: none; border-bottom: 1px solid transparent; }
  .extra-list a:hover { border-bottom: 1px solid {{ site.uq_gold }}; }
</style>

# UQ RCC HPC Documentation Hub
<p class="welcome-blurb">Welcome to the central index for information and guides for systems operated by the UQ Research Computing Centre.</p>

{% for category in site.data.descriptions %}
  {% assign dir_name = category[0] %}
  {% assign category_blurb = category[1] %}

  <div class="folder-section">
    <div class="folder-header">{{ dir_name | capitalize }}</div>
    <div class="folder-blurb">{{ category_blurb }}</div>

    {% comment %} 
      1. Aggregation Phase 
    {% endcomment %}
    {% assign priority_list = "" | split: "," %}
    {% assign additional_list = "" | split: "," %}

    {% comment %} Check all pages (Markdown with Front Matter) {% endcomment %}
    {% for p in site.pages %}
      {% if p.path contains dir_name and p.name != "index.md" %}
        {% if p.weight %}
          {% assign priority_list = priority_list | push: p %}
        {% else %}
          {% assign additional_list = additional_list | push: p %}
        {% endif %}
      {% endif %}
    {% endfor %}

    {% comment %} Check Registry for HTML tools or unweighted files {% endcomment %}
    {% for file in site.static_files %}
      {% if file.path contains dir_name %}
        {% assign reg_entry = site.data.registry[file.path] %}
        {% if reg_entry %}
          {% comment %} Create a virtual object for sorting {% endcomment %}
          {% assign virtual_page = file | append: "" %} 
          {% comment %} We actually need to handle the Registry items by path to avoid duplicates {% endcomment %}
        {% endif %}
      {% endif %}
    {% endfor %}

    {% comment %} 
       REFINED LOGIC: Separate Priority from Additional
    {% endcomment %}
    
    <div class="resource-grid">
      {% comment %} Sort priority by weight {% endcomment %}
      {% assign all_priority = site.pages | where_exp: "p", "p.path contains dir_name" | where_exp: "p", "p.weight != nil" | sort: "weight" %}
      
      {% for doc in all_priority %}
        <a href="{{ site.baseurl }}{{ doc.url }}" class="item-card">
          <span class="item-link">{{ doc.title }}</span>
        </a>
      {% endfor %}

      {% comment %} Manually Inject Registry Tools into Priority Grid {% endcomment %}
      {% for entry in site.data.registry %}
        {% assign file_path = entry[0] %}
        {% assign meta = entry[1] %}
        {% if file_path contains dir_name %}
          <a href="{{ site.baseurl }}/{{ file_path }}" class="item-card">
            <span class="item-link">{{ meta.title }}</span>
          </a>
        {% endif %}
      {% endfor %}
    </div>

    {% comment %} 2. Dropdown for everything else {% endcomment %}
    {% assign all_others = site.pages | where_exp: "p", "p.path contains dir_name" | where_exp: "p", "p.weight == nil" | where_exp: "p", "p.name != 'index.md'" %}
    
    {% if all_others.size > 0 %}
      <details>
        <summary>Additional {{ dir_name | capitalize }} Resources</summary>
        <ul class="extra-list">
          {% for doc in all_others %}
            {% comment %} Prettify the title: strip hyphens/ext, then respect provided title {% endcomment %}
            <li>
              <a href="{{ site.baseurl }}{{ doc.url }}">
                {{ doc.title | default: doc.basename | replace: "-", " " | replace: "_", " " }}
              </a>
            </li>
          {% endfor %}
        </ul>
      </details>
    {% endif %}

  </div>
{% endfor %}
