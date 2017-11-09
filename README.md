# dokku-build-env

**Note: dokku-build-env is deprecated in favour of the built-in build-env plugin (since dokku 0.3.9).**

Allows you to specify custom environment variables for the build stage of your app. Unlike [dokku-user-env-compile][1], these are not application-specific.

## Installation

```sh
cd /var/lib/dokku/plugins
git clone https://github.com/cameron-martin/dokku-build-env.git build-env
```

## Usage

Add any environment variables to `/home/dokku/BUILD_ENV`, like so

```sh
export VAR_NAME=value
```

### Example

Amazon S3 kept timing out when pushing, resulting in the following error

```
 !     Command: 'set -o pipefail; curl --fail --retry 3 --retry-delay 1 --connect-timeout 3 --max-time 30 https://s3-external-1.amazonaws.com/heroku-buildpack-ruby/ruby-2.0.0.tgz -s -o - | tar zxf -' failed unexpectedly:
 !      
 !     gzip: stdin: invalid compressed data--format violated
 !     tar: Unexpected EOF in archive
 !     tar: Unexpected EOF in archive
 !     tar: Error is not recoverable: exiting now
```

So I added the following to `/home/dokku/BUILD_ENV`

```sh
export CURL_TIMEOUT=60
export CURL_CONNECT_TIMEOUT=30
```

[1]: https://github.com/musicglue/dokku-user-env-compile
