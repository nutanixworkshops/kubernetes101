.. _day5:

.. title:: Introduction to Kubernetes

Day 5 - Conclusion
============================================

Conclusion
----------

Now that John is at the end of his project he grabs his tabel from day 1 and adds a column, called result

.. list-table::
   :widths: 30 30 40 
   :header-rows: 1

   * - Task
     - k8s
     - Result
   * - Can use Docker containers                         
     - Yes
     - Yes part of the YAML file.
   * - Config changes outside of container
     - Yes, using configMaps
     - Not entirely via configMaps, but using external storage easy to do.
   * - Rebooting container should not impact service
     - Yes
     - Yes, if you have more than two replicas running in your deployment.
   * - Reboot host (master or worker) no impact on service
     - Yes, just make sure the cluster is big enough wrt “surviving nodes”
     - If rebooting the Master in a single master cluster than the services keep running, but the cluster cannot be controlled anymore
   * - Update config and/or image: Roll back
     - Not sure, need to investigate
     - Yes, all services, if more then one replica, will be updated one after the other and have a rollback possibility
   * - Update config and/or image: no impact on service
     - Not sure, need to investigate
     - Yes, all services, if more then one replica, will be updated one after the other and have a rollback possibility. Small changes on YAML files can be updated on the fly.
   * - Scaling possibilities (out/in)
     - Yes, automatic on failure of pod.
     - Yes, by adding a higher replicas number than 1 in the YAML file and redeploying the YAML file. If the number of pods lower then the number in the replicas parameter, k8s will start another pod. k8s seems to be able to run a automatic way of scaling out/in (HPA) and up/down (VPA) (https://www.replex.io/blog/kubernetes-in-production-best-practices-for-cluster-autoscaler-hpa-and-vpa). For a description of HPA John found this article: https://www.magalix.com/blog/kubernetes-automatic-scaling
   * - Public cloud supported
     - Yes, natively and via VMs
     - Yes. Not tested, but all looked at (AWS, Azure and GCP, have native K8s services)
