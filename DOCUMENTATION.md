## Documentation

You can see below the API reference of this module.

### `getCache(cacheFile)`
Utility method to load our json cache file. Failover to an empty object.
The native browserify cache object includes the sources. However,
since parsing large JSON files is extremely slow, it is much more more
performant to store the source content in their individual cache files,
and then reconstruct the cache object when reading.

#### Params

- **** `cacheFile`: [String] - full path to the json file

### `update()`
Walk through the dependency cache. If any dependency's modification time has changed, or the file has been
removed, invalidate the cache and remove the entry.

If the file implicitly requires other files due to a transform, invalidate them.
If the file is implicitly required as part of a transform, invalidate the files that require it.

### `write()`
Write the internal dependency cache to a file on the file system.

### `bundle(`cb`)`
Override the browserify `bundle` function. We need to intercept the call to see if any bundling is really
needed. When the cache is valid, we just return null. If `watch` is true, though, we setup the watchers on all
the files in the cache. Otherwise we do the bundling.

#### Params

- **** ``cb``: {Function} - optional callback

#### Return
- **** - either the stream from `_bundle` or `null` if the cache is valid.

