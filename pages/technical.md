# Technical Overview

Please note that this page is **not required reading to know how to use CBNR** -- it is "just for fun", for developers who want to know what's running under the hood!

The back-end of Cloudy But No Rain is comprised of **one platform** supporting **four services**.

### The Platform

CBNR is currently run entirely on one server, located in Germany and rented from [Hetzner](foo). It does not use any cloud services, like load balancers or serverless functions.

On that server, there's only one custom service running under `systemd`, which is [k3s](foo). This is a single-binary distribution of Kubernetes which is robust but quick to set up on individual machines.

All the rest of CBNR is run on this Kubernetes distribution and managed via [Helm](foo) charts.

There are two "platform-level" services, which foo.

* [Caddy](foo), which operates as the load balancer and reverse proxy. It procures certificates from [Let's Encrypt](foo) and terminates SSL so the downstream services don't need to worry about it. All traffic, L4 and L7, flows through Caddy, and it's the only service exposed to the Internet.
* [Prometheus](foo), which is our telemetry hub. Each pod exposes data on a `/metrics` endpoint, and this service scrapes those endpoints every few seconds, aggregates, stores, and graphs that data.

The other services are custom CBNR code, written in Golang, and they can be found [here](foo).

### Service 1: `api`

### Service 2: `git`

### Service 3: `intake`

### Service 4: `query`
