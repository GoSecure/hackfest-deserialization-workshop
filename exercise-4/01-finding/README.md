# Exercise 3 - Finding gadgets


0. Register an account on LGTM

https://lgtm.com/

1. Setup the code base:

Add the following GitHub project:
https://github.com/GoSecure/goinsecure-deserialization

2. Got to the Query Console:
https://lgtm.com/query

3. Build & Execute a query:

```js
import java
import semmle.code.java.dataflow.DataFlow
import semmle.code.java.dataflow.TaintTracking


///Sink
predicate isReflectionSink(DataFlow::Node sink) {
  exists(MethodAccess ma | ma.getMethod().hasName("invoke") |
    ma.getMethod().getDeclaringType().hasQualifiedName("java.lang.reflect","Method") and //"java.lang","Class" //"java.lang.reflect","Method"
    sink.asExpr() = ma.getArgument(1)
  )
}

//Source
predicate isInsideReadObject(DataFlow::Node source) {
  source.asExpr().getEnclosingCallable().getDeclaringType().getASupertype*().hasQualifiedName("java.io", "Serializable") and
    source.asExpr().getEnclosingCallable().hasName("readObject")
}

class GadgetTaintTrackingCfg extends DataFlow::Configuration {
  GadgetTaintTrackingCfg() {
    this = "mapping"
  }

  override predicate isSource(DataFlow::Node source) {
    isInsideReadObject(source)
  }

  override predicate isSink(DataFlow::Node sink) {
    isReflectionSink(sink)
  }

  override predicate isAdditionalFlowStep(DataFlow::Node node1, DataFlow::Node node2) {
    TaintTracking::localTaintStep(node1, node2) or
    exists(Field f, RefType t | node1.asExpr() = f.getAnAssignedValue() and node2.asExpr() = f.getAnAccess() and
      node1.asExpr().getEnclosingCallable().getDeclaringType() = t and
      node2.asExpr().getEnclosingCallable().getDeclaringType() = t
    )
  }
}

from GadgetTaintTrackingCfg cfg, DataFlow::Node source, DataFlow::Node sink
where cfg.hasFlow(source, sink) 
select source, sink,source.getEnclosingCallable()
```