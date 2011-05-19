<div id="ui-tabs-1" class="section">
		<h2 class="section-title">Recent</h2>
		<ul>
			{% for post in site.posts limit: 5 %}
				<li><a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a></li>
			{% endfor %}
		</ul>
</div>
<div id="ui-tabs-2" class="section">
		<h2 class="section-title">Categories</h2>
		<ul>
			{% for topic in site.iterable.categories %}
				<li><a href="/categories/{{ topic.name }}">{{ topic.name }}</a></li>
			{% endfor %}
		</ul>
</div>
