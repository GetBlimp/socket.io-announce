socket.io-announce in Python
============================

.. image:: https://travis-ci.org/GetBlimp/socket.io-announce.png?branch=master
    :target: https://travis-ci.org/GetBlimp/socket.io-announce


Lightweight infrastructure broadcast for use with Socket.io RedisStore.
This was ported from `dshaw/socket.io-announce`_ a Node.js project.
Thanks to `@dshaw`_.

Install
-------

.. code:: bash

    pip install socket.io-announce

Use anywhere in your stack, independent of other socket.io servers.
-------------------------------------------------------------------

.. code:: python

    from announce import Announce

    announce = Announce()
    announce.emit('status', {'msg': 'Going down for maintenance in 15 minutes', 'countdown': 10000})

Emit to all users.
------------------

.. code:: python

    announce.send('Hello, world!')
    announce.emit('quote', {'symbol':'APPL', 'price': 5000})

Target socket.io rooms.
-----------------------

.. code:: python

    announce.send('Yoyo yo!', room='boardroom')
    announce.emit('tweet', {'id': '1', 'user': '@dshaw', 'text': 'Keeping things small...'}, room='nodeup')
    
Target socket.io namespaces (with rooms too).
---------------------------------------------

.. code:: python

    announce = Announce(namespace='/namespace')
    announce.emit('episode', {'url': 'http://www.nodeup.com/twentyfour'}, room='nodeup')

Custom JSON Serialization
-------------------------

If you run into JSON errors trying to serialize data types like date/time/timedelta, decimal, generators, or any other
that is not supported by the standard json library, you'll probably need to use a custom JSONEncoder.

.. code:: python
    
    def custom_json_dumps(data):
        return json.dumps(data, cls=CustomJSONEncoder)
    
    announce = Announce(namespace='/namespace', json_dumps=custom_json_dumps)
    announce.emit('episode', {'date': datetime.datetime.today()}, room='nodeup')


License
-------

(The MIT License)

Copyright (c) 2014 Blimp LLC - Giovanni Collazo

Permission is hereby granted, free of charge, to any person obtaining a
copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be included
in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS
OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

.. _dshaw/socket.io-announce: https://github.com/dshaw/socket.io-announce

.. _@dshaw: https://twitter.com/dshaw
