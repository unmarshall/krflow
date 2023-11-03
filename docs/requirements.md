# Requirements

* It should be possible to create a flow consisting of a combination of `sequential` and `concurrent` steps.

* It should be possible to compose flow(s) from other flow(s).

* For concurrent steps it should be possible to define the following behavior/spec:

  * Fail fast at first error OR execute all concurrent steps irrespective of errors
  * Propagate panic or convert it into error and record the error
  * Either wait on all concurrent steps to complete OR define `WaitOn` constraints at the steps level. The executor will then wait for the steps which have the constraint defined.

* It should be possible to record the progress of a flow.

* It should be possible to record and optionally publish metrics for each flow step.

* It should be possible to provide variants of steps/stages/flow:

  * Retriable step/stage/flow - on error the step or stage or flow should be retried. For each retry entity it should be possible to specify a retry-behavior:

    * Retry until a predicate is met
    * Retry until a timeout
    * Retry fixed number of times

    Any combination of the above can be specified as a retry behavior.

    Retry-Step: Only a single step is retriable.

    Retry-Stage: If there is an error in any step in a Stage (sub-flow) then the whole sub-flow/stage is retried.

    Retry-Flow: On error of any step/sub-flow the entire flow is retried.

  * Resumable Stage/Flow:  If a stage(sub-flow) or flow is marked as resumable and it is also marked as Retriable then on Error it will resume from the last erroneous step.

  * Conditional Step/Stage(Sub-Flow): It should be possible to execute a step or a sub-flow based on a predicate evaluation. If the predicate evaluation is true - then the step/sub-flow executes else it is skipped.

* It should be possible to choose a sub-flow based on predicate evaluate - a.k.a sub-flow branching.

* It should be possible to provide steps that always execute at the end of a step/sub-flow/flow. One way could be using `Finally` as a special step/callback.

* It should be possible to define `on failure` step for step/sub-flow/flow. One way could be using `Try`, `Catch` definitions

* It should be possible to visualize a flow at compile time and runtime.