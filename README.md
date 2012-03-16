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
