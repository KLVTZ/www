---
page_title: "Using Vault with Consul Template"
title: "Using Vault with Consul Template"
list_image_url: "/images/blog/using-vault-with-consul-template/ct-vault.png"
post_image_url: "/images/blog/using-vault-with-consul-template/ct-vault.png"
tags: vault
author: Seth Vargo
---

Today we announce first-class support for [Vault](https://vaultproject.io) in Consul Template. Consul Template is a key tool for generating configurations and managing infrastructure, and we believe that Vault is going to change the way organizations think about and manage their secret data. As such, we are building first-class support for Vault in Consul Template. This allows users to seemless integrate secret data into the configurations.

READMORE

Last October we [announced Consul Template](https://www.hashicorp.com/blog/introducing-consul-template.html), a standalone application that renders data from Consul onto the file system. Since then, Consul Template has grown to new scales and is one of our most popular Consul tools. Today we are excited to bring an amazing new feature to Consul Template - first class support for [Vault](https://vaultproject.io?utm_source=Consul+Template).

[Announced yesterday](https://www.hashicorp.com/blog/vault.html), Vault is HashiCorp's newest open source tool that provides a unified solution for secure key and secret management complete with in-transit encryption, key rolling, key revocation, and detailed audit logs.

## Demo

<iframe src="https://player.vimeo.com/video/126398526" width="740" height="375" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

## Use Cases

Consul Template's powerful abstraction and templating language are perfect for creating dynamic configurations. Using Consul Template with Vault will feel friendly and familiar:

    ---
    production:{{with $secret := vault "secret/my-app/production" }}
      adapter: postgresql
      host: {{key "my-app/production/host"}}
      username: {{$secret.Data.username}}
      password: {{$secret.Data.password}}
    {{end}}

This example combines existing functionality of watching a key in Consul and the new `vault` function which queries a Vault instance for a secret. Consul Template transparently handles the authentication, retrieval, and renewal of secrets. You can read more about the new Vault integration in [Consul Template's GitHub repository](https://github.com/hashicorp/consul-template).

## Conclusion

Consul Template has changed the way organizations manage service discovery and configuration. Vault has changed the way organizations manage keys and secrets in distributed systems. Together Consul Template and Vault can be the foundation for service discovery and service configuration in the modern datacenter. Since both Vault and Consul Template are **open source**, you can view the source code and discover just how the integration works. Please join me in welcoming the newest integration to Consul Template!
