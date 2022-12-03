# DBSCAN
For each instance how many instances are located within a small distance $\epsilon$ from it. Region is called $\epsilon$-neighborhood.
If an instance has at least min_samples instances in its vicinity its considered a core. All instances in said neighborhood belong to the same cluster and may include other core instances.
Non involved instances are anomalies.