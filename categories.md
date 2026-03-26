---
layout: page
permalink: /categories/
title: Categories
---

<style>
.category-nav {
  margin-bottom: 30px;
  display: flex;
  align-items: center;
  gap: 10px;
}

.category-nav label {
  font-weight: bold;
  margin-right: 10px;
}

.category-nav select {
  padding: 8px 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  background-color: #f8f9fa;
}

.category-nav select:hover {
  border-color: #3498db;
  background-color: #fff;
}

.archive-group {
  margin-bottom: 40px;
  padding: 20px 0;
  border-bottom: 2px solid #f0f0f0;
}

.archive-group:last-child {
  border-bottom: none;
}

.category-head {
  color: #2c3e50;
  font-size: 24px;
  margin: 20px 0 15px 0;
  padding-bottom: 10px;
  border-bottom: 3px solid #3498db;
}

.archive-item {
  margin-left: 20px;
  margin-bottom: 12px;
  padding: 10px;
  background-color: #f8f9fa;
  border-left: 4px solid #3498db;
  border-radius: 2px;
}

.archive-item h4 {
  margin: 0;
  color: #2c3e50;
  font-size: 16px;
}

.archive-item a {
  text-decoration: none;
  color: #3498db;
  font-weight: 500;
}

.archive-item a:hover {
  text-decoration: underline;
  color: #2980b9;
}

.archive-item p {
  margin: 5px 0 0 0;
  color: #7f8c8d;
  font-size: 14px;
}
</style>

<div class="category-nav">
  <label for="category-select">Jump to category:</label>
  <select id="category-select" onchange="jumpToCategory(this.value)">
    <option value="">-- Select a category --</option>
    {% for category in site.categories %}
    {% capture category_name %}{{ category | first }}{% endcapture %}
    <option value="#{{ category_name | slugize }}">{{ category_name }}</option>
    {% endfor %}
  </select>
</div>

<script>
function jumpToCategory(anchor) {
  if (anchor) {
    window.location.hash = anchor;
    document.querySelector(anchor).scrollIntoView({ behavior: 'smooth' });
  }
}
</script>

<div id="archives">
  {% for category in site.categories %}
  <div class="archive-group">
    {% capture category_name %}{{ category | first }}{% endcapture %}
    <div id="{{ category_name | slugize }}"></div>
    <h3 class="category-head">{{ category_name }}</h3>
    {% for post in site.categories[category_name] %}
    <article class="archive-item">
      <h4>
        <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
      </h4>
      <p>📅 {{ post.date | date: "%B %d, %Y" }}</p>
    </article>
    {% endfor %}
  </div>
  {% endfor %}
</div>