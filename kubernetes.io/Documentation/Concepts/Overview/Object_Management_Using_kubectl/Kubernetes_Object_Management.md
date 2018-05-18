# Management Techniques
* A Kubernetes object should be managed using only one technique. Mixing and matching techniques for the same object results in undefined behavior.
Management technique|Operates on|Recommended environment|Supported writers|Learning curve
--------------------|-----------|-----------------------|-----------------|--------------
Imperative commands|Live objects|Development projects|1+|Lowest
Imperative object configuration|Individual files|Production projects|1|Moderate
Declarative object configuration|Directories of files|Production projects|1+|Highest
# References
* https://kubernetes.io/docs/concepts/overview/object-management-kubectl/overview/
