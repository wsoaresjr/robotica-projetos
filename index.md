# Arquivo: index.md (homepage com Tailwind, busca e "tags populares")
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


// Clique em tags populares preenche o filtro
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