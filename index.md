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
    {% assign extra_docs = "" | split: "" %}

    <div class="resource-grid">
      {% comment %} 
        MANUAL OVERRIDE: Add specific external links here. 
        We check if we are in the 'guides' section to display the Acknowledgment link.
      {% endcomment %}
      {% if dir_name == "guides" %}
        <a href="https://rcc.uq.edu.au/about/acknowledging-rcc" class="item-card">
          <span class="item-link">How to Acknowledge Bunya and/or RCC</span>
        </a>
      {% endif %}

      {% comment %} 1. Weighted Markdown Pages {% endcomment %}
      {% assign weighted_pages = site.pages | where_exp: "p", "p.path contains dir_name" | where: "weight", true | sort: "weight" %}
      {% for p in weighted_pages %}
        <a href="{{ p.url | relative_url }}" class="item-card">
          <span class="item-link">{{ p.title }}</span>
        </a>
        {% assign displayed_paths = displayed_paths | push: p.path %}
      {% endfor %}
    </div>

    {% comment %} 2. Unweighted Files (MD, PDF, HTML) in Dropdown {% endcomment %}
    {% assign all_files = site.pages | concat: site.static_files %}
    {% for file in all_files %}
      {% if file.path contains dir_name %}
        {% if file.extname == ".pdf" or file.extname == ".html" or file.extname == ".md" %}
          {% assign clean_path = file.path | remove_first: "/" %}
          {% unless displayed_paths contains clean_path or displayed_paths contains file.path or file.name == "index.md" %}
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
              <a href="{{
