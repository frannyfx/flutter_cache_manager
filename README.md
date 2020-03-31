# flutter_cache_manager

A CacheManager that allows you to download and cache files in the cache directory of the app based on **CUSTOM KEYS**. Various settings on how long to keep a file can be changed.

It uses the cache-control http header to efficiently retrieve files.

The more basic usage is explained here. See the complete docs for more info.

## How to install
Add the following to your *pubspec.yaml* file under `dependencies`:
```
flutter_cache_manager:
    git:
      url: git://github.com/frannyfx/flutter_cache_manager.git
      ref: develop
```

## Usage

The cache manager can be used to get a file on various ways
The easiest way to get a single file is call `.getSingleFile`.

```
    var file = await DefaultCacheManager().getSingleFile(url, cacheKey);
```
`getFile(url, cacheKey)` returns a stream with the first result being the cached file and later optionally the downloaded file.

`downloadFile(url, cacheKey)` directly downloads from the web.

`getFileFromCache` only retrieves from cache and returns no file when the file is not in the cache.

`putFile` gives the option to put a new file into the cache without downloading it.

`removeFile` removes a file from the cache. 

`emptyCache` removes all files from the cache. 

## How it works
By default the cached files are stored in the temporary directory of the app. This means the OS can delete the files any time.

Information about the files is stored in a database using sqflite. The file name of the database is the key of the cacheManager, that's why that has to be unique.

This cache information contains the end date till when the file is valid and the eTag to use with the http cache-control.
