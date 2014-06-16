# Active Admin Jcrop

## Cropping feature for Active Admin ##

### Instalation ###
Add to your Gemfile:
```ruby
gem 'activeadmin'
# Because active_admin_jcrop autoload modules by checking plugins you use, it's
# recommended to require it explictly before active_admin_jcrop
# e.g. if you use carrierwave
# gem 'carrierwave', :require => 'carrierwave'
gem 'active_admin_jcrop' #, git: 'git://github.com/Ricardonacif/active_admin_jcrop.git'
```

Configure your form to use Jcrop:

```ruby
# RAILS_ROOT/app/admin/post.rb
ActiveAdmin.register Post do

  jcropable
  
  form do |f|                         
    f.inputs "Details" do
      f.input :image, as: :jcrop
    end                      
    f.actions
  end              
  
end

```

If you use Paperclip, you need to do nothing else, active_admin_jcrop will append it's processor to your attachment automatically. If CarrierWave is used, please invoke :active_admin_crop in your uploader, and include both modules:

```ruby
class AvatarUploader < CarrierWave::Uploader::Base

  include CarrierWave::MiniMagick
  include ActiveAdminJcrop::AssetEngine::CarrierWave

  version :thumb do
    process :active_admin_crop
    process resize_to_fill: [500,320]
  end

end
```

Done! Now when there's a image attached, visit the edit page of the resource and click  on the button Crop Image to open the crop modal. You don't need to save this resource, cropping will be done via ajax.

## Dependencies ##

* MRI 1.9.3 (All above 1.8.6 should work, I only tested on 1.9.3)
* Rails 3.x
* MiniMagick

## Supported ORM ##

* ActiveRecord
* Mongoid

## Supported Asset Plugin ##

* CarrierWave
* Paperclip

## TODO ##

* make sure :active_admin_jcrop load after paperclip/carrierwave load
* automate :active_admin_jcrop for CarrierWave uploader
* write some specs
* add locale support

## Contributing ##

Any help is encouraged. Here are some ways you can contribute:

* by using it
* by telling people
* by reporting bugs or suggesting new features on github issue tracker
* by fixing bugs or implementing features

## Thanks ##

This gem was based on [Rails Admin Jcrop](https://github.com/janx/rails_admin_jcrop), so I'd like to thank those developers. Also, a special thanks to everyone that contributed to Active Admin and jCrop.