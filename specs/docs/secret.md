> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# The Secret Endpoint

> Get a special gift from Resend.

You'll need an API key to run this - [get one here](https://resend.com/api-keys).

## Body Parameters

**first\_name** `string` *required*

First name

**last\_name** `string` *required*

Last name

**address1** `string` *required*

Address line

**address2** `string`

Additional address info (e.g., apartment number, suite, floor)

**city** `string` *required*

City name

**state** `string` *required*

State codes are based on the [ISO 3166-2
standard](https://en.wikipedia.org/wiki/ISO_3166-2:US) and are two letters
long

**country** `string` *required*

Country codes are based on the [ISO 3166-1
alpha-2](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes)
standard and are two letters long

**zip** `string` *required*

ZIP code

**cpf** `string`

In case of Brazil country this field becomes required. The CPF format is
000.000.000-00 (14 characters).

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

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "message": "Check your mailbox in a few days :)"
}
```
