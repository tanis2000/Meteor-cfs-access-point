## cfs-access-point Public API ##

CollectionFS, add ddp and http accesspoint capability

_API documentation automatically generated by [docmeteor](https://github.com/raix/docmeteor)._

-

### <a name="FS.HTTP.setBaseUrl"></a>*fsHttp*.setBaseUrl(newBaseUrl)&nbsp;&nbsp;<sub><i>Anywhere</i></sub> ###

*This method __setBaseUrl__ is defined in `FS.HTTP`*

__Arguments__

* __newBaseUrl__ *{String}*  

 Change the base URL for the HTTP GET and DELETE endpoints.


__Returns__  *{undefined}*


> ```FS.HTTP.setBaseUrl = function setBaseUrl(newBaseUrl) { ...``` [access-point-common.js:13](access-point-common.js#L13)


-

### <a name="FS.File.prototype.url"></a>*fsFile*.url([options])&nbsp;&nbsp;<sub><i>Anywhere</i></sub> ###

*This method __url__ is defined in `prototype` of `FS.File`*

__Arguments__

* __options__ *{object}*  (Optional)
    * __store__ *{string}*  (Optional)

    Name of the store to get from. If not defined,

    * __auth__ *{boolean}*  (Optional, Default = null)

    Wether or not the authenticate

    * __download__ *{boolean}*  (Optional, Default = false)

    Should headers be set to force a download

    * __brokenIsFine__ *{boolean}*  (Optional, Default = false)

    Return the URL even if


the first store defined in `options.stores` for the collection is used.
we know it's currently a broken link because the file hasn't been saved in
the requested store yet.

Return the http url for getting the file - on server set auth if wanting to
use authentication on client set auth to true or token

> ```FS.File.prototype.url = function(options) { ...``` [access-point-common.js:52](access-point-common.js#L52)


-

### <a name="FS.HTTP.publish"></a>*fsHttp*.publish(collection, func)&nbsp;&nbsp;<sub><i>Server</i></sub> ###

*This method __publish__ is defined in `FS.HTTP`*

__Arguments__

* __collection__ *{[FS.Collection](#FS.Collection)}*  
* __func__ *{Function}*  

 Publish function that returns a cursor.


__Returns__  *{undefined}*


Publishes all documents returned by the cursor at a GET URL
with the format baseUrl/record/collectionName. The publish
function `this` is similar to normal `Meteor.publish`.

> ```FS.HTTP.publish = function fsHttpPublish(collection, func) { ...``` [access-point-server.js:32](access-point-server.js#L32)


-

### <a name="FS.HTTP.unpublish"></a>*fsHttp*.unpublish(collection)&nbsp;&nbsp;<sub><i>Server</i></sub> ###

*This method __unpublish__ is defined in `FS.HTTP`*

__Arguments__

* __collection__ *{[FS.Collection](#FS.Collection)}*  

__Returns__  *{undefined}*


Unpublishes a restpoint created by a call to `FS.HTTP.publish`

> ```FS.HTTP.unpublish = function fsHttpUnpublish(collection) { ...``` [access-point-server.js:57](access-point-server.js#L57)


-

### <a name="FS.HTTP.mount"></a>*fsHttp*.mount(mountPoints, selector_f)&nbsp;&nbsp;<sub><i>Server</i></sub> ###

*This method __mount__ is defined in `FS.HTTP`*

__Arguments__

* __mountPoints__ *{[array of string](#array of string)}*  

 mount points to map rest functinality on

* __selector_f__ *{function}*  

 [selector] function returns `{ collection, file }` for mount points to work with



> ```FS.HTTP.mount = function(mountPoints, selector_f) { ...``` [access-point-server.js:108](access-point-server.js#L108)


-

### <a name="FS.HTTP.unmount"></a>*fsHttp*.unmount([mountPoints])&nbsp;&nbsp;<sub><i>Server</i></sub> ###

*This method __unmount__ is defined in `FS.HTTP`*

__Arguments__

* __mountPoints__ *{[string ](#string )|[ array of string](# array of string)}*  (Optional)

 Optional, if not specified all mountpoints are unmounted




> ```FS.HTTP.unmount = function(mountPoints) { ...``` [access-point-server.js:206](access-point-server.js#L206)



-
### FS.Collection maps on HTTP pr. default on the following restpoints:
*
baseUrl + '/files/:collectionName/:id/:filename',
baseUrl + '/files/:collectionName/:id',
baseUrl + '/files/:collectionName'

Change/ replace the existing mount point by:
```js
unmount all existing
FS.HTTP.unmount();
Create new mount point
FS.HTTP.mount([
'/cfs/files/:collectionName/:id/:filename',
'/cfs/files/:collectionName/:id',
'/cfs/files/:collectionName'
]);
```
