# Gaufrette Extras 

[![Quality Score](https://img.shields.io/scrutinizer/g/KnpLabs/Gaufrette-extras.svg?style=flat-square)](https://scrutinizer-ci.com/g/KnpLabs/Gaufrette-extras)
[![Packagist Version](https://img.shields.io/packagist/v/KnpLabs/Gaufrette-extras.svg?style=flat-square)](https://packagist.org/packages/KnpLabs/Gaufrette-extras)
[![Total Downloads](https://img.shields.io/packagist/dt/KnpLabs/Gaufrette-extras.svg?style=flat-square)](https://packagist.org/packages/KnpLabs/Gaufrette-extras)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE)
[![Tests](https://github.com/KnpLabs/gaufrette-extras/actions/workflows/ci.yml/badge.svg)](https://github.com/KnpLabs/gaufrette-extras/actions/workflows/ci.yml)

Provides extras functionality around Gaufrette like Resolvable filesystem.

### Resolvable filesystem

`ResolvableFilesystem` is a decorator permitting to resolve objects paths into URLs.

In order to use it, you have to pass the decorated Filesystem and a Resolver:

    $client     = // AwsS3 client instantiation
    $decorated  = new Filesystem(new AwsS3($client, 'my_bucket', ['directory' => 'root/dir']));
    $filesystem = new ResolvableFilesystem(
        $decorated,
        new AwsS3PresignedUrlResolver($client, 'my_bucket', 'root/dir', new \DateTime('+ 1 hour'))
    );

Then you can call `resolve($key)`:

    $filesystem->resolve('/foo.png'); // = 'https://...

Currently these resolvers are supported:

* AwsS3PublicUrlResolver
* AwsS3PresignedUrlResolver
* StaticUrlResolver
