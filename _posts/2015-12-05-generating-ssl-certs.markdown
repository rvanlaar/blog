---
layout: post
title: "Generating SSL Certificates"
modified:
categories:
excerpt: A simple guide to follow when generating secure SSL certificates.
tags: [ SSL, RSA, self signed certificates]
image:
  feature:
date: 2015-12-05T11:58:51+00:00
---


## How to Generate SSL Certificates

There is lots to know about SSL and generating secure certificates.
If you only want to know the commands to get a certificate follow this guide.

Save this configuration file as `cert.conf`.
Fill in your own values for the `CN` (Common Name), emailAddress, `O` (Organisation), `L` (Location) and `C` (Country). Don't forget to change the `PASSPHRASE`.
Fill in the `subjectAltName` for all the domains you want in this certificate.

{% highlight ini %}
[req]
prompt = no
distinguished_name = dn
req_extensions = ext
input_password = PASSPHRASE

[dn]
CN = micite.net
emailAddress = webmaster@micite.net
O = R. van Laar Automatisering
L = Utrecht
C = NL

[ext]
subjectAltName = DNS:micite.net,DNS:www.micite.net

{% endhighlight %}

## RSA key generation

{% highlight bash %}
openssl genrsa -out rsa.key 2048
openssl req -new -config cert.conf -key rsa.key -out rsa.csr -sha256
{% endhighlight %}

This creates two files:

 * rsa.key: Your private key, don't give this to anyone
 * rsa.csr: A Certificate Signing Request. Upload this file to your SSL seller. You will receive a signed certificate.

### Self Signing

If you want to self sign the request for use this:
{% highlight bash %}
openssl x509 -req -days 365 -in rsa.csr  -signkey rsa.key -out rsa.crt -sha256
{% endhighlight %}
This gives you rsa.crt, your public key. This certificate is valid for a year.

## Elliptic Curve

Do you want a more modern key? Elliptic Curve cryptography has smaller key sizes compared to RSA. A 256-bit public key is as secure as a 3072-bit RSA public key.

{% highlight bash %}
openssl ecparam -genkey -name secp256r1 -out ec.param
openssl ec -in ec.param -out ec.key
openssl req -new -config cert.conf -key ec.key -out ec.csr
{% endhighlight %}

This creates three files:

 * ec.param: Specifies the elliptic curve used
 * ec.key: The private key
 * ec.csr: A Certificate Signing Request. Upload this file to your SSL seller.

### Self Signing

If you want to self sign the request for use this:
{% highlight bash %}
openssl x509 -req -days 365 -in ec.csr -signkey ec.key -out ec.crt -sha256
{% endhighlight %}
This gives you ec.crt, your public key. This certificate is valid for a year.

## The OpenSSL Cookbook

If you want to know more, I highly recommend this book:
[OpenSSL Cookbook](https://www.feistyduck.com/library/openssl-cookbook/)