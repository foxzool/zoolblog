---
layout: post
title: 增加carrierwave对rails_admin的支持
category: rails
tags: rails
---

由于rails_admin默认只是支持paperclip, 所以使用carrierwave的话, 需要手动做些修改.

一共3个文件

{% highlight ruby %}
#app/views/rails_admin/main/_form_carrier_wave_file.html.haml
= label_tag "#{field.abstract_model.to_param}_#{field.name}", field.label
.input
  - if field.bindings[:object].send("#{field.name}_url")
    .row
      = link_to field.bindings[:object].send("#{field.name}_url")
      %br
      = form.check_box "remove_#{field.name}"
      = form.label "remove_#{field.name}", "Remove existing #{field.label.downcase}", :class => "inline"
  .row
    = form.file_field field.name, :class => "fileUploadField #{field.has_errors? ? "errorField" : nil}"
    = form.hidden_field "#{field.name}_cache"
{% endhighlight %}

{% highlight ruby %}
#app/views/rails_admin/main/_form_carrier_wave_image.html.haml

= label_tag "#{field.abstract_model.to_param}_#{field.name}", field.label
.input
  - image = field.bindings[:object].send(field.name)
  - if image.path # the most direct check of an assets existence I could see
    .row
      -# load a default 'version' if it exists. should really be set through rails_admin's DSL:
      - default_version = image.versions[:main]
      = image_tag default_version && default_version.url || image.url
      %br
      = form.check_box "remove_#{field.name}"
      = form.label "remove_#{field.name}", "Remove existing #{field.label.downcase}", :class => "inline"
  .row
    = form.file_field field.name, :class => "fileUploadField #{field.has_errors? ? "errorField" : nil}"
    = form.hidden_field "#{field.name}_cache"
{% endhighlight %}

{% highlight ruby %}
#config/initializers/rails_admin.rb

# Register a custom field factory and field type for CarrierWave if its defined
if defined?(::CarrierWave)
  module RailsAdmin::Config::Fields::Types
    # Field type that supports CarrierWave file uploads
    class CarrierWaveFile < RailsAdmin::Config::Fields::Types::FileUpload
      register_instance_option(:partial) do
        :form_carrier_wave_file
      end
    end
    
    # Field type that supports CarrierWave file uploads with image preview
    class CarrierWaveImage < CarrierWaveFile
      register_instance_option(:partial) do
        :form_carrier_wave_image
      end
    end
    
    # Register field type to the types registry
    register(:carrier_wave_file, CarrierWaveFile)
    register(:carrier_wave_image, CarrierWaveImage)
  end
  RailsAdmin::Config::Fields.register_factory do |parent, properties, fields|
    model = parent.abstract_model.model
    if model.kind_of?(CarrierWave::Mount) && model.uploaders.include?(properties[:name])
      type = properties[:name] =~ /image|picture|thumb/ ? :carrier_wave_image : :carrier_wave_file
      fields << RailsAdmin::Config::Fields::Types.load(type).new(parent, properties[:name], properties)
      true
    else
      false
    end
  end
end
{% endhighlight %}