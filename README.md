### Argo rollouts demo

This Repository contains examples of argo rollouts with various deployment strategies, which can be used for testing and development purpose.




## Canary Deployment Strategy 
A canary rollout is a deployment strategy where the operator releases a new version of their application to a small percentage of the production traffic.

To create canary rollout, clone this repository and run the following commands

```bash
oc apply -f analysis-templates
oc apply -f canary
```



## BlueGreen Deployment Strategy

A Blue Green Deployment allows users to reduce the amount of time multiple versions running at the same time.



To create blue-green rollout, clone this repository and run the following commands

```bash
oc apply -f analysis-templates
oc apply -f blue-green
```
