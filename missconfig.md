# Misconfigurations

## Trivy 

`trivy conf .`

<details>
<summary>Show Results</summary>

```
k8s-manifest/ds.yaml (kubernetes)

Tests: 34 (SUCCESSES: 23, FAILURES: 11, EXCEPTIONS: 0)
Failures: 11 (UNKNOWN: 0, LOW: 7, MEDIUM: 4, HIGH: 0, CRITICAL: 0)

```

</details>

## Kubeaudit

`kubeaudit all -f k8s-manifest/deploy-insecureDefault.yaml  `

<details>
<summary>Show Results</summary>

```

---------------- Results for ---------------

  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: nginx-deployment

--------------------------------------------

-- [error] AppArmorAnnotationMissing
   Message: AppArmor annotation missing. The annotation 'container.apparmor.security.beta.kubernetes.io/nginx' should be added.
   Metadata:
      Container: nginx
      MissingAnnotation: container.apparmor.security.beta.kubernetes.io/nginx

-- [error] AutomountServiceAccountTokenTrueAndDefaultSA
   Message: Default service account with token mounted. automountServiceAccountToken should be set to 'false' on either the ServiceAccount or on the PodSpec or a non-default service account should be used.

-- [error] CapabilityOrSecurityContextMissing
   Message: Security Context not set. The Security Context should be specified and all Capabilities should be dropped by setting the Drop list to ALL.
   Metadata:
      Container: nginx

-- [warning] LimitsCPUNotSet
   Message: Resource CPU limit not set.
   Metadata:
      Container: nginx

-- [error] RunAsNonRootPSCNilCSCNil
   Message: runAsNonRoot should be set to true or runAsUser should be set to a value > 0 either in the container SecurityContext or PodSecurityContext.
   Metadata:
      Container: nginx

-- [error] AllowPrivilegeEscalationNil
   Message: allowPrivilegeEscalation not set which allows privilege escalation. It should be set to 'false'.
   Metadata:
      Container: nginx

-- [warning] PrivilegedNil
   Message: privileged is not set in container SecurityContext. Privileged defaults to 'false' but it should be explicitly set to 'false'.
   Metadata:
      Container: nginx

-- [error] ReadOnlyRootFilesystemNil
   Message: readOnlyRootFilesystem is not set in container SecurityContext. It should be set to 'true'.
   Metadata:
      Container: nginx

-- [error] SeccompAnnotationMissing
   Message: Seccomp annotation is missing. The annotation seccomp.security.alpha.kubernetes.io/pod: runtime/default should be added.
   Metadata:
      MissingAnnotation: seccomp.security.alpha.kubernetes.io/pod

```

</details>

## Checkov

`checkov -f k8s-manifest/deploy-secure.yaml`

<details>
<summary>Show Results</summary>

```

kubernetes scan results:

Passed checks: 83, Failed checks: 6, Skipped checks: 0

Check: CKV_K8S_37: "Minimize the admission of containers with capabilities assigned"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_34
Check: CKV_K8S_80: "Ensure that the admission control plugin AlwaysPullImages is set"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-admission-control-plugin-alwayspullimages-is-set
Check: CKV_K8S_113: "Ensure that the --bind-address argument is set to 127.0.0.1"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-bind-address-argument-is-set-to-127001
Check: CKV_K8S_34: "Ensure that Tiller (Helm v2) is not deployed"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_32
Check: CKV_K8S_33: "Ensure the Kubernetes dashboard is not deployed"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_31
Check: CKV_K8S_104: "Ensure that encryption providers are appropriately configured"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-etcd-cafile-argument-is-set-as-appropriate
Check: CKV_K8S_12: "Memory requests should be set"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_11
Check: CKV_K8S_77: "Ensure that the --authorization-mode argument includes RBAC"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-authorization-mode-argument-includes-rbac
Check: CKV_K8S_82: "Ensure that the admission control plugin ServiceAccount is set"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-admission-control-plugin-serviceaccount-is-set
Check: CKV_K8S_74: "Ensure that the --authorization-mode argument is not set to AlwaysAllow"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-authorization-mode-argument-is-not-set-to-alwaysallow-1
Check: CKV_K8S_20: "Containers should not run with allowPrivilegeEscalation"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_19
Check: CKV_K8S_26: "Do not specify hostPort unless absolutely necessary"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_25
Check: CKV_K8S_97: "Ensure that the --service-account-key-file argument is set as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-service-account-key-file-argument-is-set-as-appropriate
Check: CKV_K8S_114: "Ensure that the --profiling argument is set to false"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-profiling-argument-is-set-to-false-1
Check: CKV_K8S_108: "Ensure that the --use-service-account-credentials argument is set to true"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-use-service-account-credentials-argument-is-set-to-true
Check: CKV_K8S_146: "Ensure that the --hostname-override argument is not set"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-hostname-override-argument-is-not-set
Check: CKV_K8S_112: "Ensure that the RotateKubeletServerCertificate argument is set to true"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-rotatekubeletservercertificate-argument-is-set-to-true-for-controller-manager
Check: CKV_K8S_15: "Image Pull Policy should be Always"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_14
Check: CKV_K8S_148: "Ensure that the --tls-cert-file and --tls-private-key-file arguments are set as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-tls-cert-file-and-tls-private-key-file-arguments-are-set-as-appropriate-for-kubelet
Check: CKV_K8S_27: "Do not expose the docker daemon socket to containers"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_26
Check: CKV_K8S_89: "Ensure that the --secure-port argument is not set to 0"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-secure-port-argument-is-not-set-to-0
Check: CKV_K8S_13: "Memory limits should be set"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_12
Check: CKV_K8S_70: "Ensure that the --token-auth-file argument is not set"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-token-auth-file-parameter-is-not-set
Check: CKV_K8S_68: "Ensure that the --anonymous-auth argument is set to false"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-anonymous-auth-argument-is-set-to-false-1
Check: CKV_K8S_151: "Ensure that the Kubelet only makes use of Strong Cryptographic Ciphers"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-kubelet-only-makes-use-of-strong-cryptographic-ciphers
Check: CKV_K8S_141: "Ensure that the --read-only-port argument is set to 0"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-read-only-port-argument-is-set-to-0
Check: CKV_K8S_119: "Ensure that the --peer-cert-file and --peer-key-file arguments are set as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-peer-cert-file-and-peer-key-file-arguments-are-set-as-appropriate
Check: CKV_K8S_106: "Ensure that the --terminated-pod-gc-threshold argument is set as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-terminated-pod-gc-threshold-argument-is-set-as-appropriate
Check: CKV_K8S_143: "Ensure that the --streaming-connection-idle-timeout argument is not set to 0"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-streaming-connection-idle-timeout-argument-is-not-set-to-0
Check: CKV_K8S_40: "Containers should run as a high UID to avoid host conflict"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_37
Check: CKV_K8S_10: "CPU requests should be set"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_9
Check: CKV_K8S_79: "Ensure that the admission control plugin AlwaysAdmit is not set"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-admission-control-plugin-alwaysadmit-is-not-set
Check: CKV_K8S_39: "Do not use the CAP_SYS_ADMIN linux capability"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_36
Check: CKV_K8S_115: "Ensure that the --bind-address argument is set to 127.0.0.1"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-bind-address-argument-is-set-to-127001-1
Check: CKV_K8S_16: "Container should not be privileged"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_15
Check: CKV_K8S_45: "Ensure the Tiller Deployment (Helm V2) is not accessible from within the cluster"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_40
Check: CKV_K8S_88: "Ensure that the --insecure-port argument is set to 0"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-insecure-port-argument-is-set-to-0
Check: CKV_K8S_111: "Ensure that the --root-ca-file argument is set as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-root-ca-file-argument-is-set-as-appropriate
Check: CKV_K8S_19: "Containers should not share the host network namespace"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_18
Check: CKV_K8S_84: "Ensure that the admission control plugin PodSecurityPolicy is set"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-admission-control-plugin-podsecuritypolicy-is-set
Check: CKV_K8S_116: "Ensure that the --cert-file and --key-file arguments are set as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-cert-file-and-key-file-arguments-are-set-as-appropriate
Check: CKV_K8S_91: "Ensure that the --audit-log-path argument is set"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-audit-log-path-argument-is-set
Check: CKV_K8S_22: "Use read-only filesystem for containers where possible"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_21
Check: CKV_K8S_95: "Ensure that the --request-timeout argument is set as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-request-timeout-argument-is-set-as-appropriate
Check: CKV_K8S_93: "Ensure that the --audit-log-maxbackup argument is set to 10 or as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-audit-log-maxbackup-argument-is-set-to-10-or-as-appropriate
Check: CKV_K8S_145: "Ensure that the --make-iptables-util-chains argument is set to true"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-make-iptables-util-chains-argument-is-set-to-true
Check: CKV_K8S_110: "Ensure that the --service-account-private-key-file argument is set as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-service-account-private-key-file-argument-is-set-as-appropriate
Check: CKV_K8S_105: "Ensure that the API Server only makes use of Strong Cryptographic Ciphers"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-api-server-only-makes-use-of-strong-cryptographic-ciphers
Check: CKV_K8S_144: "Ensure that the --protect-kernel-defaults argument is set to true"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-protect-kernel-defaults-argument-is-set-to-true
Check: CKV_K8S_69: "Ensure that the --basic-auth-file argument is not set"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-basic-auth-file-argument-is-not-set
Check: CKV_K8S_100: "Ensure that the --tls-cert-file and --tls-private-key-file arguments are set as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-tls-cert-file-and-tls-private-key-file-arguments-are-set-as-appropriate
Check: CKV_K8S_72: "Ensure that the --kubelet-client-certificate and --kubelet-client-key arguments are set as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-kubelet-client-certificate-and-kubelet-client-key-arguments-are-set-as-appropriate
Check: CKV_K8S_35: "Prefer using secrets as files over secrets as environment variables"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_33
Check: CKV_K8S_75: "Ensure that the --authorization-mode argument includes Node"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-authorization-mode-argument-includes-node
Check: CKV_K8S_17: "Containers should not share the host process ID namespace"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_16
Check: CKV_K8S_18: "Containers should not share the host IPC namespace"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_17
Check: CKV_K8S_138: "Ensure that the --anonymous-auth argument is set to false"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-anonymous-auth-argument-is-set-to-false
Check: CKV_K8S_28: "Minimize the admission of containers with the NET_RAW capability"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_27
Check: CKV_K8S_117: "Ensure that the --client-cert-auth argument is set to true"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-client-cert-auth-argument-is-set-to-true
Check: CKV_K8S_81: "Ensure that the admission control plugin SecurityContextDeny is set if PodSecurityPolicy is not used"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-admission-control-plugin-securitycontextdeny-is-set-if-podsecuritypolicy-is-not-used
Check: CKV_K8S_102: "Ensure that the --etcd-cafile argument is set as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-etcd-cafile-argument-is-set-as-appropriate-1
Check: CKV_K8S_73: "Ensure that the --kubelet-certificate-authority argument is set as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-kubelet-certificate-authority-argument-is-set-as-appropriate
Check: CKV_K8S_86: "Ensure that the --insecure-bind-address argument is not set"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-insecure-bind-address-argument-is-not-set
Check: CKV_K8S_85: "Ensure that the admission control plugin NodeRestriction is set"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-admission-control-plugin-noderestriction-is-set
Check: CKV_K8S_99: "Ensure that the --etcd-certfile and --etcd-keyfile arguments are set as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-etcd-certfile-and-etcd-keyfile-arguments-are-set-as-appropriate
Check: CKV_K8S_29: "Apply security context to your pods and containers"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_28
Check: CKV_K8S_30: "Apply security context to your pods and containers"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_28
Check: CKV_K8S_90: "Ensure that the --profiling argument is set to false"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-profiling-argument-is-set-to-false-2
Check: CKV_K8S_92: "Ensure that the --audit-log-maxage argument is set to 30 or as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-audit-log-maxage-argument-is-set-to-30-or-as-appropriate
Check: CKV_K8S_71: "Ensure that the --kubelet-https argument is set to true"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-kubelet-https-argument-is-set-to-true
Check: CKV_K8S_147: "Ensure that the --event-qps argument is set to 0 or a level which ensures appropriate event capture"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-event-qps-argument-is-set-to-0-or-a-level-which-ensures-appropriate-event-capture
Check: CKV_K8S_14: "Image Tag should be fixed - not latest or blank"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_13
Check: CKV_K8S_94: "Ensure that the --audit-log-maxsize argument is set to 100 or as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-audit-log-maxsize-argument-is-set-to-100-or-as-appropriate
Check: CKV_K8S_107: "Ensure that the --profiling argument is set to false"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-profiling-argument-is-set-to-false
Check: CKV_K8S_38: "Ensure that Service Account Tokens are only mounted where necessary"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_35
Check: CKV_K8S_23: "Minimize the admission of root containers"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_22
Check: CKV_K8S_139: "Ensure that the --authorization-mode argument is not set to AlwaysAllow"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-authorization-mode-argument-is-not-set-to-alwaysallow
Check: CKV_K8S_11: "CPU limits should be set"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_10
Check: CKV_K8S_149: "Ensure that the --rotate-certificates argument is not set to false"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-rotate-certificates-argument-is-not-set-to-false
Check: CKV_K8S_118: "Ensure that the --auto-tls argument is not set to true"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-auto-tls-argument-is-not-set-to-true
Check: CKV_K8S_140: "Ensure that the --client-ca-file argument is set as appropriate"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-client-ca-file-argument-is-set-as-appropriate-scored
Check: CKV_K8S_83: "Ensure that the admission control plugin NamespaceLifecycle is set"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-admission-control-plugin-namespacelifecycle-is-set
Check: CKV_K8S_96: "Ensure that the --service-account-lookup argument is set to true"
        PASSED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/ensure-that-the-service-account-lookup-argument-is-set-to-true
Check: CKV_K8S_31: "Ensure that the seccomp profile is set to docker/default or runtime/default"
        FAILED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_29

                Code lines for this resource are too many. Please use IDE of your choice to review the file.
Check: CKV_K8S_8: "Liveness Probe Should be Configured"
        FAILED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_7

                Code lines for this resource are too many. Please use IDE of your choice to review the file.
Check: CKV_K8S_9: "Readiness Probe Should be Configured"
        FAILED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_8

                Code lines for this resource are too many. Please use IDE of your choice to review the file.
Check: CKV_K8S_25: "Minimize the admission of containers with added capability"
        FAILED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_24

                Code lines for this resource are too many. Please use IDE of your choice to review the file.
Check: CKV_K8S_21: "The default namespace should not be used"
        FAILED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_20

                Code lines for this resource are too many. Please use IDE of your choice to review the file.
Check: CKV_K8S_43: "Image should use digest"
        FAILED for resource: Deployment.default.nginx-deployment
        File: /k8s-manifest/deploy-secure.yaml:1-53
        Guide: https://docs.bridgecrew.io/docs/bc_k8s_39

                Code lines for this resource are too many. Please use IDE of your choice to review the file.
```

</details>

## kube-score

```
kube-score score  k8s-manifest/deploy-secure.yaml 
apps/v1/Deployment nginx-deployment                                           💥
    [CRITICAL] Pod NetworkPolicy
        · The pod does not have a matching NetworkPolicy
            Create a NetworkPolicy that targets this pod to control who/what can communicate with this pod. Note, this feature needs to be
            supported by the CNI implementation used in the Kubernetes cluster to have an effect.
    [CRITICAL] Container Ephemeral Storage Request and Limit
        · nginx -> Ephemeral Storage limit is not set
            Resource limits are recommended to avoid resource DDOS. Set resources.limits.ephemeral-storage

demo-k8s-security ➜ kube-score score  k8s-manifest/deploy.yaml       
apps/v1/Deployment nginx-deployment                                           💥
    [CRITICAL] Container Resources
        · nginx -> CPU limit is not set
            Resource limits are recommended to avoid resource DDOS. Set resources.limits.cpu
    [CRITICAL] Container Ephemeral Storage Request and Limit
        · nginx -> Ephemeral Storage limit is not set
            Resource limits are recommended to avoid resource DDOS. Set resources.limits.ephemeral-storage
    [CRITICAL] Container Security Context ReadOnlyRootFilesystem
        · nginx -> Container has no configured security context
            Set securityContext to run the container in a more secure context.
    [CRITICAL] Container Image Tag
        · nginx -> Image with latest tag
            Using a fixed tag is recommended to avoid accidental upgrades
    [CRITICAL] Pod NetworkPolicy
        · The pod does not have a matching NetworkPolicy
            Create a NetworkPolicy that targets this pod to control who/what can communicate with this pod. Note, this feature needs to be
            supported by the CNI implementation used in the Kubernetes cluster to have an effect.
    [CRITICAL] Container Security Context User Group ID
        · nginx -> Container has no configured security context
            Set securityContext to run the container in a more secure context.
```