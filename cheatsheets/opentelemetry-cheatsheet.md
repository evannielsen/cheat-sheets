---
layout: default
title: OpenTelemetry Cheat Sheet
---

<div class="coversheet">
  <h1><span class="icon">&#x1F4C8;</span> OpenTelemetry Cheat Sheet</h1>
  <p>A comprehensive guide to understanding and using OpenTelemetry for observability</p>
</div>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F4D6;</span> <span class="accent-blue">Prerequisites</span></h3>
    <ul>
      <li>Basic understanding of distributed systems and observability</li>
      <li>Node.js or other supported language (Go, Python, Java, etc.)</li>
      <li>Understanding of metrics, traces, and logs</li>
      <li>Access to a monitoring backend (Jaeger, Prometheus, Grafana, etc.)</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4CA;</span> <span class="accent-green">Installation Steps</span></h3>
    <ol>
      <li>Install OpenTelemetry SDK for your language</li>
      <li>Configure the exporter to send data to your backend</li>
      <li>Instrument your application code</li>
      <li>Test and validate telemetry data</li>
    </ol>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F9E0;</span> <span class="accent-purple">Key Concepts</span></h3>
    <ul>
      <li>Traces - Track request flow across services</li>
      <li>Metrics - Quantitative measurements of system behavior</li>
      <li>Logs - Text-based event records</li>
      <li>Instrumentation - Code that generates telemetry data</li>
      <li>Exporters - Send data to monitoring backends</li>
    </ul>
  </div>
</div>

<h2 class="section-heading"><span class="icon">&#x1F4D8;</span> Getting Started</h2>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F527;</span> Step 1: Install OpenTelemetry SDK</h3>
    <p>For Node.js:</p>
    <pre><code>npm install @opentelemetry/sdk-trace-node
npm install @opentelemetry/exporter-trace-otlp-http
npm install @opentelemetry/instrumentation
npm install @opentelemetry/auto-instrumentations-node</code></pre>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F528;</span> Step 2: Initialize Tracer</h3>
    <p>Create a basic tracer configuration:</p>
    <pre><code>const { NodeTracerProvider } = require('@opentelemetry/sdk-trace-node');
const { OTLPTraceExporter } = require('@opentelemetry/exporter-trace-otlp-http');
const { ConsoleSpanExporter } = require('@opentelemetry/exporter-trace-console');

const provider = new NodeTracerProvider();
provider.addSpanProcessor(new BatchSpanProcessor(new OTLPTraceExporter({
  url: 'http://localhost:4318/v1/traces'
})));
provider.register();</code></pre>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4D1;</span> Step 3: Basic Instrumentation</h3>
    <p>Add tracing to your application:</p>
    <pre><code>const { trace } = require('@opentelemetry/api');

// Create a span
const span = trace.getSpan(context.active());
if (span) {
  span.setAttribute('key', 'value');
  span.addEvent('event-name');
}</code></pre>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4E6;</span> Step 4: Configure Exporters</h3>
    <p>Configure where your telemetry data goes:</p>
    <pre><code>// For Jaeger
const { JaegerExporter } = require('@opentelemetry/exporter-jaeger');

// For Prometheus
const { PrometheusExporter } = require('@opentelemetry/exporter-prometheus');</code></pre>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F504;</span> Step 5: Run with Auto-instrumentation</h3>
    <p>Use auto-instrumentation for quick setup:</p>
    <pre><code>node -r @opentelemetry/auto-instrumentations-node/register app.js</code></pre>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4A1;</span> Step 6: Validate Setup</h3>
    <p>Check that spans are being exported:</p>
    <pre><code>// Add console exporter for debugging
provider.addSpanProcessor(new BatchSpanProcessor(new ConsoleSpanExporter()));</code></pre>
  </div>
</div>

<div class="card-standalone">
  <h2 class="section-heading"><span class="icon">&#x26A1;</span> Quick Tips</h2>
  <div class="mini-grid">
    <div class="mini-item">Use semantic conventions for consistent attribute naming</div>
    <div class="mini-item">Set sampling rates to control data volume</div>
    <div class="mini-item">Instrument at the right level of granularity</div>
    <div class="mini-item">Monitor your exporter's performance impact</div>
  </div>
</div>

<div class="card-grid" style="margin-bottom: 1rem;">
  <div class="card-item">
    <div class="tip-box"><strong>Tip:</strong> Start with auto-instrumentation to quickly get telemetry data, then add manual instrumentation for specific needs.</div>
  </div>
  <div class="card-item">
    <div class="warning-box"><strong>Warning:</strong> Be careful with high cardinality attributes - they can significantly increase resource usage.</div>
  </div>
</div>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F4DC;</span> Core Components</h3>
    <ul>
      <li><strong>Tracer</strong> - Creates and manages spans</li>
      <li><strong>Span</strong> - Represents a unit of work in a trace</li>
      <li><strong>Exporter</strong> - Sends telemetry data to backend systems</li>
      <li><strong>Instrumentation</strong> - Code that generates telemetry data</li>
      <li><strong>SDK</strong> - The implementation of the OpenTelemetry specification</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4CA;</span> <span class="accent-green">Span Operations</span></h3>
    <ul>
      <li><strong>Start Span</strong> - Begin a new span</li>
      <li><strong>Add Attributes</strong> - Add key-value pairs to span</li>
      <li><strong>Add Events</strong> - Log events within the span</li>
      <li><strong>Set Status</strong> - Mark span as successful or failed</li>
      <li><strong>End Span</strong> - Complete the span and send it for export</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F9E0;</span> <span class="accent-purple">Telemetry Types</span></h3>
    <ul>
      <li><strong>Traces</strong> - Track request flow through distributed systems</li>
      <li><strong>Metrics</strong> - Quantitative measurements (counters, gauges, histograms)</li>
      <li><strong>Logs</strong> - Text-based event records with timestamps</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4E6;</span> <span class="accent-orange">Exporters</span></h3>
    <ul>
      <li><strong>OTLP</strong> - OpenTelemetry Protocol exporter</li>
      <li><strong>Jaeger</strong> - Jaeger backend exporter</li>
      <li><strong>Prometheus</strong> - Metrics collection and exposition</li>
      <li><strong>Zipkin</strong> - Zipkin backend exporter</li>
      <li><strong>Console</strong> - Debug output to console</li>
    </ul>
  </div>
</div>

<div class="card-standalone">
  <h2 class="section-heading"><span class="icon">&#x26A1;</span> Quick Reference</h2>
  <div class="mini-grid">
    <div class="mini-item">Use semantic conventions for consistent attribute naming</div>
    <div class="mini-item">Set sampling rates to control data volume</div>
    <div class="mini-item">Instrument at the right level of granularity</div>
    <div class="mini-item">Monitor your exporter's performance impact</div>
  </div>
</div>

<div class="card-grid" style="margin-bottom: 1rem;">
  <div class="card-item">
    <div class="note"><strong>Tip:</strong> Use environment variables for configuration to support different environments.</div>
  </div>
  <div class="card-item">
    <div class="note"><strong>Best Practice:</strong> Always end spans to ensure proper telemetry data collection.</div>
  </div>
  <div class="card-item">
    <div class="note"><strong>Structure:</strong> Follow the pattern: SDK initialization → Instrumentation → Exporter configuration</div>
  </div>
</div>

<h2 class="section-heading"><span class="icon">&#x1F4D8;</span> Core Concepts Explained</h2>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F4DC;</span> Traces</h3>
    <p>A trace is a tree of spans that represent the execution flow of a request through a distributed system. Each span represents a unit of work.</p>
    <ul>
      <li>Spans are linked by parent-child relationships</li>
      <li>Each trace has a root span and one or more child spans</li>
      <li>Traces help identify bottlenecks and performance issues</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F527;</span> Spans</h3>
    <p>A span is a named, timed operation representing work done in a trace:</p>
    <ul>
      <li>Have a start and end time</li>
      <li>Contain attributes (key-value pairs)</li>
      <li>Can contain events (named timestamps with attributes)</li>
      <li>Can have status information (success, error, etc.)</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F50D;</span> Attributes</h3>
    <p>Key-value pairs attached to spans for contextual information:</p>
    <ul>
      <li>Used to filter and search traces</li>
      <li>Should follow semantic conventions</li>
      <li>High cardinality attributes can impact performance</li>
      <li>Examples: HTTP method, response status code, user ID</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4C8;</span> Exporters</h3>
    <p>Components that send telemetry data to backend systems:</p>
    <ul>
      <li>Support various protocols (HTTP, gRPC, etc.)</li>
      <li>Can be configured for different backends</li>
      <li>May include batching and retry mechanisms</li>
      <li>Should be monitored for performance impact</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F501;</span> Instrumentation</h3>
    <p>Code that generates telemetry data:</p>
    <ul>
      <li>Can be auto-instrumented or manually instrumented</li>
      <li>Auto-instrumentation provides quick setup</li>
      <li>Manual instrumentation offers more control and specificity</li>
      <li>Instrumentation libraries exist for common frameworks</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4A5;</span> Best Practices</h3>
    <p>Follow these guidelines for effective OpenTelemetry usage:</p>
    <ul>
      <li>Start with auto-instrumentation for quick results</li>
      <li>Add manual instrumentation for specific business logic</li>
      <li>Use semantic conventions consistently</li>
      <li>Monitor and tune sampling rates</li>
      <li>Be mindful of cardinality in attributes</li>
      <li>Test your telemetry setup before production deployment</li>
    </ul>
  </div>
</div>

<h2 class="section-heading"><span class="icon">&#x1F4AC;</span> Common Patterns</h2>

<p style="font-size: .88rem; color: var(--muted); margin-bottom: 0.5rem;">Creating a span:</p>
<pre><code>const { trace } = require('@opentelemetry/api');

const span = trace.getTracer('my-tracer').startSpan('operation-name');
span.setAttribute('key', 'value');
span.end();</code></pre>

<p style="font-size: .88rem; color: var(--muted); margin-bottom: 0.5rem;">Using context propagation:</p>
<pre><code>const { context } = require('@opentelemetry/api');

// Propagate context
const span = trace.getTracer('my-tracer').startSpan('operation-name');
const ctx = trace.setSpan(context.active(), span);
context.with(ctx, () => {
  // Operations that should be part of this span
});
span.end();</code></pre>

<p style="font-size: .88rem; color: var(--muted); margin-bottom: 0.5rem;">Adding events to spans:</p>
<pre><code>const { trace } = require('@opentelemetry/api');

const span = trace.getTracer('my-tracer').startSpan('operation-name');
span.addEvent('event-name', { key: 'value' });
span.end();</code></pre>

<h2 class="section-heading"><span class="icon">&#x1F4C9;</span> Development Structure</h2>

<div style="background: #0d1117; padding: 1rem; border-radius: 6px; margin-bottom: 1rem;">
<pre><code>project/
├── package.json
├── app.js
├── instrumentation.js      # OpenTelemetry setup and configuration
├── traces/                 # Trace-related code
└── exporters/              # Exporter-specific configurations
</code></pre>
</div>

<h2 class="section-heading"><span class="icon">&#x1F4B0;</span> Common Use Cases</h2>

<div class="card-grid">
  <div class="card-item">
    <p><strong>Request Tracing</strong> - Track requests through microservices</p>
  </div>
  <div class="card-item">
    <p><strong>Performance Monitoring</strong> - Identify bottlenecks in applications</p>
  </div>
  <div class="card-item">
    <p><strong>Error Tracking</strong> - Correlate errors with request traces</p>
  </div>
  <div class="card-item">
    <p><strong>Business Metrics</strong> - Track business-relevant KPIs</p>
  </div>
</div>

<h2 class="section-heading"><span class="icon">&#x1F4B0;</span> Configuration Tips</h2>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F4DC;</span> Environment Variables</h3>
    <p>Use environment variables for configuration:</p>
    <ul>
      <li><code>OTEL_EXPORTER_OTLP_ENDPOINT</code></li>
      <li><code>OTEL_SERVICE_NAME</code></li>
      <li><code>OTEL_TRACES_SAMPLER</code></li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F50D;</span> Sampling Strategies</h3>
    <p>Control data volume with sampling:</p>
    <ul>
      <li><strong>AlwaysOn</strong> - Export all traces</li>
      <li><strong>Never</strong> - Export no traces</li>
      <li><strong>TraceIdRatioBased</strong> - Sample based on ratio</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4A5;</span> Performance Tuning</h3>
    <p>Optimize your telemetry setup:</p>
    <ul>
      <li>Batch spans for efficient export</li>
      <li>Use appropriate buffer sizes</li>
      <li>Monitor memory usage</li>
      <li>Configure retry mechanisms</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4C8;</span> Security Considerations</h3>
    <p>Ensure secure telemetry data handling:</p>
    <ul>
      <li>Use HTTPS for exporters</li>
      <li>Validate attribute values to prevent injection attacks</li>
      <li>Protect sensitive information in attributes</li>
      <li>Consider data retention policies</li>
    </ul>
  </div>
</div>

<h2 class="section-heading"><span class="icon">&#x1F4AC;</span> Common Commands</h2>

<div class="card-grid">
  <div class="card-item">
    <p><strong>Install OpenTelemetry:</strong></p>
    <pre><code>npm install @opentelemetry/sdk-trace-node</code></pre>
  </div>

  <div class="card-item">
    <p><strong>Run with auto-instrumentation:</strong></p>
    <pre><code>node -r @opentelemetry/auto-instrumentations-node/register app.js</code></pre>
  </div>

  <div class="card-item">
    <p><strong>Set environment variables:</strong></p>
    <pre><code>export OTEL_SERVICE_NAME=my-service
export OTEL_EXPORTER_OTLP_ENDPOINT=http://localhost:4318</code></pre>
  </div>

  <div class="card-item">
    <p><strong>View traces in Jaeger UI:</strong></p>
    <pre><code>http://localhost:16686</code></pre>
  </div>
</div>

<p class="credits">Made with <span style="color: var(--accent-pink);">&#x2764;</span> for observability engineers &mdash; keep tracing! &#x1F50D;</p>