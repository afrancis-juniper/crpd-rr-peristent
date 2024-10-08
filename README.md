# cRPD Route-Reflector Examples

This repository provides examples for how to achieve different outcomes targeted at containerized route reflector ("cRR") use cases. Examples contained herein do not construe recommendations but are available means to construct bespoke solutions for the particular requirements.

# Example

## Docker

- Juniper cRPD images
- `Docker compose` style initialization
- `nftables` for container-level firewall
- `macvlan` driver on docker
  - Layer 2 connectivity to physical network via dedicated interfaces from host VM/BMS

## Reference command to use

### Creating the container
`docker compose up -d` in the folder with the compose file or with the folder specified
 
### destroying the container
`docker compose down` in the folder with the compose file or with the folder specified

### show the running container 
`docker ps`

### show the active nftables

#### from from the docker host cli
`docker exec rr-crpd-1 sh -c "nft list table inet filter"` from the docker host cli

#### from the container bash
`docker exec -it rr-crpd-1 bash`
`nft list table inet filter`

### Add nftables entry to specific prefixes
`docker exec rr-crpd-1 nft add element inet filter SSHAllowed { 172.16.1.255 }`

### Copy the the active nft config from a specific container to file for persistance
`docker exec rr-crpd-1 sh -c "nft list rable inet filter > /etc/nftables.conf`
