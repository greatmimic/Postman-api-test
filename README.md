# ReqRes Postman API Portfolio
 
API testing collection built with Postman, using [ReqRes](https://reqres.in) as a real hosted backend. Tests cover a full CRUD workflow on a `products` collection.
 
---
 
## Collection Overview
 
| Request | Method | Description |
|---|---|---|
| Get full list of products | GET | Retrieves all product records |
| Get single product | GET | Retrieves one product by ID |
| Add product | POST | Creates a new product record |
| Update product | PUT | Updates an existing product by ID |
| Delete product | DELETE | Deletes a product by ID |
 
---

## Tests
 
### Get full list of products
- Status is 200
- Response data is an array
- Array contains at least one item
- Each item has `id`, `created_by`, `name`, `price`, `category`, `in_stock`
- Each `id` is a string
- Each `created_by` is a number
- Each `data` field is an object
- Each `name` is a string
- Each `price` is a number greater than 0
- Each `category` is a string
- Each `in_stock` is a boolean
 
### Get single product
- Status is 200
- Response `id` matches the requested `{{id}}` environment variable
- All fields are present: `id`, `collection_id`, `project_id`, `app_user_id`, `created_by`, `created_at`, `updated_at`, `deleted_at`, `data`
- Nested `data` object contains: `name`, `price`, `category`, `in_stock`
 
### Add product
- Status is 201
- Response contains a valid `id` (string)
- Saves new product ID to `{{new_product_id}}` environment variable
- Response data matches the request body (`name`, `price`, `category`, `in_stock`)
 
---

## RestCountry — Country Data
 
Read-only queries against the RestCountries public API, including a negative test case for invalid input.
 
### Requests
 
| Request | Method | Endpoint |
|---|---|---|
| Get all countries | GET | `/all?fields=name,capital,population,region,currencies` |
| Get by country name | GET | `/name/{{country_name}}` |
| Get country by region | GET | `/region/{{region}}?fields=name,population,capital,currencies,region` |
| Filter country by currency | GET | `/currency/{{currency}}?fields=name,currencies` |
| Get by invalid country name | GET | `/name/{{invalid_country_name}}` |
 
### Tests
 
**Get all countries**
- Status is 200
- Response is an array
- Array contains more than one country
- Each country has `name`, `capital`, `population`, `currencies`, `region`
- Each population is a positive number
- Sets a random country name to `{{country_name}}` environment variable automatically
 
**Get by country name**
- Status is 200
- Response is an array
- Country name returned matches `{{country_name}}`
- Country has a capital
- Country has a valid population (number greater than 0)
 
**Get country by region**
- Status is 200
- Response is an array
- All countries belong to the requested `{{region}}`
- Each country has `name` and a valid population
 
**Filter country by currency**
- Status is 200
- Response is an array
- Each country has a `currencies` field
- Each country has a `name` field
- Each country's currency keys include the requested `{{currency}}`
 
**Get by invalid country name** *(negative test)*
- Status is 404
- Response contains an error `status` field equal to 404
- Response contains an error `message` field (string)
 
---
