Plotur REST Reference - Trace(s)
================================

.. http:get:: /traces
    
    All of the traces available to the current user. Because this
    is very costly to do it always returns the empty set currently.

    **Example Request**:

    .. sourcecode:: http

        GET /traces HTTP/1.1
        Host: plotur.com
        Accept: application/json

    **Example Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Content-Type: application/json

        []

.. http:post:: /traces
    
    Create a new trace without any associated data.

    **Example Request**:

    .. sourcecode:: http

        POST /traces HTTP/1.1
        Host: plotur.com
        Accept: */*
        
        name=Whatever
        
        

    **Example Response**:

    .. sourcecode:: http

        HTTP/1.1 303 See Other
        Location: http://plotur.com/traces/4ykBEKmX
        Content-Type: text/plain
        


.. http:put:: /traces/(trace_id)/data
    
    Set the trace column data from a csv file.

    **Example Request**:

    .. sourcecode:: http

        PUT /traces/4ykBEKmX/data HTTP/1.1
        Host: plotur.com
        Accept: */*
        Content-Length: 52000
        Content-Type: text/csv
        Expect: 100-continue
        


    **Example Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Content-Type: text/plain
        


