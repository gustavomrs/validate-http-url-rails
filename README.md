# Validator para urls HTTP/HTTPS

### Crie um recurso para validators em app/validators/ (caso ainda não tenha), e adicione a classe:

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

### Adicione o validate url: true para o seu atributo que contém a url:

```ruby
class WhateverClass < ActiveRecord::Base
  validates :my_url, url: true
end
```
