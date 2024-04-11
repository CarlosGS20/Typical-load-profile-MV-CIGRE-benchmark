
# Prueba



<p align="center" width="100%">
    <img src="https://github.com/CarlosGS20/Typical-load-profile-MV-CIGRE-benchmark/blob/main/Profiles_consumption_disaggregation.jpg" width="400" height="400">
</p>
<p style="text-align: center;">Sample text with center alignment</p>
## _includes/image.html
<div class="image-wrapper" >
  {% if include.url %}
  <a href="{{ include.url }}" title="{{ include.title }}" target="_blank">
  {% endif %}
      <img src="{{ site.url }}/{{ include.img }}" alt="{{ include.title }}"/>
  {% if include.url %}
  </a>
  {% endif %}
  {% if include.caption %}
      <p class="image-caption">{{ include.caption }}</p>
  {% endif %}
</div>

## Include the image in your post and specify a caption with this tag
{% include image.html img="assets/images/image_file" title="" caption="" %}
