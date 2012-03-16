CKeditor+carrierwave'in kullanıldığı Rails 3.2 uygulamasıdır.

# Size düşen nedir?

Aşağıdaki şekilde çalışın,

    $ git clone git@github.com:seyyah/ckeditor-carrierwave.git
    $ cd ckeditor-carrierwave/
    $ git checkout rails3.2
    $ bundle
    $ rake db:migrate
    $ rails s --binding=1.2.3.4

Test: http://1.2.3.4:3000/main/index
Heroku: http://ckeditor-carrierwave.heroku.com/main/index

> Heroku tarafında resim upload sorunu mevcut.
> Şöyle bir çözüm önerilmiş:
> https://github.com/jnicklas/carrierwave/wiki/How-to%3A-Make-Carrierwave-work-on-Heroku

# Neden?

Çok sayıda WYSIWYG editör ve/veya dosya yöneticisi ve/veya dosya uploader
mevcut,

- mercury: http://jejacks0n.github.com/mercury/

> GUI'si çok hoş fakat dosya upload desteği henüz yok.

- tinyMCE: http://www.tinymce.com

> güçlü bir aday fakat dosya upload'eru için ücret ödemek gerekiyor.
> Ayrıca öncelikle PHP ve .NET için uyumlu, rails için farklı çalışma
> gruplarınca çalışmalar mevuct: tinymce-rails, tinymce-hummer gibi.

- widgEditor: http://www.themaninblue.com/experiment/widgEditor/

> En son 2008'de güncellenmiş ve resim/dosya upload imkanı yok!

- filemanager: https://github.com/scorpio/filemanager

> 2 yıl geçmiş bir ekleme yok!

- boxroom: http://boxroom.rubyforge.org/

> Dosya upload ve nette paylaşım olanağı sunuyor. Rails3.1. Editör ile kullanıma
> uygun değil!

- mediabrowser: https://github.com/vinyll/rails-mediabrowser

> rails3.2 uyumsuzluğu var!

- Diğerleri: aloha, yui-editor, nicedit

# How to build this app from scratch

  gem install rails --pre
  rails new rails_3_1_with_ckeditor_and_carrierwave --skip-bundle
  cd rails_3_1_with_ckeditor_and_carrierwave

Add this to your gemfile

  # if you need carrierwave you should use this line for now
  gem "ckeditor", :git => "git://github.com/galetahub/ckeditor.git"

  gem "carrierwave"
  gem "mini_magick"

Run

  bundle install

There is a bug in installation generator (which I'll fix eventually) for Rails 3.1 and you must create public/javascripts directory manually (cause Rails 3.1 doesn't need it by default):

  mkdir public/javascripts

Run generators:

  rails generate ckeditor:install
  rails generate ckeditor:models --orm=active_record --backend=carrierwave

Migrate database (if you're using ActiveRecord):

  rake db:migrate

Generate your controller and view:

  rails generate controller main index


And paste this lines to app/views/main/index.html.erb:

  <%= javascript_include_tag "/javascripts/ckeditor/ckeditor.js" %>
  <%= cktext_area_tag("test_area", "Ckeditor is the best") %>

Start the server

  rails server

and visit

  http://localhost:3000/main/index
