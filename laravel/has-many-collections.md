# HasMany on Collections replaces containsManyItems

`containsManyItems` is deprecated and will be removed in Laravel 13, currently hands off to the new `HasMany` method, applies to both Collection and LazyCollection. The deprecated function accepted a callback, whereas the the new method is more flexible, accepting either a callback (a filter function to narrow the search), or a key value pair.

The new method:

```php
/**
 * Determine if the collection contains multiple items, optionally matching the given criteria.
 *
 * @param  (callable(TValue, TKey): bool)|string|null  $key
 * @param  mixed  $operator
 * @param  mixed  $value
 * @return bool
 */
public function hasMany($key = null, $operator = null, $value = null): bool
{
    $filter = func_num_args() > 1
        ? $this->operatorForWhere(...func_get_args())
        : $key;

    return $this
        ->unless($filter == null)
        ->filter($filter)
        ->take(2)
        ->count() === 2;
}
```

So

```php
$collection->hasMany(); // equivalent to ($collection->count() > 1)
$collection->hasMany('version', '=', 13);
$collection->hasMany(fn ($item) => $item['version'] === 12)

```
