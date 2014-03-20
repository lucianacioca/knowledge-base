
=======
MongoDB
=======

MongoDB client
==============

List databases : ::

    show dbs

Connect to database : ::

    use my_database

Drop database : ::

    use my_database
    db.dropDatabase()

List collections : ::

    use my_database
    show collections

View collection content : ::

    use my_database
    db.my_collection.find()

Insert entry into collection : ::

    db.my_collection.insert({
        key1: 'value1',
        key2: 'value2',
    })

Remove all entries in collection : ::

    db.my_collection.remove()

