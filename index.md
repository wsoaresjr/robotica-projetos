---
layout: default
title: "Projetos de Robótica"
---

<section class="page-hero" style="padding: 2rem 0;">
  <h1 style="margin:0;">Catálogo de Projetos de Robótica</h1>
  <p style="color:#6b7280; max-width: 56ch;">
    Cada projeto abaixo é um post: capa, descrição, materiais, links de repositório e demo.
  </p>
</section>

<input id="busca" type="search" placeholder="Buscar por nome ou tags…" style="width:100%; max-width:420px; padding:.6rem .8rem; border-radius:12px; border:1px solid #e5e7eb; margin:.5rem 0 1.5rem;" />

<div id="grid" class="cards" style="display:grid; gap:1rem; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));">
  {% for post in site.posts %}
    <article class="card" data-text="{{ post.title | downcase }} {{ post.tags | join: ' ' | downcase }}" style="border:1px solid #e5e7eb; border-radius:16px; overflow:hidden;">
      <a href="{{ site.baseurl }}{{ post.url }}" style="text-decoration:none; color:inherit;">
        {% if post.image %}
          <div style="aspect-ratio:16/9; background:#f1f5f9; overflow:hidden;">
            <img src="{{ site.baseurl }}{{ post.image }}" alt="{{ post.title }}" style="width:100%; height:100%; object-fit:cover;">
          </div>
        {% endif %}
        <div style="padding:1rem;">
          <h3 style="margin:.25rem 0 0;">{{ post.title }}</h3>
          {% if post.excerpt %}
            <p style="color:#6b7280; font-size:.95rem; margin:.5rem 0 1rem;">{{ post.excerpt | strip_html | truncate: 120 }}</p>
          {% endif %}
          {% if post.tags %}
            <div style="display:flex; gap:.4rem; flex-wrap:wrap; margin-bottom:.5rem;">
              {% for t in post.tags %}
                <span style="font-size:.75rem; padding:.2rem .5rem; border:1px solid #e5e7eb; border-radius:999px; background:#f8fafc;">{{ t }}</span>
              {% endfor %}
            </div>
          {% endif %}
          <span style="color:#64748b; font-size:.85rem;">Publicado em {{ post.date | date: "%d/%m/%Y" }}</span>
        </div>
      </a>
    </article>
  {% endfor %}
</div>

<script>
  (function () {
    const input = document.getElementById('busca');
    const cards = Array.from(document.querySelectorAll('.card'));
    input?.addEventListener('input', function () {
      const q = (this.value || '').toLowerCase();
      cards.forEach(card => {
        const txt = card.getAttribute('data-text') || '';
        card.style.display = (!q || txt.includes(q)) ? '' : 'none';
      });
    });
  })();
</script>
