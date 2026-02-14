# Pausing queues

Introduced in 12.40 and enhanced in 12.41.

In the queueManager there are now two additional methods for pausing a queue, and one for resuming manually.

```php
public function pause($connection, $queue)
{
    $this->app['cache']
        ->store()
        ->forever("illuminate:queue:paused:{$connection}:{$queue}", true);
}

public function pauseFor($connection, $queue, $ttl)
{
    $this->app['cache']
        ->store()
        ->put("illuminate:queue:paused:{$connection}:{$queue}", true, $ttl);
}
```

The framework has addition artisan commands to pause and resume an individual queue. There was no change to add the facility to pass an interval/integer to the PauseCommand.
