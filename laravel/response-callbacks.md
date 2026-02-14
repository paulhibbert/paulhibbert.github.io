# afterResponse callback in Http Facade

Adds ability to inspect and mutate the response fluently.

There is a complete example in the PR, which is pretty self explanatory:

```php
class ShopifyResponse extends Response
{
    public function __construct($response)
    {
        $this->response = $response;
        $this->decoded = json_decode($this->body(), true, flags: JSON_THROW_ON_ERROR);
    }

    public function getQueryCost(): array {
        // ...
    }
}

Http::macro('shopifyRequest', function (ShopCredentials $shopCreds) {
    return Http::acceptJson()
        ->withHeader('X-Shopify-Access-Token', $shopCreds->token)
        ->baseUrl("https://{$shopCreds->shop_domain}.myshopify.com/admin/api/2025-10/")
        ->afterResponse(
            // Report any deprecation notices that were in the header
            function (Response $response) use ($shopCreds) {
                $header = $response->header('X-Shopify-API-Deprecated-Reason');
                if ($header) {
                    event(new ShopifyDeprecationNotice($shopCreds->shop, $header);
                }
         })
        ->afterResponse(
            // Map the response into our own custom response class
            fn (Response $response) => new ShopifyResponse($response->toPsrResponse())
        )
        ->afterResponse(
            // Report the cost of the query
            static fn (ShopifyResponse $response) => QueryCostResponse::report(
                $response->getQueryCost(),
                $shopCreds->shop
            )
        )
});

$r = Http::shopifyRequest($someShopCredentials)->post('graphql.json', ['query' => 'some graphql query']);
```

If the callback returns the response or a class which extends `\Illuminate\Http\Client\Response` the return from the callback is returned instead of the response passed to the callback.
