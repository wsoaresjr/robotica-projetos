---
layout: default
title: "Projetos de Robótica"
---

<section class="mb-8">
  <div class="py-8">
    <h1 class="text-4xl font-extrabold">Catálogo de Projetos de Robótica</h1>
    <p class="text-slate-600 dark:text-slate-400 max-w-2xl mt-2">Cada projeto aqui é um post com capa, descrição, materiais, links de repositório e demo. Use a busca ou filtre por tags.</p>
  </div>
  <div class="flex flex-wrap gap-3 items-center">
    <input id="q" class="flex-1 min-w-[260px] max-w-[420px] px-4 py-2 rounded-xl border border-slate-200 dark:border-slate-700 bg-white dark:bg-slate-950" type="search" placeholder="Buscar por título ou tags…"/>
    <select id="tag" class="px-4 py-2 rounded-xl border border-slate-200 dark:border-slate-700 bg-white dark:bg-slate-950">
      <option value="">Todas as tags</option>
      {% assign all = site.tags | sort %}
      {% for pair in all %}
        {% assign tag = pair[0] %}
        <option value="{{ tag | downcase }}">{{ tag }}</option>
      {% endfor %}
    </select>
  </div>
</section>

<section id="tags" class="mb-10">
  <h2 class="text-xl font-semibold mb-3">Tags populares</h2>
  <div class="flex flex-wrap gap-2">
    {% assign shown = 0 %}
    {% for pair in site.tags %}
      {% assign tag = pair[0] %}
      {% assign posts_for = pair[1] %}
      <a href="#" data-tag="{{ tag | downcase }}" class="pill hover:border-brand-500 hover:text-brand-700 dark:hover:text-brand-300">{{ tag }} ({{ posts_for | size }})</a>
      {% assign shown = shown | plus: 1 %}
      {% if shown >= 12 %}{% break %}{% endif %}
    {% endfor %}
  </div>
</section>

<div id="grid" class="grid gap-4 sm:grid-cols-2 lg:grid-cols-3">
  {% for post in site.posts %}
    <article class="card bg-white dark:bg-slate-950 border border-slate-200 dark:border-slate-800 rounded-2xl overflow-hidden hover:shadow-lg transition">
      <a href="{{ site.baseurl }}{{ post.url }}" class="block">
        {% if post.image %}
          <div class="aspect-video bg-slate-100 dark:bg-slate-800 overflow-hidden">
            <img src="{{ site.baseurl }}{{ post.image }}" alt="{{ post.title }}" class="w-full h-full object-cover"/>
          </div>
        {% endif %}
        <div class="p-4">
          <h3 class="font-bold text-lg">{{ post.title }}</h3>
          {% if post.excerpt %}
            <p class="text-slate-600 dark:text-slate-400 text-sm mt-1 mb-3">{{ post.excerpt | strip_html | truncate: 130 }}</p>
          {% endif %}
          {% if post.tags %}
            <div class="flex flex-wrap gap-2 mb-2">
              {% for t in post.tags %}<span class="pill">{{ t }}</span>{% endfor %}
            </div>
          {% endif %}
          <span class="text-slate-500 dark:text-slate-400 text-xs">{{ post.date | date: "%d/%m/%Y" }}</span>
        </div>
      </a>
    </article>
  {% endfor %}
</div>

<div id="empty" class="hidden text-slate-600 dark:text-slate-400 border border-dashed border-slate-300 dark:border-slate-700 rounded-xl p-6 mt-6">Nenhum projeto encontrado para esse termo/tag.</div>

<script>
(function(){
  const $q = document.getElementById('q');
  const $tag = document.getElementById('tag');
  const $grid = document.getElementById('grid');
  const $empty = document.getElementById('empty');

  function apply(){
    const q = ($q?.value||'').trim().toLowerCase();
    const tg = ($tag?.value||'').trim().toLowerCase();
    let visible = 0;
    Array.from($grid.children).forEach(card=>{
      const text = (card.textContent||'').toLowerCase();
      const okQ = !q || text.includes(q);
      const okT = !tg || text.includes(tg);
      const show = okQ && okT;
      card.style.display = show? '' : 'none';
      if(show) visible++;
    });
    $empty.classList.toggle('hidden', !!visible);
  }

  $q?.addEventListener('input', apply);
  $tag?.addEventListener('change', apply);

  document.querySelectorAll('[data-tag]').forEach(el=>{
    el.addEventListener('click', (e)=>{
      e.preventDefault();
      const t = el.getAttribute('data-tag')||'';
      const opt = Array.from($tag.options).find(o=>o.value===t);
      if(opt){ $tag.value = t; }
      apply();
      window.scrollTo({ top: document.getElementById('grid').offsetTop - 80, behavior: 'smooth' });
    });
  });

  apply();
})();
</script>