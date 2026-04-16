---
layout: default
---

<style>
  /* Layout: Full Width & Professional Dashboard */
  .wrapper { max-width: 1200px !important; margin: 0 auto !important; padding: 20px !important; }
  header { display: none !important; }
  section { width: 100% !important; float: none !important; }
  
  footer { 
    position: relative !important; 
    clear: both !important; 
    margin-top: 80px !important; 
    display: block !important;
    padding-bottom: 20px !important;
  }

  body { font-family: Arial, sans-serif !important; color: #333; line-height: 1.6; }
  h1 { color: #51247a; border-bottom: 4px solid #A08030; padding-bottom: 10px; margin-bottom: 5px; }
  .welcome-blurb { margin-bottom: 40px; color: #555; font-size: 1.1rem; }
  
  .folder-section { margin-top: 50px; }
  .folder-header { color: #51247a; font-size: 1.6rem; font-weight: bold; margin-bottom: 5px; border-left: 10px solid #A08030; padding-left: 15px; }
  .folder-blurb { font-style: italic; color: #666; margin-bottom: 20px; padding-left: 25px; }

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
    border-left: 5px solid #51247a;
    border-radius: 4px;
    text-decoration: none;
    transition: 0.2s ease;
  }
  .item-card:hover { border-left-color: #A08030; background: #fdfdfd; transform: translateX(5px); box-shadow: 0 2px 8px rgba(0,0,0,0.1); }
  .item-link { font-weight: bold; color: #51247a; font-size: 1.05rem; }

  details { background: #f9f9f9; padding: 15px; border-radius: 4px; border: 1px solid #eee; margin-top: 10px; }
  summary { font-weight: bold; color: #51247a; cursor: pointer; outline: none; }
  .extra-list { list-style: none; padding: 15px 0 0 10px; margin: 0; display: grid; grid-template-columns: repeat(auto-fill, minmax(350px, 1fr)); gap: 10px; }
  .extra-list a { color: #51247a; text-decoration: none; }
  .extra-list a:hover { text-decoration: underline; }
</style>

# UQ RCC HPC Documentation Hub
<p class="welcome-blurb">Welcome to the central index for information and guides for systems operated by the UQ Research Computing Centre.</p>

{% for category in site.data.descriptions %}
  {% assign dir_name = category[0] %}
  {% assign category_blurb = category[1] %}

  <div class="folder-section">
    <div class="folder-header">{{ dir_name | capitalize }}</div>
    <div class="folder-blurb">{{ category_blurb }}</div>

    {% assign displayed_paths = "" | split: "" %}
    {% assign priority_docs = "" | split: "" %}
    {% assign extra_docs = "" | split: "" %}

    {% comment %} 
      1. Collect Registry items and weighted Pages into one list for sorting.
    {% endcomment %}
    
    {% for entry in site.data.registry %}
      {% if entry[0] contains dir_name %}
        {% assign priority_docs = priority_docs | push: entry %}
        {% assign displayed_paths = displayed_paths | push: entry[0] %}
      {% endif %}
    {% endfor %}

    {% assign cat_pages = site.pages | where_exp: "p", "p.path contains dir_name" %}
    {% for p in cat_pages %}
      {% if p.name != "index.md" and p.title %}
        {% unless displayed_paths contains p.path %}
          {% if p.weight %}
             {% assign priority_docs = priority_docs | push: p %}
          {% else %}
             {% assign extra_docs = extra_docs | push: p %}
          {% endif %}
          {% assign displayed_paths = displayed_paths | push: p.path %}
        {% endunless %}
      {% endif %}
    {% endfor %}

    {% comment %} 2. Render Grid with explicit URL branching {% endcomment %}
    <div class="resource-grid">
      {% assign sorted_priority = priority_docs | sort: "weight" %}
      {% for item in sorted_priority %}
        
        {% if item.layout %}
          {% comment %} This is a Jekyll Page Object {% endcomment %}
          {% assign final_link = item.url | relative_url %}
          {% assign final_title = item.title %}
        {% else %}
          {% comment %} This is a Registry Entry (Array [key, meta]) {% endcomment %}
          {% assign reg_key = item[0] %}
          {% assign reg_meta = item[1] %}
          {% assign final_title = reg_meta.title %}
          
          {% if reg_meta.url %}
            {% assign final_link = reg_meta.url %}
          {% else %}
            {% assign final_link = reg_key | relative_url %}
          {% endif %}
        {% endif %}

        <a href="{{ final_link }}" class="item-card">
          <span class="item-link">{{ final_title }}</span>
        </a>
      {% endfor %}
    </div>

    {% comment %} 3. Additional Static Files (PDF/HTML) {% endcomment %}
    {% for file in site.static_files %}
      {% if file.path contains dir_name %}
        {% if file.extname == ".pdf" or file.extname == ".html" %}
          {% assign clean_path = file.path | remove_first: "/" %}
          {% unless displayed_paths contains clean_path or displayed_paths contains file.path %}
            {% assign extra_docs = extra_docs | push: file %}
          {% endunless %}
        {% endif %}
      {% endif %}
    {% endfor %}

    {% if extra_docs.size > 0 %}
      <details>
        <summary>Additional {{ dir_name | capitalize }} Resources</summary>
        <ul class="extra-list">
          {% assign sorted_extras = extra_docs | sort: "title" %}
          {% for doc in sorted_extras %}
            <li>
              <a href="{{ doc.url | default: doc.path | relative_url }}">
                {{ doc.title | default: doc.basename | replace: "-", " " | replace: "_", " " }}
              </a>
            </li>
          {% endfor %}
        </ul>
      </details>
    {% endif %}

  </div>
{% endfor %}
