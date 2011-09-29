Egret
=====
A really minimal couchdb application building thingy. It consists of a single Python module which depends only on the Python Standard Library.

It works like you probably expected CouchApp to work, aside from not being a stupid furniture pun.

Stuff goes here:

    ./shows: shows
    ./lists: lists
    ./views: views
    ./updates: updates

In all cases, directory structures get mapped directly to objects in the design doc. For example:

    ./lists/bar.js ==> "lists": {"bar": "<contents of bar.js>"}

and

    ./views/foo/map.js
    --------------
    function(doc) {
        if(doc.type == "thinger")
            emit(doc._id, doc);
    }

    design doc
    ----------
    "views": {
        "foo": {
            "map": "function(doc) {\n  if(doc.type == \"thinger\")\n    emit(doc._id, doc);\n}"
         }
    }

And so on.

Everything in ./attachments gets uploaded as an attachment.

