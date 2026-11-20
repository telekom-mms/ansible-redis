<!-- BEGIN_ANSIBLE_DOCS -->

# Ansible role telekom_mms.redis

Highly configurable role to install Redis and Redis Sentinel from source

## Contents

1. [Supported Operating Systems](#supported-operating-systems)
2. [Role Variables](#role-variables)
3. [Dependencies](#dependencies)
4. [Requirements](#requirements)
5. [Getting Started](#getting-started)
  1. [Single Redis node](#single-redis-node)
  2. [Primary-Replica Replication](#primary-replica-replication)
  3. [Redis Sentinel](#redis-sentinel)
6. [Advanced Options](#advanced-options)
  1. [Install from local tarball](#install-from-local-tarball)
  2. [Install inside restricted environments](#install-inside-restricted-environments)
  3. [Building with TLS support](#building-with-tls-support)
8. [Author Information](#author-information)
9. [License](#license)

## Supported Operating Systems

- Ubuntu
  - jammy, noble, resolute
- Debian
  - bookworm, trixie
- EL
  - 9, 10
- opensuse
  - all

## Role Variables

- `redis_appendfilename`
  - Default: `appendonly.aof`
  - Description: Filename used for the append-only file.
  - Type: str
  - Required: no

- `redis_appendfsync`
  - Default: `everysec`
  - Description: fsync policy for the append-only file.
  - Type: str
  - Required: no

- `redis_appendonly`
  - Default: `no`
  - Description: Enable append-only file persistence.
  - Type: str
  - Required: no

- `redis_as_service`
  - Default: `True`
  - Description: Configure Redis to run as a service.
  - Type: bool
  - Required: no

- `redis_auto_aof_rewrite_min_size`
  - Default: `64mb`
  - Description: Minimum append-only file size before automatic rewrite.
  - Type: str
  - Required: no

- `redis_auto_aof_rewrite_percentage`
  - Default: `100`
  - Description: Append-only file rewrite threshold as a percentage.
  - Type: str
  - Required: no

- `redis_bind`
  - Default: `0.0.0.0`
  - Description: Address to which Redis binds.
  - Type: raw
  - Required: no

- `redis_checksum`
  - Default: ``
  - Description: Optional checksum override in algorithm:digest format.
  - Type: str
  - Required: no

- `redis_client_output_buffer_limit_normal`
  - Default: `0 0 0`
  - Description: Output-buffer limit for normal clients.
  - Type: str
  - Required: no

- `redis_client_output_buffer_limit_pubsub`
  - Default: `32mb 8mb 60`
  - Description: Output-buffer limit for Pub/Sub clients.
  - Type: str
  - Required: no

- `redis_client_output_buffer_limit_slave`
  - Default: `256mb 64mb 60`
  - Description: Output-buffer limit for replica clients.
  - Type: str
  - Required: no

- `redis_config_additional`
  - Default: ``
  - Description: Additional Redis configuration directives.
  - Type: str
  - Required: no

- `redis_config_file_name`
  - Default: `{{ redis_port }}.conf`
  - Description: Name of the Redis configuration file.
  - Type: str
  - Required: no

- `redis_daemonize`
  - Default: `yes`
  - Description: Run Redis as a daemon.
  - Type: str
  - Required: no

- `redis_databases`
  - Default: `16`
  - Description: Number of Redis databases.
  - Type: int
  - Required: no

- `redis_db_filename`
  - Default: `dump.rdb`
  - Description: Filename used for the RDB backup.
  - Type: str
  - Required: no

- `redis_dir`
  - Default: `/var/lib/redis/{{ redis_port }}`
  - Description: Working directory used by Redis.
  - Type: str
  - Required: no

- `redis_download_url`
  - Default: `http://download.redis.io/releases/redis-{{ redis_version }}.tar.gz`
  - Description: URL used to download the Redis source archive.
  - Type: str
  - Required: no

- `redis_group`
  - Default: `{{ redis_user }}`
  - Description: System group used by the Redis user.
  - Type: str
  - Required: no

- `redis_hz`
  - Default: `10`
  - Description: Redis internal task frequency in hertz.
  - Type: int
  - Required: no

- `redis_install_dir`
  - Default: `/opt/redis`
  - Description: Directory where Redis is installed.
  - Type: str
  - Required: no

- `redis_install_from_source`
  - Default: `True`
  - Description: Install Redis from source instead of a system package.
  - Type: bool
  - Required: no

- `redis_local_facts`
  - Default: `True`
  - Description: Install local Ansible facts for Redis.
  - Type: bool
  - Required: no

- `redis_logfile`
  - Default: `""`
  - Description: Redis log file; an empty value logs to standard output.
  - Type: str
  - Required: no

- `redis_loglevel`
  - Default: `notice`
  - Description: Redis logging verbosity.
  - Type: str
  - Required: no

- `redis_lua_time_limit`
  - Default: `5000`
  - Description: Maximum execution time for a Lua script in milliseconds.
  - Type: int
  - Required: no

- `redis_make_tls`
  - Default: `False`
  - Description: Build Redis with TLS support.
  - Type: bool
  - Required: no

- `redis_maxclients`
  - Default: `10000`
  - Description: Maximum number of simultaneous clients.
  - Type: int
  - Required: no

- `redis_maxmemory`
  - Default: `False`
  - Description: Maximum Redis memory in a Redis-supported format, or false for no limit.
  - Type: raw
  - Required: no

- `redis_maxmemory_policy`
  - Default: `noeviction`
  - Description: Key eviction policy used when Redis reaches its memory limit.
  - Type: str
  - Required: no

- `redis_min_slaves_max_lag`
  - Default: `10`
  - Description: Maximum replica lag in seconds for write availability.
  - Type: int
  - Required: no

- `redis_min_slaves_to_write`
  - Default: `0`
  - Description: Minimum number of replicas that must be available for writes.
  - Type: int
  - Required: no

- `redis_no_appendfsync_on_rewrite`
  - Default: `no`
  - Description: Avoid fsync during rewrites when enabled.
  - Type: str
  - Required: no

- `redis_nofile_limit`
  - Default: `16384`
  - Description: Open-file limit for Redis and Sentinel.
  - Type: int
  - Required: no

- `redis_notify_keyspace_events`
  - Default: `""`
  - Description: Keyspace notification events to publish.
  - Type: str
  - Required: no

- `redis_oom_score_adjust`
  - Default: `0`
  - Description: OOM killer score adjustment for Redis.
  - Type: int
  - Required: no

- `redis_password`
  - Default: `False`
  - Description: Password required to authenticate to Redis.
  - Type: raw
  - Required: no

- `redis_pidfile`
  - Default: `/var/run/redis/{{ redis_port }}.pid`
  - Description: Path to the Redis process ID file.
  - Type: str
  - Required: no

- `redis_port`
  - Default: `6379`
  - Description: TCP port on which Redis listens.
  - Type: int
  - Required: no

- `redis_rdbchecksum`
  - Default: `yes`
  - Description: Add checksums to RDB files.
  - Type: str
  - Required: no

- `redis_rdbcompression`
  - Default: `yes`
  - Description: Compress RDB files.
  - Type: str
  - Required: no

- `redis_rename_commands`
  - Default: `[]`
  - Description: Redis commands to rename or disable, in command and replacement pairs.
  - Type: list of 'str'
  - Required: no

- `redis_repl_backlog_size`
  - Default: `False`
  - Description: Replication backlog size, or false to use the Redis default.
  - Type: raw
  - Required: no

- `redis_save`
  - Default: `['900 1', '300 10', '60 10000']`
  - Description: RDB snapshot save rules.
  - Type: list of 'str'
  - Required: no

- `redis_sentinel`
  - Default: `False`
  - Description: Configure this host as a Redis Sentinel.
  - Type: bool
  - Required: no

- `redis_sentinel_bind`
  - Default: `0.0.0.0`
  - Description: Address to which Sentinel binds.
  - Type: str
  - Required: no

- `redis_sentinel_dir`
  - Default: `/var/lib/redis/sentinel_{{ redis_sentinel_port }}`
  - Description: Working directory used by Sentinel.
  - Type: str
  - Required: no

- `redis_sentinel_logfile`
  - Default: `""`
  - Description: Sentinel log file; an empty value logs to standard output.
  - Type: str
  - Required: no

- `redis_sentinel_monitors`
  - Default: `[{'name': 'primary01', 'host': 'localhost', 'port': 6379, 'quorum': 2, 'auth_pass': 'ant1r3z', 'down_after_milliseconds': 30000, 'parallel_syncs': 1, 'failover_timeout': 180000, 'notification_script': False, 'client_reconfig_script': False, 'rename_commands': []}]`
  - Description: Sentinel primary instances to monitor and their failover settings.
  - Type: list of 'dict'
  - Required: no

- `redis_sentinel_oom_score_adjust`
  - Default: `0`
  - Description: OOM killer score adjustment for Sentinel.
  - Type: int
  - Required: no

- `redis_sentinel_pidfile`
  - Default: `/var/run/redis/sentinel_{{ redis_sentinel_port }}.pid`
  - Description: Path to the Sentinel process ID file.
  - Type: str
  - Required: no

- `redis_sentinel_port`
  - Default: `26379`
  - Description: TCP port on which Sentinel listens.
  - Type: int
  - Required: no

- `redis_sentinel_syslog_ident`
  - Default: `sentinel_{{ redis_sentinel_port }}`
  - Description: Identifier used for Sentinel syslog messages.
  - Type: str
  - Required: no

- `redis_server`
  - Default: `True`
  - Description: Install and configure the Redis server.
  - Type: bool
  - Required: no

- `redis_service_name`
  - Default: `redis_{{ redis_port }}`
  - Description: Name of the Redis service.
  - Type: str
  - Required: no

- `redis_slave_priority`
  - Default: `100`
  - Description: Replica priority used during failover.
  - Type: int
  - Required: no

- `redis_slave_read_only`
  - Default: `yes`
  - Description: Whether replicas reject write commands.
  - Type: str
  - Required: no

- `redis_slaveof`
  - Default: `False`
  - Description: Replication primary in host port format, or false to disable replication.
  - Type: raw
  - Required: no

- `redis_slowlog_log_slower_than`
  - Default: `10000`
  - Description: Slow-log queries taking longer than this many microseconds.
  - Type: int
  - Required: no

- `redis_slowlog_max_len`
  - Default: `128`
  - Description: Maximum number of slow-log entries to retain.
  - Type: int
  - Required: no

- `redis_socket_path`
  - Default: `False`
  - Description: Unix socket path, or false to disable the socket.
  - Type: raw
  - Required: no

- `redis_socket_perm`
  - Default: `755`
  - Description: Permissions for the Unix socket.
  - Type: int
  - Required: no

- `redis_stop_writes_on_bgsave_error`
  - Default: `yes`
  - Description: Stop writes when a background save fails.
  - Type: str
  - Required: no

- `redis_syslog_enabled`
  - Default: `yes`
  - Description: Enable Redis syslog logging.
  - Type: str
  - Required: no

- `redis_syslog_facility`
  - Default: `USER`
  - Description: Syslog facility used by Redis.
  - Type: str
  - Required: no

- `redis_syslog_ident`
  - Default: `{{ redis_service_name }}`
  - Description: Identifier used for Redis syslog messages.
  - Type: str
  - Required: no

- `redis_tarball`
  - Default: `False`
  - Description: Local source archive path, or false to download the archive.
  - Type: raw
  - Required: no

- `redis_tcp_backlog`
  - Default: `511`
  - Description: TCP listen backlog for Redis.
  - Type: int
  - Required: no

- `redis_tcp_keepalive`
  - Default: `0`
  - Description: TCP keepalive interval in seconds.
  - Type: int
  - Required: no

- `redis_timeout`
  - Default: `0`
  - Description: Client idle timeout in seconds; zero disables the timeout.
  - Type: int
  - Required: no

- `redis_user`
  - Default: `redis`
  - Description: System user that runs Redis.
  - Type: str
  - Required: no

- `redis_verify_checksum`
  - Default: `False`
  - Description: Retrieve and verify the source archive checksum.
  - Type: bool
  - Required: no

- `redis_version`
  - Default: `2.8.24`
  - Description: Redis version to install.
  - Type: str
  - Required: no


## Dependencies

None.

## Requirements

Source builds on Red Hat-family and SUSE systems require `gcc`, `gcc-c++`, and `make`,
which the role installs automatically.

The role requires the following Ansible collections:

```yaml
---
collections:
  - name: ansible.posix
  - name: community.general

```

```bash
ansible-galaxy collection install -r requirements.yml
```

## Getting Started

### Single Redis node

```yaml
- hosts: all
  vars:
    redis_version: 8.10.3
    redis_bind: 127.0.0.1
  roles:
    - telekom_mms.redis
```

### Primary-Replica Replication

Configuring [replication](http://redis.io/topics/replication) in Redis is accomplished by deploying multiple nodes and setting the `redis_slaveof` variable on the replica nodes, just as you would in the redis.conf. In the example that follows, we'll deploy a Redis primary with three replicas.

``` ini
[redis-primary]
redis-primary

[redis-replica]
redis-replica0[1:3]
```

```yaml
- hosts: redis-primary
  vars:
    redis_version: 8.10.3
  roles:
    - telekom_mms.redis
```

```yaml
- hosts: redis-replica
  vars:
    redis_version: 8.10.3
    redis_bind: 0.0.0.0
    redis_slaveof: redis-primary 6379
  roles:
    - telekom_mms.redis
```

This setup assumes that you have DNS records for `redis-primary` and `redis-replica` nodes. To be more flexible you can define something like this:

```yaml

redis_slaveof: "{{ hostvars['redis-primary'].ansible_facts.default_ipv4.address }} {{ redis_port }}"

```

Running this playbooks will set up a Redis primary with three replicas, using the specified `redis_slaveof` configuration to establish replication.

### Redis Sentinel

Primary-replica replication is useful for durability and distributing reads and writes, but by itself does not provide high availability. If the primary fails, a replica must be promoted and connections redirected to the new primary. [Redis Sentinel](http://redis.io/topics/sentinel) provides automatic failover in a Redis deployment.

Sentinel itself uses the same redis-server binary that Redis uses, but runs with the `--sentinel` flag and with a different configuration file.

```yaml
- hosts: redis-sentinel-primary
  vars:
    redis_version: 8.10.3
    redis_bind: 0.0.0.0
    redis_sentinel: true
    redis_sentinel_monitors:
      - name: primary
        host: redis-sentinel-primary
        port: 6379
        down_after_milliseconds: 10000
    redis_sentinel_config_additional: |
      sentinel resolve-hostnames yes
      sentinel announce-hostnames yes
  roles:
    - telekom_mms.redis
```

```yaml
- hosts: redis-sentinel-replica
  vars:
    redis_version: 8.10.3
    redis_bind: 0.0.0.0
    redis_slaveof: redis-sentinel-primary 6379
    redis_sentinel: true
    redis_sentinel_monitors:
      - name: primary
        host: redis-sentinel-primary
        port: 6379
        down_after_milliseconds: 10000
    redis_sentinel_config_additional: |
      sentinel resolve-hostnames yes
      sentinel announce-hostnames yes
  roles:
    - telekom_mms.redis
```

This playbook sets up Redis with Sentinel for high availability, ensuring that if the primary node fails, a replica can be promoted automatically. It is recommended to have at least three Sentinel nodes to achieve a quorum for failover decisions.

For more information on Redis Sentinel, refer to the [official Redis Sentinel documentation](http://redis.io/topics/sentinel).

## Install from local tarball

To install Redis from a local tarball, set the `redis_tarball` variable to the path of the tarball file. For example:

```yaml
- hosts: redis
  vars:
    redis_version: 8.10.3

    redis_tarball: /path/to/redis-{{ redis_version }}.tar.gz

  roles:
    - telekom_mms.redis
```

## Install inside restricted environments (e.g. containerized environments)

If Redis is to be installed inside a systemctl restricted environment, it might be neccessary to change `vm.overcommit_memory` using other means than this role. In such a case the config key `redis_inside_container` can be defined, which causes the role to skip this setting.

## Building with TLS support

To build Redis with TLS support, set the `redis_make_tls` variable to `true`. Note that this requires OpenSSL development libraries to be available on the system.

```yaml
- hosts: redis
  vars:
    redis_version: 8.10.3
    redis_make_tls: true
  roles:
    - telekom_mms.redis
```

## Facts

The following facts are accessible in your inventory or tasks outside of this role.


- `{{ ansible_local.redis.bind }}`
- `{{ ansible_local.redis.port }}`
- `{{ ansible_local.redis.sentinel_bind }}`
- `{{ ansible_local.redis.sentinel_port }}`
- `{{ ansible_local.redis.sentinel_monitors }}`


To disable these facts, set `redis_local_facts` to a false value.

## Author Information

- David Wittman
- rndmh3ro
- beechesII

## License

MIT

## Testing

Run `molecule test -s single_node`, `molecule test -s primary_replica`, or
`molecule test -s sentinel`. Running `molecule test` without a scenario uses
`default`, an entry point for the single-node test.

Set `REDIS_VERSION`, `REDIS_MAKE_TLS`, and `MOLECULE_IMAGE` to select the build
and container image. `REDIS_MAKE_TLS` enables TLS compilation, not encrypted
connections. Multi-container tests disable Redis protected mode only on their
isolated Docker networks; no Redis ports are published to the host.

<!-- END_ANSIBLE_DOCS -->
