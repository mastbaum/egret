Egret
=====
A really minimal couchdb application building thingy. It consists of a single Python module which depends only on the Python Standard Library.

It works like you probably expected CouchApp to work, aside from not being a stupid furniture pun.

Usage:

    egret create
    - Create directory structure for a new couch app

    egret push db_url
    - push couch app in cwd to the couchdb server

    egret pushdata db_url file
    - upload documents to the couchdb server. file must contain a list of
      dictionaries, e.g. [{"_id": "foo", "bar": "baz"}, {...}]

      (caveat: this uses the couchdb bulk document api, so all features apply
      including not overwriting without the right _rev.)

    egret createdb db_url
    - create a database on the couchdb server. this is done automatically by
      push and pushdata if necessary

    In all cases, the format of db_url is (bracketed means optional):

        [http(s)://][user:password@]server/dbname

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

