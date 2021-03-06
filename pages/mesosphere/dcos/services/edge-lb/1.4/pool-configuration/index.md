---
layout: layout.pug
navigationTitle: Pool configuration
title: Pool configuration
menuWeight: 80
excerpt: Reference information for Edge-LB pool configuration settings
enterprise: true
---

This section provides reference information for all Edge-LB pool configuration settings and examples to demonstrate various use-cases.

# Configuration reference

The API reference, in swagger format, can be found by running the command below. It contains all possible options and a short description for each endpoint.

```
dcos edgelb show --reference
```

For more information, see the [CLI Reference Guide entry for `dcos edgelb show`](/mesosphere/dcos/services/edge-lb/1.4/cli-reference/dcos-edgelb-show/).

Choose an API version on the sidebar to view the appropriate configuration reference or examples.

# API versions

A new top-level pool configuration field named `apiVersion` was introduced in Edge-LB v1.0.0. The two models are almost identical, with one important difference: `pool.haproxy.backends.servers` (in apiVersion `V1`) has been replaced with `pool.haproxy.backends.services`, with a more intuitive way to select services/backends for HAProxy.

<p class="message--note"><strong>NOTE: </strong>Edge-LB 1.0 and later supports both the <tt>V1</tt> and <tt>V2</tt> API for backward compatibility. Therefore clients that were written against Edge-LB versions prior to Edge-LB 1.0 should work without any modifications with Edge-LB 1.0 and later. New setups should use API <tt>V2</tt> as at some point <tt>V1</tt> is going to be deprecated and then removed.</p>

<p class="message--note"><strong>NOTE: </strong> The <tt>apiVersion</tt> field in the pool definition defaults to <tt>V2</tt> if it was not provided. Hence, in order to use the <tt>V1</tt> config, you must explicitly set the <tt>pool.apiVersion</tt> to `"V1"`.</p>
