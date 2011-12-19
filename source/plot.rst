Plotur REST Reference - Plot(s)
================================

.. http:post:: /plots
    
    Create a new trace without any associated data.

    **Example Request**:

    .. sourcecode:: http

        POST /plots HTTP/1.1
        Host: plotur.com
        Accept: */*
        
        name=Whatever&traces=4ykBEKmX


    **Example Response**:

    .. sourcecode:: http

        HTTP/1.1 303 See Other
        Location: http://plotur.com/plots/4ykBEKmX
        Content-Type: text/plain
        


.. http:put:: /plot/(plot_id)/traces/(trace_id)
    
    Add a trace to the plot. The body should be EMPTY. The plot_id and 
    trace_id should exist.

    **Example Request**:

    .. sourcecode:: http

        PUT /plots/4ykBEKmX/traces/4ykBEKmX HTTP/1.1
        Host: plotur.com
        Accept: */*
        Expect: 100-continue
        


    **Example Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Content-Type: text/plain
        

.. http:delete:: /plot/(plot_id)/traces/(trace_id)
    
    Remove a trace from the plot. The plot_id and 
    trace_id should exist.

    **Example Request**:

    .. sourcecode:: http

        DELETE /plots/4ykBEKmX/traces/4ykBEKmX HTTP/1.1
        Host: plotur.com
        Accept: */*
        Expect: 100-continue
        


    **Example Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Content-Type: text/plain
        
