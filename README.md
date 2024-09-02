### Argo rollouts demo

This Repository contains examples of argo rollouts with various deployment strategies, which can be used for testing and development purpose.

## Canary Deployment Strategy

A canary rollout is a deployment strategy where the operator releases a new version of their application to a small percentage of the production traffic.

- To map Rollout to an Gitops application, Update the gitops application name in canary-rollout.yaml metadata

  - Update Rollout's `metadata.labels` [#reference](https://github.com/karthikjeeyar/argo-rollouts-demo/blob/main/canary/canary-rollout.yaml#L5C3-L7C44):

  ```
  metadata:
   labels:
       "backstage.io/kubernetes-id": <GITOPS_APPLICATION_NAME>
       app.kubernetes.io/instance: <GITOPS_APPLICATION_NAME>

  ```

  - update `spec.selector.matchLabels` and `spec.template.metadata` [#reference](https://github.com/karthikjeeyar/argo-rollouts-demo/blob/main/canary/canary-rollout.yaml#L11-L21)

```
spec:
  ....
  selector:
    matchLabels:
      app: canary-rollout-analysis
      "backstage.io/kubernetes-id": <GITOPS_APPLICATION_NAME>
      app.kubernetes.io/instance: <GITOPS_APPLICATION_NAME>
   ...
   template:
    metadata:
      labels:
        app: canary-rollout-analysis
        "backstage.io/kubernetes-id": <GITOPS_APPLICATION_NAME>
        app.kubernetes.io/instance: <GITOPS_APPLICATION_NAME>
```

- create analysis-templates and canary rollout.

```bash
oc apply -f analysis-templates
oc apply -f canary
```

## BlueGreen Deployment Strategy

A Blue Green Deployment allows users to reduce the amount of time multiple versions running at the same time.

- To map BlueGreen Rollout to an Gitops application, Update the gitops application name in [bluegreen-rollout.yaml](https://github.com/karthikjeeyar/argo-rollouts-demo/blob/main/blue-green/bluegreen-rollout.yaml) metadata

  - Update Rollout's `metadata.labels` [#reference](https://github.com/karthikjeeyar/argo-rollouts-demo/blob/main/blue-green/bluegreen-rollout.yaml#L6-L7):

  ```
  metadata:
   labels:
       "backstage.io/kubernetes-id": <GITOPS_APPLICATION_NAME>
       app.kubernetes.io/instance: <GITOPS_APPLICATION_NAME>

  ```

  - update `spec.selector.matchLabels` and `spec.template.metadata` [#reference](https://github.com/karthikjeeyar/argo-rollouts-demo/blob/main/blue-green/bluegreen-rollout.yaml#L11-L21)

```
spec:
  ....
  selector:
    matchLabels:
      app: rollout-bluegreen
      "backstage.io/kubernetes-id": <GITOPS_APPLICATION_NAME>
      app.kubernetes.io/instance: <GITOPS_APPLICATION_NAME>
   ...
   template:
    metadata:
      labels:
        app: rollout-bluegreen
        "backstage.io/kubernetes-id": <GITOPS_APPLICATION_NAME>
        app.kubernetes.io/instance: <GITOPS_APPLICATION_NAME>
```

- create analysis-templates and bluegreen rollout.

```bash
oc apply -f analysis-templates
oc apply -f blue-green
```
