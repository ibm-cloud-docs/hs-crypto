## Testing reuse pages

Enable encryption for workloads in a namespace to achieve mutual TLS (mTLS) inside the cluster. Traffic that is routed by Envoy among pods in the cluster is encrypted with TLS. The certificate management for mTLS is handled by Istio. For more information, see the [Istio mTLS documentation](https://istio.io/latest/docs/tasks/security/authentication/authn-policy){: external}.
{: shortdesc}

Create an authentication policy file that is named `default.yaml`. This policy is namespace-scoped and configures workloads in the service mesh to accept only encrypted requests with TLS. Note that no `targets` specifications are included because the policy applies to all services in the mesh in this namespace.

Here is another example of coding the links for [an existing topic](/docs/hs-crypto?topic=hs-crypto-regions#available-regions).