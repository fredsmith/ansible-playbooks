Ansible Configuration
------

The ansible roles and plays in this repo manage my systems and websites.  

  - The nginx_proxy role and play automatically configures, requests and installs [Lets Encrypt](https://letsencrypt.org) certificates for any sites set to ssl: true
  - Sites are configured as local static/php sites, or as proxies to backend services running on docker, based on the presence of a backend or repo setting
  - Site aliases are included in both the nginx configuration and the Lets Encrypt Certificate

**Important Note**: Lets Encrypt applies a rate limit of approximately 10 certificates per domain per week.  This means that if you have a lot of subdomains or aliases of a single top level domain, you need to space out turning SSL on on your sites.   This configuration repo currently does not refresh certificates from lets encrypt automatically, and they expire every 60 days.  I intend to add automatic monitoring and renewal later.

System Architecture:


                --------------
                |  Linode    |
                --------------
                     |
                     |  (OpenVPN)
                     |
                --------------     
                |  EdgeMax   |
                |  Router    |
                --------------
                     |
        -------------------------------
       |             |                |
    ----------   ----------    ------------
    | Docker |   |   NFS  |    | Internal |
    | Cluster|   | Server |    | Services |
    ---------    ---------     -----------


