> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# The Secret Endpoint

> Get a special gift from Resend.

You'll need an API key to run this - [get one here](https://resend.com/api-keys).

## Body Parameters

<ParamField body="first_name" type="string" required>
  First name
</ParamField>

<ParamField body="last_name" type="string" required>
  Last name
</ParamField>

<ParamField body="address1" type="string" required>
  Address line
</ParamField>

<ParamField body="address2" type="string">
  Additional address info (e.g., apartment number, suite, floor)
</ParamField>

<ParamField body="city" type="string" required>
  City name
</ParamField>

<ParamField body="state" type="string" required>
  State codes are based on the [ISO 3166-2
  standard](https://en.wikipedia.org/wiki/ISO_3166-2:US) and are two letters
  long
</ParamField>

<ParamField body="country" type="string" required>
  Country codes are based on the [ISO 3166-1
  alpha-2](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes)
  standard and are two letters long
</ParamField>

<ParamField body="zip" type="string" required>
  ZIP code
</ParamField>

<ParamField body="cpf" type="string">
  In case of Brazil country this field becomes required. The CPF format is
  000.000.000-00 (14 characters).
</ParamField>

<RequestExample>
  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/secret' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "first_name": "Steve",
    "last_name": "Wozniak",
    "address1": "4300 El Camino Real",
    "address2": "Suite 100",
    "city": "Los Altos",
    "state": "CA",
    "country": "US",
    "zip": "94022"
  }'
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "message": "Check your mailbox in a few days :)"
  }
  ```
</ResponseExample>
