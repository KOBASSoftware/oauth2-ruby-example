# OAuth 2.0 & Ruby Kobas Example

```ruby
require 'oauth2'

client_id = '' # Provided by Kobas
client_secret = '' # Provided by Kobas
client_scopes = '' # Provided by Kobas
kobas_company_id = '' # Provided by Kobas

oauth_domain = 'https://oauth.kobas.co.uk' # Will only change if you are using Kobas training mode.
api_domain = 'https://api.kobas.co.uk/v3' # Will only change if you are using Kobas training mode.


# Setup the client
client = OAuth2::Client.new(client_id, client_secret, :site => oauth_domain, :authorize_url => '/authorize', :token_url => '/access_token', :connection_opts => {:headers => {'x-kobas-company-id' => kobas_company_id}})

# Request the token
token = client.client_credentials.get_token({:scope => client_scopes}, :headers => {'x-kobas-company-id' => kobas_company_id})

# Make API request using token
response = token.get(api_domain + '/venue', :headers => {'x-kobas-company-id' => kobas_company_id})

## The result
print response.body
```