---
title: Tracing Reference
content-type: reference
---

This reference describes the OpenTelemetry tracing capabilities of {{site.base_gateway}}.
{% if_version gte:3.7.x %}

{:.important}
> **Important**: OpenTelemetry tracing replaces the deprecated Granular Tracing feature.
Granular Tracing has been removed from {{site.base_gateway}} starting in 3.7.0.0,
and configurations like `tracing = on` are no longer available. Instead, use the
OpenTelemetry Tracing described on this page.
{% endif_version %}

## Core instrumentations

The following instrumentations can be used by any plugins built on top of Kong's tracing API, for example, 
the [OpenTelemetry plugin](/hub/kong-inc/opentelemetry/).

{% if_version gte:3.2.x %}
Kong provides a set of core instrumentations for tracing, these can be configured in the `tracing_instrumentations` configuration.
{% endif_version %}
{% if_version lte:3.1.x %}
Kong provides a set of core instrumentations for tracing, these can be configured in the `opentelemetry_tracing` configuration.
{% endif_version %}

- `off`: do not enable instrumentations.
- `request`: only enable request-level instrumentations.
- `all`: enable all the following instrumentations.
- `db_query`: trace database query.
- `dns_query`: trace DNS query.
- `router`: trace router execution, including router rebuilding.
- `http_client`: trace OpenResty HTTP client requests.
- `balancer`: trace balancer retries.
- `plugin_rewrite`: trace plugins iterator execution with rewrite phase.
- `plugin_access`: trace plugins iterator execution with access phase.
- `plugin_header_filter`: trace plugins iterator execution with `header_filter` phase.

## Propagation

The tracing API supports propagating the following headers:
- `w3c` - [W3C trace context](https://www.w3.org/TR/trace-context/)
- `b3`, `b3-single` - [Zipkin headers](https://github.com/openzipkin/b3-propagation)
- `jaeger` - [Jaeger headers](https://www.jaegertracing.io/docs/client-libraries/#propagation-format)
- `ot` - [OpenTracing headers](https://github.com/opentracing/specification/blob/master/rfc/trace_identifiers.md)

The tracing API detects the propagation format from the headers, and uses the appropriate format to propagate the span context.
If no appropriate format is found, it falls back to the default format, which can be user-specified.

The propagation API works for both the OpenTelemetry plugin and the Zipkin plugin.
