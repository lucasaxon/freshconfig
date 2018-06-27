<h2>Encabezado:</h2>
Modifica el encabezado del html del portal.

```
<!-- Title for the page -->
<title> {{ meta.title }} : {{ portal.name }} </title>

<!-- Meta information -->
{{ meta | default_meta }}

<!-- Responsive setting -->
{{ portal | default_responsive_settings }}
```

<h2>Encabezado:</h2>
Cambiar el área del encabezado del portal de asistencia

```
{% if  portal.current_page != 'csat_survey' %}
	<header class="banner">
		<div class="banner-wrapper page">
			<div class="banner-title">
				{{ portal | logo }}
				<h1 class="ellipsis heading">{{portal.name|h}}</h1>
			</div>
			<nav class="banner-nav">
				{{ portal | welcome_navigation }}
			</nav>
		</div>
	</header>
	<nav class="page-tabs">
	<div class="page no-padding">
		{% if portal.tabs.size > 0 %}
			<a data-toggle-dom="#header-tabs" href="#" data-animated="true" class="mobile-icon-nav-menu show-in-mobile"></a>
			<div class="nav-link" id="header-tabs">
				{% for tab in portal.tabs %}
					{% if tab.url %}
						<a href="{{tab.url}}" class="{% if tab.tab_type == portal.current_tab %}active{% endif %}">{{ tab.label }}</a>
					{% endif %}
				{% endfor %}
			</div>
		{% endif %}
		</div>
	</nav>

<!-- Search and page links for the page -->
{% if portal.current_tab and portal.current_tab != "home" %}
	<section class="help-center-sc rounded-6">	
		<div class="page no-padding">
		<div class="hc-search">
			<div class="hc-search-c">
				{% snippet search_form %}
			</div>
		</div>
		<div class="hc-nav {% if portal.contact_info %} nav-with-contact {% endif %}">			
          <!-- LUCAS Barra de new Ticket  !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! -->
			{{ portal | helpcenter_navigation }}
      <!-- Hasta aca -->
		</div>
		</div>
	</section>
{% endif %}
{% else %} 
	<header class="banner">
		<div class="banner-wrapper">
			<div class="banner-title">
				{{ portal | logo : true }}
				<h1 class="ellipsis heading">{{portal.name|h}}</h1>
			</div>
		</div>
	</header>
{% endif %}

```
<h2>Pie de página:</h2>
Cambiar el pie de página del portal de asistencia

```
{% if  portal.current_page != 'csat_survey' %}
	<footer class="footer rounded-6">
		<nav class="footer-links page no-padding">
			{% if portal.tabs.size > 0 %}
					{% for tab in portal.tabs %}
						<a href="{{tab.url}}" class="{% if tab.tab_type == current_tab %}active{% endif %}">{{ tab.label }}</a>
					{% endfor %}
			{% endif %}
			{{ portal | link_to_privacy_policy }}
			{{ portal | link_to_cookie_law }}
		</nav>
	</footer>
	{{ portal | portal_copyright }}
{% endif %}
```

<h2>Distribución de la página:</h2>
Personalizar toda la distribución de portal de asistencia

```
{{ header }}
<div class="page">
	
	
	<!-- Search and page links for the page -->
	{% if portal.current_tab and portal.current_tab == "home" %}
		<section class="help-center rounded-6">	
			<div class="hc-search">
				<div class="hc-search-c">
					<h2 class="heading hide-in-mobile">{% translate header.help_center %}</h2>
					{% snippet search_form %}
				</div>
			</div>
			<div class="hc-nav {% if portal.contact_info %} nav-with-contact {% endif %}">				
				{{ portal | helpcenter_navigation }}
			</div>
		</section>
	{% endif %}

	<!-- Notification Messages -->
	{{ page_message }}

	{% if portal.current_page != "user_signup" and portal.current_page != "submit_ticket" %}
	<div class="c-wrapper">		
		{{ content_for_layout }}
	</div>
	{% elsif portal.current_page == "submit_ticket" %}
	<div class="c-wrapper">		
		<div class="new_ticket_page">
		{{ content_for_layout }}
		</div>
	</div>
	{% else %}
	<div class="signup-page">
	<div class="signup-wrapper">
	{{ content_for_layout }}
	</div>
	</div>
	{% endif %}

	

</div>
{{ footer }}
```
