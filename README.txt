# jpegleg-registry

Create a private docker registry behind haproxy, built for CentOS 7.

It uses httpd and lets encrypt to get a free trusted certificate.

The httpd instance can be used to serve up a website or wikion 443 and/or 80 etc, while haproxy runs on a custom port and is required to access the registry.

ACLs in haproxy are used to restrict access to the registry based on IP, DNS, or IP ranges.

This is an ephemeral type registry. The intent is to have the actual repo elsewhere or files on disk, then load them into the registry to serve up the product images to the clusters. If a registry goes down, it shouldn't matter as long as your CI system is the source of the actual repo etc.

developers --------> github/CI ------> jpegleg-registry server <----------------- ( cloud instance, IoT, appliance, deployment )
    |                                     |
dockerhub --------------------------------|
