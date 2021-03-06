What is this?
=============

This is a simple python API for the Aussie Broadband customer portal. There's
a lot more that can be done with the portal than what I have implemented here,
but this was enough to get me what I wanted for now (graphing for usage in
prometheus and grafana).

Feel free to drop me a line at mikal@stillhq.com if you want to help expand
this.

Usage
=====

A usage example in example.py, but here are the high points. First, install aussiebb from pypi:

```
$ pip install aussiebb
```

This code uses environment variables to get your username and password, so set those up:

```
$ export AUSSIE_USERNAME="fred"
$ export AUSSIE_PASSWORD="banana"
```

Now run the example:

```
$ python examples/example.py
```

You should get output like this (for an example service of course):

```
$ python3 example.py 
You have 0 tickets open
You have 2 orders

+------+--------+---------------+--------------------+-------------+-----------------+--------------------+
| Type |   ID   | Download (MB) |     Remaining      | Upload (MB) | Current Outages |      Bolt ons      |
+------+--------+---------------+--------------------+-------------+-----------------+--------------------+
| NBN  | 451493 |     450486    | Unlimited, 24 days |    22537    |        0        | Static IP ($10.00) |
+------+--------+---------------+--------------------+-------------+-----------------+--------------------+
```

Docker image for a prometheus exporter
======================================

There is also a Docker image of a prometheus exporter, which might be
useful. To build the image, do this:

```
docker build -t aussiebb .
docker tag aussiebb harbor.home.stillhq.com/stillhq/aussiebb
docker push harbor.home.stillhq.com/stillhq/aussiebb
```

Where harbor.home.stillhq.com is your image repository. You can then run
image like this:

```
docker run -e AUSSIE_USERNAME=foo -e AUSSIE_PASSWORD=bar \
    -p 8000:8000 aussiebb:latest
```

Installation from source
========================

You should run this in a venv. Do something like this:

```
$ python3 -m venv ~/virtualenvs/aussiebb
$ . ~/virtualenvs/aussiebb/bin/activate
$ pip install -U pip
$ pip install -U -r requirements.txt
$ pip install -e .
```