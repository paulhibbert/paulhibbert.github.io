# Cache::withoutOverlapping()

Essentially shortcut for:

```php
Cache::lock('my-lock-key', 600)->block(10, function () {
    // my function
});
```

Signature is:

```php
/**
 * Execute a callback while holding an atomic lock on a cache mutex to prevent overlapping calls.
 *
 * @template TReturn
 *
 * @param  string  $key
 * @param  callable(): TReturn  $callback
 * @param  int  $lockSeconds
 * @param  int  $waitSeconds
 * @param  string|null  $owner
 * @return TReturn
 *
 * @throws \Illuminate\Contracts\Cache\LockTimeoutException
 */
public function withoutOverlapping($key, callable $callback, $lockSeconds = 600, $waitSeconds = 10, $owner = null)
{
    return $this->store->lock($key, $lockSeconds, $owner)->block($waitSeconds, $callback);
}
```
