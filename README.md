# corosync Cookbook

Installs corosync, and configures authkey-based communication with explicitly defined cluster members.

Requires encrypted data bags.

## Usage
Create a 1024-bit authkey and get its base64 value so it can be placed in an encrypted data bag.

From an existing authkey, e.g.: `openssl base64 < /etc/corosync/authkey | tr -d '\n'`

Or generate your own: `openssl rand 128 -base64 | tr -d '\n'`

It will be pulled from `data_bag_item('keys', 'corosync')['authkey']`.

Add all the members to `default['corosync']['members']` and set each
`node['corosync']['bindnetaddr']` to the IP to bind to.

## Testing

The tests depend on all defined nodes being up, since it checks that members have joined. To ensure nodes are converged before verify, you can do all the steps in order:

```bash
kitchen converge && kitchen verify
```

Contributing
------------
The usual: fork, topic branch, test, pull req.

Authors
-------------------
* [Joshua Yotty](https://github.com/jyotty)
