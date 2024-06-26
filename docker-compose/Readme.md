# Docker Compose Example

This example will start a single Nexoedge cluster which consists of

| Component(s) | Service name(s) | Compose file |
|--------------|-----------------|--------------|
| A proxy                           | `proxy`                               | `nexoedge-proxy.yaml`    |
| Two agents                        | `storage-node-01`, `storage-node-02`  | `nexoedge-agents.yaml`   |
| A Samba server with Nexoedge VFS  | `cifs`                                | `nexoedge-cifs-cluster.yaml`  |
| A metadata store                  | `metastore`                           | `nexoedge-proxy.yaml`    |
| A statistics store                | `statsdb`                             | `nexoedge-proxy.yaml`    |
| A reporter for statistics collection   | `reporter`                       | `nexoedge-proxy.yaml`    |
| A portal frontend                 | `portal-frontend`                     | `nexoedge-proxy.yaml`    |
| A portal backend                  | `portal-backend`                      | `nexoedge-proxy.yaml`    |

The cluster setup is defined in the file `nexoedge-cluster.yml` with the service names listed in the above.

The variables for cluster setup is defined in the file `.env`.

Data Persistence

- `NEXOEDGE_DATA_DIR`: Parent directory for Docker bind mounts.

Nexoedge Configurations

- `NEXOEDGE_PROXY_IP`: IP or domain name of the proxy. It should be reachable by the agents.
- `NEXOEDGE_PROXY_PORT`: Port of the proxy that opens to connections from agents.
- `NEXOEDGE_STORAGE_NODE_1_IP`: IP or domain name of the first agent. It should be reachable by the proxy.
- `NEXOEDGE_STORAGE_NODE_2_IP`: IP or domain name of the second agent. It should be reachable by the proxy.
- `NEXOEDGE_STORAGE_POLICY_N`: Total number of chunks per erasure coded stripe.
- `NEXOEDGE_STORAGE_POLICY_K`: Number of data chunks per erasure coded stripe.
- `NEXOEDGE_STORAGE_POLICY_F`: Number of agents failures to tolerate per erasure coded stripe.
- `NEXOEDGE_STORAGE_POLICY_MAX_CHUNK_SIZE`: Maximum size of an erasure coded chunk.

Docker-related Settings

- `NEXOEDGE_NETWORK`: Name of the container network to connect the Nexoedge containers
- `TAG`: Tag of the images to use, e.g., release date or version.
- `NEXOEDGE_CIFS_IMAGE_NAME`: Name of the container image to use for Nexoedge CIFS
- `NEXOEDGE_PROXY_IMAGE_NAME`: Name of the container image to use for Nexoedge proxy
- `NEXOEDGE_AGENT_IMAGE_NAME`: Name of the container image to use for Nexoedge agent 
- `NEXOEDGE_REPORTER_IMAGE_NAME`: Name of the container image to use for Nexoedge reporter 
- `NEXOEDGE_PORTAL_FRONTEND_IMAGE_NAME`: Name of the container image to use for Nexoedge admin portal (web user interface)
- `NEXOEDGE_PORTAL_BACKEND_IMAGE_NAME`: Name of the container image to use for Nexoedge admin portal backend

The script `cmd.sh` is used to start and terminate the cluster. The available commands can be listed by running `./cmd.sh`.
