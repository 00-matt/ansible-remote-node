# ansible-remote-node

[Ansible][] playbook for deploying Wownero remote nodes.

## Funding

Part of a project funded by the Wownero community. Thank you :)

See the [WFS Proposal][] for more info.

## Usage

### Setup

1. Install ansible if you don't have it already.
   You can do this in a virtualenv if you don't want to install it system-wide.
   
	```bash
	python -m venv virtualenv
	pip install -r requirements.txt
	```

2. Configure the inventory.
   Modify `inventory.ini` with the connection details of your server.

3. Run the playbook.
   
	```bash
	ansible-playbook -i inventory.ini site.yaml
	```

4. Enjoy your daemon!

### Further Configuration

The P2P and RPC listening ports can be configured with the variables
`wownerod_p2p_port` and `wownerod_rpc_port` respectively.

You can set them for a single host in your inventory like this:

```ini
daemon.example.com wownerod_p2p_port=12345 wownerod_rpc_port=12346
```

Or you can set them for all hosts:

```ini
[all]
daemon.example.com
daemon2.example.com

[all:vars]
wownerod_p2p_port=12345
wownerod_rpc_port=12346
```

### Upgrading `wownerod`

Edit `wownerod_remote_url`, `wownerod_remote_hash`, and
`wownero_version` in `roles/wownerod/defaults/main.yaml` to point to a
newer `wownerod` binary and re-run the playbook. It is recommended to
test the update on a single host first before deploying to the rest of
the pool.

Will be updated to use the official release binaries in the future,
but they currently do not support distros with an older version of
glibc (e.g. Debian Stable) so a binary built on Debian 10 is provided.

### HA Notice

The RPC server works great when behind HAProxy, nginx, or a DNS
solution like Constellix. However you'll need to extend the playbook
yourself for that.

## License

Released under the terms of the [Unlicense][].
See UNLICENSE file in project root for more info.

[Ansible]: https://www.ansible.com/  "Ansible homepage"
[WFS Proposal]: https://funding.wownero.com/proposal/44  "Funding request"
[Unlicense]: https://unlicense.org/  "Unlicense homepage"
