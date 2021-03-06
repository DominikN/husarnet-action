# Husarnet VPN Action for GitHub Actions

[beta] Connecting to Husarnet VPN network

## Usage

```yaml
name: Ping other peer from a VPN network

on: push

jobs:
  build:
    runs-on: ubuntu-20.04
    steps:

    - name: Connecting to Husarnet VPN network
      uses: husarnet-actions/husarnet@v1
      with:
        join-code: ${{ secrets.HUSARNET_JOINCODE }}

    - name: Print Husarnet IPv6 addr
      run: echo ${{ steps.husarnet.outputs.ipv6 }}

    - name: Ping other peer
      run: ping6 -c 10 my-laptop
```

## Inputs

```yaml
    - name: Husarnet VPN
      uses: husarnet-actions/husarnet@v1
      with:
        join-code: ${{ secrets.HUSARNET_JOINCODE }}
        hostname: my-hostname
        cache-key: husarnet-v
```

| input | required | default value | description |
| - | - | - | - |
| `join-code` | yes |  | A Join Code for the Husarnet network you want to connect to. Find your Join Code at https://app.husarnet.com/  |
| `hostname` | no | `my-github-action` | A hostname under which this workflow will be available in your Husarnet network. |
| `cache-key` | no | `husarnet-volume` | Thanks to cache, IPv6 address will be the same in the following job runs. Another cache means generating another peer. Useful while using matrix. |

## Outputs

```yaml
    - name: Husarnet VPN
      id: husarnet
      uses: husarnet-actions/husarnet@v1
      with:
        join-code: ${{ secrets.HUSARNET_JOINCODE }}
        hostname: my-hostname
        cache-key: husarnet-v
    
    - name: Print IPv6
      run: My IPv6 addr is ${{ steps.husarnet.outputs.ipv6 }}
```

| output | description |
| - | - |
| `ipv6` | Husarnet IPv6 address of the peer |