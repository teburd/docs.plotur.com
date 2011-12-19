Plotur REST Reference - Trace(s)
================================

A trace is a multiple level of detail storage for column oriented numerical
data.

What that really means is that you can store monsterous data sets and then
obtain only levels of detail from it. This eliminates the need to plot every
row/point in the set when attempting to visualize the entire set.

Take for example a temperature reading every second for a decade in downtown
Chicago.

That set would likely contain 2 columns time and temperature. This set likely
has 315360000 or so rows. So plotur chooses the generalized solution for
the Level of Detail problem and uses DSP FIR filters and decimators to build
levels of detail. You may set certain columns to be filtered or not when you
create a trace.

Columns are stored as compressed chunks of IEEE double values. The key of the
chunk is the SHA2 hash of the uncompressed chunk. Chunks can be reused!

This means that should you have numerous columns of data that all key in
on the same timestamp data the timestamp data is only stored once.

If you happen to be very lucky and all your numbers are 0 your data takes almost
0 space.

Columns then provide a ordered list of chunks that represent the actual data.

This works well for columns in to the 10's of billions of values.

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
        Content-Type: application/json

        {name: 'Chicago Temperature',
         columns: [{name: 'Timestamp', units: 'seconds'},
                   {name: 'Temperature', units: 'celsius', filter: true}]
        }


    **Example Response**:

    .. sourcecode:: http

        HTTP/1.1 303 See Other
        Location: http://plotur.com/traces/4ykBEKmX
        Content-Type: text/plain
        

.. http:get:: /traces/(trace_id)
    
    Get information about a  trace.

    **Example Request**:

    .. sourcecode:: http

        GET /traces/4ykBEKmX HTTP/1.1
        Host: plotur.com
        Accept: application/json

    **Example Response**:

    .. sourcecode:: http

        HTTP/1.1 303 See Other
        Location: http://plotur.com/traces/4ykBEKmX
        Content-Type: application/json
        
        {name: 'Chicago Temperature',
         columns: [{name: 'Time',
                    units: 'seconds',
                    filter: false,
                    min: 0.0,
                    max: 1000000000.0
                    },
                   {name: 'Temperature',
                    units: 'celsius',
                    filter: true
                    min: -5.0,
                    max: 34.0}],
         levels: 0,
         rows: 0
        }


.. http:put:: /traces/(trace_id)/data
    
    Append column data from a csv file.

    **Example Request**:

    .. sourcecode:: http

        PUT /traces/4ykBEKmX/columns?append=0,1 HTTP/1.1
        Host: plotur.com
        Accept: */*
        Content-Length: 52000
        Content-Type: text/csv
        Expect: 100-continue

    **Example Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Content-Type: text/plain
        

