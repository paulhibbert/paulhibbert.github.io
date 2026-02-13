# Clamp to restrict for example pagination

The pull request points to examples where there is no validation on the per_page property of the request opening an avenue for arbitrarily large result sets and expensive queries.

```php
$perPage = request()->integer('per_page', 50);
$perPage = request()->clamp('per_page', 1, 100, 50);
```

I guess its OK, still prefer validating the input.

```php
public function clamp($key, $min, $max, $default = 0)
{
    return Number::clamp($this->data($key, $default), $min, $max);
}
```

InteractsWithData is a trait also used by the `Fluent`, `UriQueryString`, `ValidatedInput`, and `ComponentAttributeBag` classes. This last class is exposed as the public `attributes` property of a `Component`, so assuming in a Blade component its possible to do something like `$this->attributes->clamp(...)` though not perhaps very useful unless somehow the component attributes are not fully controlled already.

There might be some use here with the `Fluent` class (and the `asFluent` cast). Since any array or iterable can be turned into a Fluent class, here is a perhaps far-fetched example:

```php
$preferences = fluent(['heightInMeters' => 3.0, 'age' => 16]);

$normalisedIQ = $preferences->clamp('iq', 100, 120, 110); // 110, uses default as key not found
$normalisedHeight = $preferences->clamp('heightInMeters', 1.2, 1.9) // 1.9, max used
$normalisedAge = $preferences->clamp('age', 18, 50) // 18, min uses
```
