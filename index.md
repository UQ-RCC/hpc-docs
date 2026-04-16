---
layout: default
---

<style>
  /* Layout: Full Width & No Sidebar */
  .wrapper { max-width: 1100px !important; margin: 0 auto !important; padding: 20px !important; }
  header { display: none !important; }
  section { width: 100% !important; float: none !important; }

  body { font-family: Arial, sans-serif !important; color: #333; }
  h1 { color: {{ site.uq_purple }}; border-bottom: 4px solid {{ site.uq_gold }}; padding-bottom: 10px; }
  
  .folder-section { margin-top: 40px; }
  .folder-header { color: {{ site.uq_purple }}; font-size: 1.5rem; font-weight: bold; margin-bottom: 5px; }
  .folder-blurb { font-style: italic; color: #666; margin-bottom: 15px; }

  /* Grid for Weighted/Primary items */
  .resource-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
    gap: 12px;
    margin-bottom: 20px;
  }

  .item-card { 
    display: flex;
    padding: 12px 18px;
    background: #fff;
    border: 1px solid #e1e1e1;
    border-left: 5px solid {{ site.uq_purple }};
    border-radius: 4px;
    text-decoration: none;
    transition: 0.2s ease;
  }
  .item-card:hover { border-left-color: {{ site.uq_gold }}; background: #f9f9f9; transform: translateX(5px); }
  .item-link { font-weight: bold; color: {{ site.uq_purple }}; text-decoration: none; }

  /* Dropdown for non-weighted files */
  details { background: #f7f7f7; padding: 12px; border-radius: 4px; border: 1px solid #eee; }
  summary { font-weight: bold; color: {{ site.uq_purple }}; cursor: pointer; }
  .extra-list { list-style: none; padding: 10px 0 0 10px; margin: 0; }
  .extra-list li { margin: 6px 0; border-bottom: 1px solid #eee; padding-bottom: 4px; }
  .extra-list a { color: {{ site.uq_purple }}; text-decoration: none; font-size: 0.95rem; }
</style>

# UQ RCC HPC Documentation Hub
Welcome to the central index for information and guides for systems operated by the UQ Research Computing Centre.

{% for category in site.data.descriptions %}
  {% assign dir_name = category[0] %}
  {% assign blurb = category[1] %}

  <div class="folder-section">
    <div class="folder-header">{{ dir_name | capitalize }}</div>
    <div class="folder-blurb">{{ blurb }}</div>

    {% comment %} 
      GATHER: Filter site.pages and site.static_files for this directory
    {% endcomment %}
    {% assign priority_docs = "" | split: "," %}
    {% assign additional_docs = "" | split: "," %}

    {% for p in site.pages %}
      {% comment %} Skip system files and the index itself {% endcomment %}
      {% if p.path contains dir_name and p.name != "index.md" and p.name != "index.html" %}
        {% if p.weight %}
          {% assign priority_docs = priority_docs | push: p %}
        {% else %}
          {% assign additional_docs = additional_docs | push: p %}
        {% endif %}
      {% endif %}
    {% endfor %}

    {% comment %} 
      Check static_files too (in case some HTML isn't in 'defaults' yet)
    {% endcomment %}
    {% for f in site.static_files %}
      {% if f.path contains dir_name and f.extname == ".html" %}
        {% comment %} Only add if not already caught in site.pages {% endcomment %}
        {% assign is_duplicate = false %}
        {% for pd in priority_docs %}{% if pd.path contains f.path %}{% assign is_duplicate = true %}{% endif %}{% endfor %}
        {% for ad in additional_docs %}{% if ad.path contains f.path %}{% assign is_duplicate = true %}{% endif %}{% endfor %}
        
        {% unless is_duplicate %}
          {% assign additional_docs = additional_docs | push: f %}
        {% endunless %}
      {% endif %}
    {% endfor %}

    {% comment %} 1. Render Priority (Weighted) Cards {% endcomment %}
    {% assign sorted_priority = priority_docs | sort: "weight" %}
    <div class="resource-grid">
      {% for doc in sorted_priority %}
        <a href="{{ site.baseurl }}{{ doc.url }}" class="item-card">
          <span class="item-link">{{ doc.title | default: doc.basename | replace: "-", " " | capitalize }}</span>
        </a>
      {% endfor %}
    </div>

    {% comment %} 2. Render Additional (Unweighted) Dropdown {% endcomment %}
    {% if additional_docs.size > 0 %}
      <details>
        <summary>Additional Resources ({{ additional_docs.size }})</summary>
        <ul class="extra-list">
          {% assign sorted_extras = additional_docs | sort: "title" %}
          {% for doc in sorted_extras %}
            <li>
              <a href="{{ site.baseurl }}{{ doc.url | default: doc.path }}">
                {{ doc.title | default: doc.basename | replace: "-", " " | capitalize }}
              </a>
            </li>
          {% endfor %}
        </ul>
      </details>
    {% endif %}
  </div>
{% endfor %}
