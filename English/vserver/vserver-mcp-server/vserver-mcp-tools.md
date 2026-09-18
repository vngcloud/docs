# vServer MCP Tools

**vServer MCP Server** exposes **183 tools** with `--allow-write` and **84 tools** in the default read-only mode. Every tool follows the EKS-style `verb_noun` naming convention (`list_servers`, `create_volume`, `delete_security_group`) and maps 1:1 to the `greennode-cli` command name where one exists.

Every tool carries an MCP **ToolAnnotation**:

| Access        | Meaning                                                                                                      |
| ------------- | ------------------------------------------------------------------------------------------------------------ |
| `read`        | Idempotent, no state change. Available in read-only mode. Clients can auto-approve.                          |
| `write`       | Creates or modifies state. Requires `--allow-write`. Reversible, such as renaming a resource.                |
| `destructive` | Deletes state or overwrites data, such as rollback or delete. Requires `--allow-write`. Clients should warn. |

Data tools return structured Pydantic models. FastMCP emits `outputSchema` and `structuredContent` as JSON. Region is a fixed `Literal["HCM-3", "HAN"]`; every `list_*` output echoes the region it was fetched from.

### Guidance

| Tool                | Access | Description                                                                                 |
| ------------------- | ------ | ------------------------------------------------------------------------------------------- |
| `get_feature_guide` | read   | Step-by-step guide for a multi-step flow — call it **first** for any create or manage flow. |

`get_feature_guide` accepts one of:

* `getting_started`
* `create_server`
* `manage_server`
* `create_volume`
* `create_network`
* `secure_server`
* `snapshot_and_restore`
* `network_acl`
* `connect_networks`
* `high_availability`

Each guide describes a feature — a capability assembled from several tools — and is written in Vietnamese, like the other GreenNode MCP servers. The same ten guides are also available as MCP prompts under the `vserver_` prefix.

### Discovery

| Tool                      | Access | Description                                                  |
| ------------------------- | ------ | ------------------------------------------------------------ |
| `get_access_token`        | read   | Current IAM token, region, and endpoint.                     |
| `list_zones`              | read   | Enabled availability zones — step 1 of every creation flow.  |
| `get_zone`                | read   | One zone by ID; check `enabled` before placing a resource.   |
| `list_flavor_families`    | read   | Instance families (`general-purpose`, `gpu`).                |
| `list_flavor_codes`       | read   | CPU/GPU platform codes.                                      |
| `list_flavors`            | read   | Flavors of one family × code, filtered by zone and capacity. |
| `get_flavor`              | read   | One flavor by ID — what a server runs on today.              |
| `list_images`             | read   | Bootable OS or GPU images, with an optional name filter.     |
| `list_volume_types`       | read   | Disk IOPS tiers of a zone (NVMe preferred, SSD fallback).    |
| `get_volume_type`         | read   | One IOPS tier by ID.                                         |
| `get_default_volume_type` | read   | The tier vServer falls back to when none is given.           |
| `get_quota`               | read   | Project quota and current usage, per region.                 |

### Servers

<table><thead><tr><th width="195.734375">Tool</th><th width="128.59765625">Access</th><th>Description</th></tr></thead><tbody><tr><td><code>list_servers</code></td><td>read</td><td>Instances, with private/public IPs and zone.</td></tr><tr><td><code>get_server</code></td><td>read</td><td>One instance, with full nested detail.</td></tr><tr><td><code>list_server_interfaces</code></td><td>read</td><td>Internal and external NICs of a server.</td></tr><tr><td><code>list_server_security_groups</code></td><td>read</td><td>Attached groups plus effective inbound/outbound rules.</td></tr><tr><td><code>list_server_actions</code></td><td>read</td><td>Audit trail of creates, resizes, and reboots.</td></tr><tr><td><code>list_subnet_servers</code></td><td>read</td><td>Servers with an interface in one subnet.</td></tr><tr><td><code>get_server_console_url</code></td><td>read</td><td>Time-limited browser VNC console URL.</td></tr><tr><td><code>get_server_console_log</code></td><td>read</td><td>Serial-console output (tail) for boot and kernel failures.</td></tr><tr><td><code>get_server_external_interface</code></td><td>read</td><td>One attached elastic interface by ID.</td></tr><tr><td><code>create_server</code></td><td>write</td><td>Create an instance; billing and backup fields are deliberately excluded.</td></tr><tr><td><code>start_server</code></td><td>write</td><td>Power on.</td></tr><tr><td><code>stop_server</code></td><td>write</td><td>Power off.</td></tr><tr><td><code>reboot_server</code></td><td>write</td><td>Reboot.</td></tr><tr><td><code>resize_server</code></td><td>write</td><td>Change flavor; restarts the instance.</td></tr><tr><td><code>rename_server</code></td><td>write</td><td>Change the display name.</td></tr><tr><td><code>update_server_security_groups</code></td><td>write</td><td>Replace the attached group set.</td></tr><tr><td><code>create_server_image</code></td><td>write</td><td>Capture the instance as a reusable user image.</td></tr><tr><td><code>attach_server_internal_interface</code></td><td>write</td><td>Add private NICs on given subnets.</td></tr><tr><td><code>detach_server_internal_interfaces</code></td><td>destructive</td><td>Remove private NICs.</td></tr><tr><td><code>attach_server_internal_interface_floating_ip</code></td><td>write</td><td>Add private NICs that each come with a public IP.</td></tr><tr><td><code>detach_server_internal_interface_floating_ip</code></td><td>destructive</td><td>Remove those NICs and release their public IPs.</td></tr><tr><td><code>attach_server_external_interface</code></td><td>write</td><td>Move an elastic interface on.</td></tr><tr><td><code>detach_server_external_interface</code></td><td>destructive</td><td>Move an elastic interface off.</td></tr><tr><td><code>attach_server_floating_ip</code></td><td>write</td><td>Add a public IP to an interface.</td></tr><tr><td><code>detach_server_floating_ip</code></td><td>destructive</td><td>Remove a public IP from an interface.</td></tr><tr><td><code>delete_server</code></td><td>destructive</td><td>Delete the instance, optionally with its volumes.</td></tr></tbody></table>

### Storage

| Tool                       | Access      | Description                                                     |
| -------------------------- | ----------- | --------------------------------------------------------------- |
| `list_volumes`             | read        | Block-storage volumes.                                          |
| `get_volume`               | read        | One volume.                                                     |
| `list_server_volumes`      | read        | Volumes attached to one server.                                 |
| `get_server_boot_volume`   | read        | The root disk of a server.                                      |
| `list_volume_history`      | read        | Size and IOPS changes over a volume's life.                     |
| `list_persistent_volumes`  | read        | Kubernetes PVs backed by vServer storage.                       |
| `list_user_images`         | read        | Custom images captured from servers.                            |
| `get_user_image`           | read        | One user image.                                                 |
| `create_volume`            | write       | Create a volume in a zone.                                      |
| `resize_volume`            | write       | Grow a volume or change its IOPS tier.                          |
| `update_volume_type`       | write       | Move a volume to another IOPS tier only.                        |
| `rename_volume`            | write       | Change the display name.                                        |
| `attach_volume`            | write       | Attach to a server in the same zone.                            |
| `detach_volume`            | destructive | Detach; unmount inside the guest OS first.                      |
| `delete_volume`            | destructive | Delete a detached volume and its data.                          |
| `delete_persistent_volume` | destructive | Delete a Kubernetes PV; prefer deleting it through the cluster. |
| `delete_user_image`        | destructive | Delete a user image.                                            |

### Snapshots

| Tool                            | Access      | Description                                                                          |
| ------------------------------- | ----------- | ------------------------------------------------------------------------------------ |
| `list_snapshot_policies`        | read        | Schedule policies (cadence and retention) — the only source of a `snapshotPolicyId`. |
| `list_server_snapshots`         | read        | Snapshot points of a server.                                                         |
| `list_volume_snapshots`         | read        | Snapshot points of a volume.                                                         |
| `get_server_snapshot_policy`    | read        | Auto-snapshot configuration of a server (`configured=false` when unset).             |
| `get_volume_snapshot_policy`    | read        | Auto-snapshot configuration of a volume (IAM-gated).                                 |
| `list_shared_server_snapshots`  | read        | Who else may restore from this server's snapshots (IAM-gated).                       |
| `create_server_snapshot`        | write       | Take a server snapshot now, with a retention period.                                 |
| `create_volume_snapshot`        | write       | Take a volume snapshot now, with a retention period.                                 |
| `create_server_snapshot_policy` | write       | Set up the snapshot configuration of a server.                                       |
| `update_server_snapshot_policy` | write       | Switch schedule policy on a server.                                                  |
| `update_volume_snapshot_policy` | write       | Switch schedule policy on a volume.                                                  |
| `enable_server_auto_snapshot`   | write       | Start the server schedule.                                                           |
| `disable_server_auto_snapshot`  | write       | Stop the server schedule; points are kept.                                           |
| `enable_volume_auto_snapshot`   | write       | Start the volume schedule; needs the attached server ID.                             |
| `disable_volume_auto_snapshot`  | write       | Stop the volume schedule; points are kept.                                           |
| `rollback_server_snapshot`      | destructive | Revert a server to a point — **destroys everything written since**.                  |
| `rollback_volume_snapshot`      | destructive | Revert a volume to a point — **destroys everything written since**.                  |
| `delete_server_snapshot`        | destructive | Delete one server recovery point.                                                    |
| `delete_volume_snapshot`        | destructive | Delete one volume recovery point.                                                    |
| `delete_server_snapshot_policy` | destructive | Delete the configuration **and every point under it**.                               |
| `delete_volume_snapshot_policy` | destructive | Delete the configuration **and every point under it**.                               |
| `delete_shared_server_snapshot` | destructive | Revoke a share grant.                                                                |

### Networking

| Tool                               | Access      | Description                                                                             |
| ---------------------------------- | ----------- | --------------------------------------------------------------------------------------- |
| `list_vpcs`                        | read        | VPCs in the project.                                                                    |
| `get_vpc`                          | read        | One VPC.                                                                                |
| `list_active_vpcs`                 | read        | The API's own view of which VPCs are usable (IAM-gated).                                |
| `create_vpc`                       | write       | Create a VPC.                                                                           |
| `update_vpc`                       | write       | Rename a VPC.                                                                           |
| `delete_vpc`                       | destructive | Delete a VPC.                                                                           |
| `enable_vpc_dns`                   | write       | Turn on private DNS in a VPC; one-way, with no disable operation.                       |
| `list_subnets`                     | read        | Subnets of a VPC; a subnet pins a server's zone.                                        |
| `get_subnet`                       | read        | One subnet.                                                                             |
| `create_subnet`                    | write       | Create a subnet.                                                                        |
| `update_subnet`                    | write       | Update subnet fields; name is required on every call.                                   |
| `delete_subnet`                    | destructive | Delete a subnet.                                                                        |
| `create_secondary_subnet`          | write       | Add an extra CIDR to a subnet.                                                          |
| `delete_secondary_subnet`          | destructive | Remove an extra CIDR.                                                                   |
| `list_security_groups`             | read        | Security groups; `system=true` means platform-managed.                                  |
| `get_security_group`               | read        | One security group.                                                                     |
| `list_security_group_servers`      | read        | Servers a security group is attached to — its blast radius.                             |
| `create_security_group`            | write       | Create a security group.                                                                |
| `update_security_group`            | write       | Update the group; name is required on every call.                                       |
| `delete_security_group`            | destructive | Delete a security group.                                                                |
| `list_security_group_rules`        | read        | Rules of a group.                                                                       |
| `get_security_group_rule`          | read        | One rule.                                                                               |
| `list_security_group_rule_samples` | read        | The API's 30 named presets, including SSH, All TCP, and All ICMP.                       |
| `create_security_group_rule`       | write       | Add an allow-only, stateful rule.                                                       |
| `update_security_group_rule`       | write       | Update rule description and tags; protocol, ports, and CIDR are immutable.              |
| `delete_security_group_rule`       | destructive | Delete a rule.                                                                          |
| `list_floating_ips`                | read        | Public WAN IPs and whether they are attached.                                           |
| `list_elastic_ips`                 | read        | The console-side view of public addresses (IAM-gated).                                  |
| `delete_floating_ip`               | destructive | Release an address back to the pool.                                                    |
| `list_network_interfaces`          | read        | Elastic network interfaces.                                                             |
| `get_network_interface`            | read        | One elastic network interface.                                                          |
| `create_network_interface`         | write       | Create an elastic network interface.                                                    |
| `rename_network_interface`         | write       | Change the display name.                                                                |
| `update_network_interface_tags`    | write       | Replace the tag set.                                                                    |
| `delete_network_interface`         | destructive | Delete an elastic network interface.                                                    |
| `list_dhcp_options`                | read        | DHCP option sets.                                                                       |
| `get_dhcp_option`                  | read        | One DHCP option set.                                                                    |
| `list_dhcp_option_vpcs`            | read        | VPCs bound to a DHCP option set.                                                        |
| `create_dhcp_option`               | write       | Create a DHCP option set; two platform DNS servers are included, with up to four total. |
| `update_vpc_dhcp_option`           | write       | Bind or unbind a set to a VPC.                                                          |
| `delete_dhcp_option`               | destructive | Delete a DHCP option set.                                                               |

GreenNode system images move remote administration off the default ports: SSH listens on **234** and RDP on **3490**. `list_security_group_rule_samples` returns both the standard presets (`SSH` 22, `RDP` 3389) and the GreenNode presets (`SSH VNG` 234, `RDP VNG` 3490). Pick the preset based on the image, not by habit.

### Network ACLs, route tables, and peering

| Tool                         | Access      | Description                                                                        |
| ---------------------------- | ----------- | ---------------------------------------------------------------------------------- |
| `list_network_acls`          | read        | Subnet-level firewalls; `is_default` ACLs cannot be deleted.                       |
| `get_network_acl`            | read        | One ACL.                                                                           |
| `list_network_acl_rules`     | read        | Rules split by direction, in evaluation order.                                     |
| `create_network_acl`         | write       | Create an ACL in a VPC.                                                            |
| `update_network_acl_rules`   | write       | Replace the **whole** rule set; ACLs are stateless, so both directions are needed. |
| `update_network_acl_subnets` | write       | Set which subnets the ACL governs; full replacement.                               |
| `delete_network_acl`         | destructive | Delete an ACL; its subnets fall back to allow-all.                                 |
| `list_route_tables`          | read        | Route tables of a VPC.                                                             |
| `get_route_table`            | read        | One route table.                                                                   |
| `list_route_table_routes`    | read        | Static routes in a route table.                                                    |
| `create_route_table`         | write       | Create a route table; name must be 5–50 characters.                                |
| `update_route_table_routes`  | write       | Replace the **whole** route set.                                                   |
| `delete_route_table`         | destructive | Delete a route table.                                                              |
| `list_peerings`              | read        | VPC peerings; creating one goes through GreenNode support.                         |
| `delete_peering`             | destructive | Remove a peering; re-creation needs a support request.                             |

### Interconnect

| Tool                              | Access      | Description                                                          |
| --------------------------------- | ----------- | -------------------------------------------------------------------- |
| `list_interconnects`              | read        | Private circuits to on-premises, another cloud, or the other region. |
| `get_interconnect`                | read        | One circuit.                                                         |
| `list_interconnect_packages`      | read        | The bandwidth package catalogue.                                     |
| `list_interconnect_circuit_types` | read        | The circuit-type catalogue (IAM-gated).                              |
| `list_interconnect_connections`   | read        | VPC attachments on a circuit.                                        |
| `get_interconnect_connection`     | read        | One VPC attachment.                                                  |
| `create_interconnect`             | write       | Order a circuit — **contracted and monthly billed**.                 |
| `update_interconnect`             | write       | Update description, tags, or gateway-2 redundancy.                   |
| `update_interconnect_package`     | write       | Change committed bandwidth — **changes the price**.                  |
| `create_interconnect_connection`  | write       | Attach a VPC to a circuit.                                           |
| `update_interconnect_connection`  | write       | Change the remote CIDRs of an attachment; full replacement.          |
| `ping_interconnect`               | write       | Diagnostic reachability test; changes nothing.                       |
| `delete_interconnect_connection`  | destructive | Detach a VPC from a circuit.                                         |
| `delete_interconnect`             | destructive | Remove the circuit.                                                  |

### Virtual IPs

| Tool                                          | Access      | Description                                         |
| --------------------------------------------- | ----------- | --------------------------------------------------- |
| `list_virtual_ips`                            | read        | Shared addresses for HA pairs, private and public.  |
| `get_virtual_ip`                              | read        | One virtual IP.                                     |
| `list_virtual_ip_address_pairs`               | read        | Which interfaces answer for a private VIP.          |
| `get_virtual_ip_address_pair`                 | read        | One address pair.                                   |
| `list_virtual_ip_candidate_interfaces`        | read        | Internal interfaces eligible to join a private VIP. |
| `list_public_virtual_ip_candidate_interfaces` | read        | External interfaces eligible to join a public VIP.  |
| `list_secondary_subnet_address_pairs`         | read        | Interfaces bound to a secondary subnet.             |
| `create_virtual_ip`                           | write       | Create a private VIP.                               |
| `update_virtual_ip`                           | write       | Rename or change the mode of a private VIP.         |
| `create_public_virtual_ip`                    | write       | Create a public VIP; consumes a public IP.          |
| `create_virtual_ip_address_pair`              | write       | Bind an instance's interface to a private VIP.      |
| `create_public_virtual_ip_address_pair`       | write       | Bind an external interface to a public VIP.         |
| `create_secondary_subnet_address_pair`        | write       | Bind an interface to a secondary subnet.            |
| `delete_virtual_ip_address_pair`              | destructive | Unbind an interface from a private VIP.             |
| `delete_public_virtual_ip_address_pair`       | destructive | Unbind an external interface from a public VIP.     |
| `delete_secondary_subnet_address_pair`        | destructive | Unbind from a secondary subnet.                     |
| `delete_virtual_ip`                           | destructive | Release the shared private address.                 |
| `delete_public_virtual_ip`                    | destructive | Release the shared public address.                  |

### Keys, placement, and tags

| Tool                            | Access      | Description                                                         |
| ------------------------------- | ----------- | ------------------------------------------------------------------- |
| `list_ssh_keys`                 | read        | SSH keys registered in the project.                                 |
| `get_ssh_key`                   | read        | One SSH key.                                                        |
| `create_ssh_key`                | write       | Generate a pair; the private key is returned **once**.              |
| `import_ssh_key`                | write       | Register an existing public key (preferred).                        |
| `delete_ssh_key`                | destructive | Remove a key.                                                       |
| `list_placement_groups`         | read        | Placement groups and their servers.                                 |
| `get_placement_group`           | read        | One placement group.                                                |
| `list_placement_group_policies` | read        | Affinity and anti-affinity policies.                                |
| `create_placement_group`        | write       | Create a placement group.                                           |
| `update_placement_group`        | write       | Rename or change the policy.                                        |
| `delete_placement_group`        | destructive | Delete an empty placement group.                                    |
| `list_tag_keys`                 | read        | Tag keys in the project.                                            |
| `list_tag_values`               | read        | Values used with one tag key.                                       |
| `list_resource_tags`            | read        | Tags attached to one resource.                                      |
| `list_tags`                     | read        | Every tag object in the project; system tags are hidden by default. |
| `get_tag_quota`                 | read        | How many tags one resource may carry.                               |
| `update_resource_tags`          | write       | Replace a resource's whole tag list.                                |

### Prompts

Ten guided flows are available as MCP prompts in Vietnamese. They are portable across MCP clients and always available; they do not require `--allow-write`.

Each prompt is also served through the `get_feature_guide` **tool**, using the same text as the single source of truth. Prompts must be loaded by the user, while agents call the tool on their own.

| Prompt                         | Covers                                                                            |
| ------------------------------ | --------------------------------------------------------------------------------- |
| `vserver_getting_started`      | Object model, regions/zones, and how tools chain together.                        |
| `vserver_create_server`        | Discovery → validate → confirm → create → poll for an instance.                   |
| `vserver_manage_server`        | Power, resize, rename, attach/detach interfaces, and security groups.             |
| `vserver_create_volume`        | Volume tiers, zone rules, and attach flow.                                        |
| `vserver_create_network`       | VPC, subnet, and security group from scratch.                                     |
| `vserver_secure_server`        | Security-group presets, ACLs, and keeping ports off the defaults.                 |
| `vserver_snapshot_and_restore` | Point-in-time protection, retention, rollback, and restore.                       |
| `vserver_network_acl`          | Subnet-level firewalls, stateless behaviour, platform rules, and replacement PUT. |
| `vserver_connect_networks`     | Peering and interconnect — when to use which.                                     |
| `vserver_high_availability`    | Virtual IPs, secondary subnets, and placement groups for HA pairs.                |

### Not covered

* **Bandwidth** (Network → Bandwidth in the console) has no public API — it is console-only. The `bandwidth` field on a flavor is its NIC speed, which is a different thing.
* Marketplace, server live migration, custom flavor/zone allocation, and a few redundant internal endpoints are deliberately left out. See the package `CLAUDE.md` for the reason for each endpoint.
