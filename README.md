# How to reproduce

Change the `opentelemetry-javaagent` version in the file `build.sbt` to try another version.

Then run:

```shell
# Compile and create a runnable artifact
sbt compile stage

# Run it
OTEL_SERVICE_NAME="test" \
    OTEL_METRICS_EXPORTER=console \
    OTEL_LOGS_EXPORTER=none \
    OTEL_TRACES_EXPORTER=none \
    ./target/universal/stage/bin/play-scala-seed

# Navigate to http://localhost:9000/ once or twice
# Wait for the console to output metrics (several seconds)
```

## Results

### OTEL 2.21

```
[otel.javaagent 2025-11-30 17:47:20:045 +0100] [PeriodicMetricReader-1] INFO io.opentelemetry.exporter.logging.LoggingMetricExporter - Received a collection of 13 metrics for export.

[otel.javaagent 2025-11-30 17:47:20:046 +0100] [PeriodicMetricReader-1] INFO io.opentelemetry.exporter.logging.LoggingMetricExporter - metric: ImmutableMetricData{resource=Resource{schemaUrl=https://opentelemetry.io/schemas/1.24.0, attributes={host.arch="amd64", host.name="peyrouse-lx", os.description="Linux 6.17.7-200.fc42.x86_64", os.type="linux", process.command_line="/usr/lib/jvm/java-21-openjdk/bin/java -javaagent:/tmp/otel/play-scala-seed/target/universal/stage/bin/../opentelemetry-javaagent/opentelemetry-javaagent-2.21.0.jar -Duser.dir=/tmp/otel/play-scala-seed/target/universal/stage play.core.server.ProdServerStart", process.executable.path="/usr/lib/jvm/java-21-openjdk/bin/java", process.pid=146342, process.runtime.description="Red Hat, Inc. OpenJDK 64-Bit Server VM 21.0.9+10", process.runtime.name="OpenJDK Runtime Environment", process.runtime.version="21.0.9+10", service.instance.id="0d5b8def-ac5f-48f0-bf31-530b3a001385", service.name="test", telemetry.distro.name="opentelemetry-java-instrumentation", telemetry.distro.version="2.21.0", telemetry.sdk.language="java", telemetry.sdk.name="opentelemetry", telemetry.sdk.version="1.55.0"}}, instrumentationScopeInfo=InstrumentationScopeInfo{name=io.opentelemetry.pekko-http-1.0, version=2.21.0-alpha, schemaUrl=null, attributes={}}, name=http.server.request.duration, description=Duration of HTTP server requests., unit=s, type=HISTOGRAM, data=ImmutableHistogramData{aggregationTemporality=CUMULATIVE, points=[ImmutableHistogramPointData{getStartEpochNanos=1764521179999999022, getEpochNanos=1764521240024183103, getAttributes=FilteredAttributes{http.request.method=GET,http.response.status_code=200,http.route=/assets/$file<.+>,network.protocol.version=1.1,url.scheme=http}, getSum=0.164746774, getCount=2, hasMin=true, getMin=0.078248748, hasMax=true, getMax=0.086498026, getBoundaries=[0.005, 0.01, 0.025, 0.05, 0.075, 0.1, 0.25, 0.5, 0.75, 1.0, 2.5, 5.0, 7.5, 10.0], getCounts=[0, 0, 0, 0, 0, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0], getExemplars=[ImmutableDoubleExemplarData{filteredAttributes={server.address="localhost", server.port=9000, url.path="/assets/javascripts/main.js", user_agent.original="Mozilla/5.0 (X11; Linux x86_64; rv:144.0) Gecko/20100101 Firefox/144.0"}, epochNanos=1764521209809000000, spanContext=ImmutableSpanContext{traceId=b673275de4adabd99f02d8f5401185f4, spanId=38122f95508f13fa, traceFlags=01, traceState=ArrayBasedTraceState{entries=[]}, remote=false, valid=true}, value=0.078248748}]}, ImmutableHistogramPointData{getStartEpochNanos=1764521179999999022, getEpochNanos=1764521240024183103, getAttributes=FilteredAttributes{http.request.method=GET,http.response.status_code=200,http.route=/,network.protocol.version=1.1,url.scheme=http}, getSum=0.191801044, getCount=1, hasMin=true, getMin=0.191801044, hasMax=true, getMax=0.191801044, getBoundaries=[0.005, 0.01, 0.025, 0.05, 0.075, 0.1, 0.25, 0.5, 0.75, 1.0, 2.5, 5.0, 7.5, 10.0], getCounts=[0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0], getExemplars=[ImmutableDoubleExemplarData{filteredAttributes={server.address="localhost", server.port=9000, url.path="/", user_agent.original="Mozilla/5.0 (X11; Linux x86_64; rv:144.0) Gecko/20100101 Firefox/144.0"}, epochNanos=1764521209646000000, spanContext=ImmutableSpanContext{traceId=324b19549fa1407ce8d0035895dfb37b, spanId=aafe8ab70cf32357, traceFlags=01, traceState=ArrayBasedTraceState{entries=[]}, remote=false, valid=true}, value=0.191801044}]}]}}
```

### OTEL 2.22

No Pekko HTTP instrumentation.

```
[otel.javaagent 2025-11-30 17:50:00:333 +0100] [PeriodicMetricReader-1] INFO io.opentelemetry.exporter.logging.LoggingMetricExporter - Received a collection of 12 metrics for export.
```
