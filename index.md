---
layout: default
---

<p class="welcome-blurb">Welcome to the central index for information and guides for systems operated by the UQ Research Computing Centre.</p>

{% for category in site.data.descriptions %}
  {% assign dir_name = category[0] %}
  {% assign category_blurb = category[1] %}

  <div class="folder-section">
    <div class="folder-header">{{ dir_name | capitalize }}</div>
    <div class="folder-blurb">{{ category_blurb }}</div>

    {% assign displayed_paths = "" | split: "" %}

    <div class="resource-grid">
      {% comment %} 
        Manual External Link for RCC Acknowledgments
      {% endcomment %}
      {% if dir_name == "guides" %}
        <a href="https://rcc.uq.edu.au/about/acknowledging-rcc" class="item-card">
          <span class="item-link">How to Acknowledge Bunya and/or RCC</span>
        </a>
      {% endif %}

      {% comment %} 
        1. Registry Items: We must find the Page Object for the Registry Key 
        to get the correct compiled .url
      {% endcomment %}
      {% for entry in site.data.registry %}
        {% if entry[0] contains dir_name %}
          {% assign reg_path = entry[0] %}
          {% assign page_obj = site.pages | where: "path", reg_path | first %}
          
          {% if page_obj %}
            <a href="{{ page_obj.url | relative_url }}" class="item-card">
              <span class="item-link">{{ entry[1].title }}</span>
            </a>
          {% else %}
            {% comment %} If it's a static file (PDF) not in site.pages {% endcomment %}
            <a href="{{ reg_path | relative_url }}" class="item-card">
              <span class="item-link">{{ entry[1].title }}</span>
            </a>
          {% endif %}
          {% assign displayed_paths = displayed_paths | push: reg_path %}
        {% endif %}
      {% endfor %}

      {% comment %} 
        2. Weighted Markdown Pages (not already in registry)
      {% endcomment %}
      {% assign weighted_pages = site.pages | where_exp: "p", "p.path contains dir_name" | where_exp: "p", "p.weight != nil" | sort: "weight" %}
      {% for p in weighted_pages %}
        {% unless displayed_paths contains p.path %}
          <a href="{{ p.url | relative_url }}" class="item-card">
            <span class="item-link">{{ p.title }}</span>
          </a>
          {% assign displayed_paths = displayed_paths | push: p.path %}
        {% endunless %}
      {% endfor %}
    </div>

    {% comment %} 
      3. Additional Docs (Dropdown)
    {% endcomment %}
    {% assign extra_docs = "" | split: "" %}
    
    {% assign unweighted_md = site.pages | where_exp: "p", "p.path contains dir_name" | where_exp: "p", "p.weight == nil" %}
    {% for p in unweighted_md %}
      {% if p.name != "index.md" and p.title %}
        {% unless displayed_paths contains p.path %}
          {% assign extra_docs = extra_docs | push: p %}
        {% endunless %}
      {% endif %}
    {% endfor %}

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
