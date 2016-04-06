# Validator para urls HTTP(S)

### First step: Create a resource at app/validators/url_validator with the follow content:

```ruby
class UrlValidator < ActiveModel::EachValidator
  # Realiza a validação de url
  #
  # @return [NilClass] Sem erro de validação
  # @return [ActiveModel::Errors] Erros de validação.
  def validate_each(record, attribute, value)
    record.errors[attribute] << ("Deve ser uma URL válida.") unless url_valid?(value)
  end

  # Valida se a url está com http / https
  #
  # @return [TrueClass] URL válida.
  # @return [FalseClass] URL inválida.
  def url_valid?(url)
    url = URI.parse(url) rescue false
    url.kind_of?(URI::HTTP) || url.kind_of?(URI::HTTPS)
  end
end
```

### Add the validation for your url attribute inside your model

```ruby
class WhateverClass < ActiveRecord::Base
  validates :my_url, url: true
end
```

### Feel free to talk with me in case of doubts, suggestions or whatever thing! I will appreciate it!
