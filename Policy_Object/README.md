
# Policy 

1. [**PodDisruptionBudget:**](pod_distruption_budget.md)

   A **PodDisruptionBudget** defines the maximum number of concurrently disrupted pods during voluntary disruptions like node maintenance or updates. It ensures that a certain number of pods remain available and running, preventing excessive downtime and maintaining application availability during cluster changes.

2. [**Pod Security:**](pod_security.md)

   Ensuring **Pod Security** involves using various mechanisms such as PodSecurityPolicies (deprecated in favor of PodSecurity admission controllers) and admission controllers to enforce security rules on pods. This includes setting restrictions on host namespaces, capabilities, privilege escalation, and more. The goal is to enhance the security posture of pods to prevent vulnerabilities and unauthorized actions.

These policy-related objects help you enforce rules and standards to maintain security, availability, and compliance within your Kubernetes environment. By using NetworkPolicies, PodDisruptionBudgets, and security mechanisms, you can manage communication, application availability, and the security posture of your pods effectively.